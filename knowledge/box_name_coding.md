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
  - lr(ROM起点=0x08xxxxxx)を25bit右シフト → オフセット0x04を得る
  - r11+4にr12を書き込み、r11を+4(ライトバック)
- 書き込み先: r12レジスタ(>=0x02000000)
- デフォルトではBox14 Slot28の先頭56バイトに書き込む
- r12を変更すれば任意アドレスに書き込み可能

### Hex Writer Bad Egg のバイナリ (64バイト)

```
8A 80 8F E2 00 0E B8 E8
02 04 5C E3 66 C0 4F 32
09 10 D8 E7 B1 10 51 E2
10 10 91 32 0B B2 81 50
00 B0 9C 45 01 00 1A E3
01 B0 CC 14 00 B0 A0 13
07 00 5A E3 01 A0 8A 32
00 A0 A0 23 01 90 89 22
01 90 89 E2 7E 00 59 E3
40 F0 4F 42 10 FF 2F E1
```

### Hex Writer の作成方法 (非日本語版)

1. Box3 Slot1を空にする
2. メール破損でOmanyte+Snorlaxの組み合わせを使い、Bad Eggを生成 → Box10 Slot2に配置
3. 6回のBox名コード実行でBad Eggのデータを書き換え → Hex Writer完成
4. 完成後Box14 Slot29に配置

### Hex Writer の作成方法 (日本語版)

**未確立。** 非日本語版のメール破損ワード(OMANYTE, SNORLAX等)は日本語版のかんたん会話リストと異なるため、
メールワードの日本語版対応を個別に計算する必要がある。
また、Box名コード(6回分)もGen3日本語文字エンコーディングで再計算が必要。

### Switch版での注意事項

- SwitchエミュレータはARMv5で動作。**STRH/STRB命令が誤アドレスに書き込む**問題あり
- Hex WriterはSTR(ワード書き込み)を使用するため、この問題の影響は要検証
- Box4/8/12の末尾3文字にスペースを入れると問題が起きる → 空にしてBox名を早期確定すること
- Exit Codeの微調整が必要（後述）

## Box14 Exit Code

終了処理をBox14名に移動し、Box1-13をペイロードに開放。

英語版Box14名: `U . o _ _ , o a`
必要壁紙: Box1=STARS(ほし), Box2=DESERT(さばく)

Switch版対応: GBA BIOSが内蔵されているためBIOS関連の回避策は不要。
ただしExit Codeのbox名に以下の調整が必要:
- Box11: `o _ _ _ _ _ _` → `. o` に変更（ARM命令がSwitchエミュレータでクラッシュ回避）
- 代替Exit Code: Box10を`_ F o H I o o r`、Box11を`x n` に変更

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
