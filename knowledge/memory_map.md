# memory_map: GBAメモリマップとFRLG固有アドレス

## GBAメモリ領域

- IWRAM: 0x03000000-0x03007FFF (32KB, 32bit幅, 最速)
- EWRAM: 0x02000000-0x0203FFFF (256KB, 16bit幅, 0x40000ごとにミラー)
- ROM: 0x08000000+ (読み取り専用)

## FRLG IWRAMアドレス

| 用途 | GBA版 | Switch版 |
|------|-------|----------|
| イベントスクリプト実行判定ポインタ | **不明** | 0x03000FA8 (デテロニー氏) |
| PRNGシード | 0x03005000 | **不明** |
| セーブブロックポインタ(マップ) | 0x03005008 | **不明** |
| セーブブロックポインタ(トレーナー) | 0x0300500C | **不明** |
| セーブブロックポインタ(ボックス/gPokemonStorage) | 0x03005010 | **不明** |

## FRLG EWRAMアドレス

| 用途 | GBA版 | Switch版 |
|------|-------|----------|
| 手持ちポケモンスロット1 (各100B×6匹) | 0x02024284 | **不明** |
| RamScript (ScriptMover書き込み先) | 0x02039A38 | **不明** |
| ストレージベース (early ROM) | 0x03004FA0 (+0xA0 offset) | **不明** |

## ASLR

FRLGには簡易ASLRがあり、メモリブロックがベースから0〜124バイトシフトする。建物退出・メニュー閉じでDMAポインタ(0x03005008/0C/10)が変化。ボックスデータはIWRAMポインタ経由で参照が必要。

## gPokemonStorage構造体

```c
struct PokemonStorage {
    /*0x0000*/ u8 currentBox;                  // 1B
    /*0x0001*/ struct BoxPokemon boxes[14][30]; // 14box × 30slot × 80B = 33600B
    /*0x8344*/ u8 boxNames[14][9];             // 14box × 9B (8char + 0xFF終端) = 126B ← ペイロード領域
    /*0x83C2*/ u8 boxWallpapers[14];           // 14B
};
```

重要オフセット: ボックス名=0x8344, 壁紙=0x83C2
