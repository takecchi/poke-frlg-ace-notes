# arm7tdmi: ARM7TDMI命令セットとデータ構造

## アーキテクチャ概要

- ARMv4T命令セット
- ARMモード(32bit命令) / Thumbモード(16bit命令)
- モード切替: BX命令 (アドレスbit0: 0=ARM, 1=Thumb)
- EWRAMからの実行はどちらも可

## ACEペイロード頻出命令

```
SUB PC, PC, #offset       ; PCアライメント(位置非依存)
LDR Rn, [PC, #offset]    ; 命令ストリームから定数ロード
SWI 0xC0000               ; BIOS CpuFastSet(一括コピー)
SWI 0xB0000               ; BIOS CpuSet
BX lr                     ; サブルーチン復帰
BX r0                     ; r0アドレスへ分岐
STMDB SP!, {regs}         ; レジスタpush
LDMIA SP!, {regs}         ; レジスタpop
STR rd, [rn, rm, LSR #n]! ; シフトオフセット付きストア+ライトバック
```

## バイト破損問題

ポケモンデータのoffset 20, 76 (10進)は通常操作で破損しうる。
安全なニブル値: 4, 5, 6, 7, C, D, E, F

## ポケモンデータ暗号化

暗号化キー: E = (TrainerID + SecretID × 65536) XOR PersonalityValue
種族暗号化は下位16bitのみ使用。

サブストラクチャ順序: PersonalityValue mod 24 で決定 (24通り)
→ Growth, Attacks, EVs, Condition の並び替え

## PRNG (疑似乱数生成)

線形合同法: seed_next = seed × 0x41C64E6D + 0x00006073

| 用途 | GBA版アドレス | Switch版アドレス |
|------|-------------|----------------|
| シード格納先 | 0x03005000 | **不明** |
