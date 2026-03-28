# box_name_coding: ボックス名コーディング

## 実行フロー

ACE発動 → gPokemonStorage先頭から実行開始 → ポケモンデータ領域がNOPスライドとして通過 → offset 0x8344のボックス名に到達 → ペイロード実行

## 文字エンコーディング制約

- Gen3独自エンコーディング (非ASCII)
- 256バイト値のうち入力可能は約1/3
- 0xFF = 文字列終端子 → 使用不可
- 1ボックス名 = 8文字 + 0xFF = 9バイト
- 14ボックス × 9バイト = 合計126バイトのペイロード領域

日本語版: ひらがな+カタカナ+記号 → バイト値が豊富 → ARM/Thumb両対応
非日本語版: 英数字+一部記号 → バイト値が少ない → ほぼARMモードのみ

命令サイズ対応:
- ARM (4B/命令): 1ボックス名 = 2命令
- Thumb (2B/命令): 1ボックス名 = 4命令

## Hex Writer (16進ライター)

ボックス名を16進文字列として解読し任意バイト列を書き込むバッドエッグ。

- 文字'0'-'9','A'-'F' = 1ニブル(4bit)
- 2文字 = 1バイト → 8文字/box = 4バイト/box → 14box = 56バイト/実行
- スペース = バイトスキップ
- 使用ARM命令: STR r12, [r11, lr, LSR #25]!
- 書き込み先: r12レジスタ(>=0x02000000)

## Box14 Exit Code

終了処理をBox14名に移動し、Box1-13をペイロードに開放。

英語版Box14名: `U . o _ _ , o a`
必要壁紙: Box1=STARS(ほし), Box2=DESERT(さばく)

## 3層ペイロードアーキテクチャ

1. Exit Code Bootstrap (Box1-13): ペイロードチェーン有効化
2. Hex Writer (6連続boxコード): メモリにraw hex書き込み
3. Crafting Table (Box13 Slot11): 中間アセンブリ領域
4. ScriptMover (Box14 Slot15): Crafting Table → RamScript(0x02039A38)にコピー (BIOS CpuFastSet)
5. RamScript Writer (Box14 Slot16): r12をRamScriptアドレスに設定

ScriptMoverアセンブリ:
```
06F04FE2  SUB PC, PC, #6      ; アライメント
A60E4FE2  SUB R0, PC, #0xA60  ; ソース=Crafting Table
1C109FE5  LDR R1, [address]   ; 宛先=0x02039A38
00000CEF  SWI 0xC0000         ; CpuFastSet
```
