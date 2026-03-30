# glitch_species_calc: グリッチ種族生成の計算方法

**※ 本ファイルのアセンブリ・アドレス定数はGBA版ベースです。Switch版ではメモリアドレス(手持ちスロット等)がシフトしているため、アセンブリ内のアドレス定数はそのまま適用できません。ただし以下はGBA/Switch共通であることがSwitch版LGで実機検証済み:**
- **計算式(暗号化キー、チェックサム、Species変換)**
- **文字エンコーディング表**
- **任意種族生成方法(Box4-5のデータテーブル書き換え) — 0x4F90およびアチャモ(0x0118)の生成に成功(2026-03)**

**前提条件: 手持ちは2匹以下(書き込み先のスロット3が空)であること。既存データがあるとチェックサム不整合でダメタマゴになる。**

## Gen3ポケモンデータ構造

### 暗号化キー
```
E = (TID | (SID << 16)) XOR PID
E_low  = TID XOR (PID & 0xFFFF)  → 奇数番目16bitワードの暗号化に使用
E_high = SID XOR (PID >> 16)     → 偶数番目16bitワードの暗号化に使用
```

### サブストラクチャ並び順 (PID mod 24)

| PID%24 | 順序 | PID%24 | 順序 | PID%24 | 順序 | PID%24 | 順序 |
|--------|------|--------|------|--------|------|--------|------|
| 0 | GAEM | 6 | AGEM | 12 | EGAM | 18 | MGAE |
| 1 | GAME | 7 | AGME | 13 | EGMA | 19 | MGEA |
| 2 | GEAM | 8 | AEGM | 14 | EAGM | 20 | MAGE |
| 3 | GEMA | 9 | AEMG | 15 | EAMG | 21 | MAEG |
| 4 | GMAE | 10 | AMGE | 16 | EMGA | 22 | MEGA |
| 5 | GMEA | 11 | AMEG | 17 | EMAG | 23 | MEAG |

G=Growth, A=Attacks, E=EVs/Condition, M=Miscellaneous

### Growthサブストラクチャ

| オフセット | サイズ | フィールド |
|-----------|--------|-----------|
| 0x00 | 2B | Species (種族番号) |
| 0x02 | 2B | Held Item |
| 0x04 | 4B | Experience |
| 0x08 | 1B | PP Bonuses |
| 0x09 | 1B | Friendship |
| 0x0A | 2B | Unused |

## ニドくんの固定パラメータ

- PID = 0x4C970B9E
- TID = 63184 (0xF6D0)
- SID = 不明 (ただしSpecies書き換えには不要)
- E_low = 0xF6D0 XOR 0x0B9E = **0xFD4E**
- PID mod 24 = 22 → サブストラクチャ順序 = **MEGA**
- Growth = 3rd sub (E_lowで暗号化される位置 → SID不要)

## 日本語版メールバグの仕組み

### メールスロット255のマッピング

日本語版ではメールスロット255がBox3 Slot1の**オフセット0x28以降**を上書きする。

| ワード# | Boxオフセット | サブストラクチャ | サブオフセット |
|---------|-------------|----------------|--------------|
| 1 | 0x28 | 1st sub (M) | 0x08 |
| 2 | 0x2A | 1st sub (M) | 0x0A |
| 3 | 0x2C | 2nd sub (E) | 0x00 |
| 4 | 0x2E | 2nd sub (E) | 0x02 |
| 5 | 0x30 | 2nd sub (E) | 0x04 |
| 6 | 0x32 | 2nd sub (E) | 0x06 |
| 7 | 0x34 | 2nd sub (E) | 0x08 |
| 8 | 0x36 | 2nd sub (E) | 0x0A |
| **9** | **0x38** | **3rd sub (G)** | **0x00 = Species** |

→ **メールの9番目のワードがSpeciesフィールドに対応**

### メールワードの計算

暗号化状態のSpeciesを書き換えるため:
```
メールワード = 目標Species XOR E_low
```

ニドくんの場合 E_low = 0xFD4E なので:
```
メールワード = 目標Species XOR 0xFD4E
```
※ このワードIDがかんたん会話リストに存在する必要あり

### チェックサム補正

Speciesだけ書き換えるとチェックサム不整合でバッドエッグになるため、経験値で吸収:
```
checksum_diff = 新Species - 旧Species(ニドラン♂=0x0020)
```
経験値493はこの補正値として計算された結果。

## 0xFFC9生成: Box名コードによるACE方式 (システムA: 直接ARM実行)

**※ これはシステムA(直接ARM実行、Box1-5)である。汎用コード環境(システムB、Box1+Box11-13+コードポケモン)とは完全に別物。詳細は payloads.md 冒頭の比較表を参照。**

天元(中間グリッチ)をgrab/swapでACE発動後、Box1〜5のボックス名がARM命令として実行される。

### 実行されるアセンブリ
```arm
.thumb
4778        BX      pc              ; Thumb→ARMモード切替
E3B0        (filler)
.arm
E28F0008    ADD     r0, pc, #0x8    ; r0 = データテーブルアドレス
E8B000FF    LDMIA   r0!, {r0-r7}   ; データテーブルからレジスタにロード
E8A2001F    STMIA   r2!, {r0-r4}   ; r2が指す先に書き込み
E12FFF1E    BX      lr              ; 復帰
```

### データテーブル (r0〜r7にロードされる値)
```
r0 = 0x02010000   ; hasSpecies=true, language=Japanese, isEgg=false
r1 = 0x51FFFFFF   ; filler
r2 = 0x020242BC   ; 手持ちスロット3のアドレス
r3 = 0xFFFFFFC8   ; チェックサム
r4 = 0xFFFFFFC9   ; Species=0xFFC9, Item=0xFFFF
```

STMIA命令でr2(手持ちスロット3)にr0〜r4を書き込み → 種族0xFFC9のポケモンが手持ちに生成される。

## 任意種族番号の生成方法

### 方法: データテーブルのSpeciesとチェックサムを変更

0xFFC9以外の種族を生成するには、Box4〜5の文字(データテーブル部分)を変更する:

```
新r3 = 0xFFFF{新チェックサム}
新r4 = 0xFFFF{新Species}

新チェックサム = 0xFFC8 + (新Species - 0xFFC9)
```

### 計算例: 0x4F90「ょゅゅゅ」を生成する場合

```
新Species = 0x4F90
新チェックサム = 0xFFC8 + (0x4F90 - 0xFFC9) = 0xFFC8 + 0x4FC7 = 0x4F8F

r3 = 0xFFFF4F8F
r4 = 0xFFFF4F90
```

→ これに対応するバイト列をGen3文字エンコーディングで逆引きし、Box4〜5の文字を決定する。

### バイト配置の詳細 (Box4-5とr3/r4の対応)

Box名は9バイト(8文字+0xFF終端)が連続配置される。データテーブル内のr3/r4は:

```
r3 = Box4[5] | Box4[6] | Box4[7(終端)] | Box4[8(終端)]
r4 = Box5[0] | Box5[1] | Box5[2(終端)] | Box5[3(終端)]
(リトルエンディアン: 低位バイトが若いインデックス)
```

Box4[0-4]はr1末尾(Box4[0])とr2(Box4[1-4])に属するため変更不可。
未入力のBox文字位置とBox終端子は0xFFとなるため、上位バイトが0xFFになる値は自然に得られる。

### 0x4F90「ょゅゅゅ」の概要

**ょゅゅゅ** (species 0x4F90) は汎用コード環境から召喚できるグリッチポケモン。以下の特殊能力を持つ:

- **逃がせないダメタマゴの削除**: 通常の操作では逃がせないダメタマゴをボックスから除去できる
- **ポケモンのコピー**: ボックス内のポケモンを複製できる

**召喚方法**: Box4-5のデータテーブルを0x4F90用に書き換え、みみぅむぅの入れ替えを実行する（手持ち2匹以下が前提）。

### 0x4F90「ょゅゅゅ」の具体的なBox名 (実機検証済み: Switch版LG, 2026-03)

GBA版:
```
Box 4: アＢぢいいゼぽ  (元: アＢぢいいＮ → 末尾をＮ→ゼぽに変更)
Box 5: ゾぽ            (元: Ｏ → ゾぽに変更)
```

Switch版:
```
Box 4: ア／ぢいいゼぽ  (元: ア／ぢいいＮ → 末尾をＮ→ゼぽに変更)
Box 5: ゾぽ            (元: Ｏ → ゾぽに変更)
```

Box1〜3(ARM命令部分)は変更なし。

### アチャモ(0x0118)の具体的なBox名 (実機検証済み: Switch版LG, 2026-03)

```
Species = 0x0118 (Gen3内部インデックス、図鑑No.255)
Checksum = 0x0118 - 1 = 0x0117
r3 = リトルエンディアン(0x0117) → 17 01 FF FF → ぬ あ (終端) (終端)
r4 = リトルエンディアン(0x0118) → 18 01 FF FF → ね あ (終端) (終端)
```

Switch版:
```
Box 4: ア／ぢいいぬあ  (末尾をＮ→ぬあに変更)
Box 5: ねあ            (Ｏ→ねあに変更)
```

※ Gen3内部インデックスは図鑑番号と異なる。ホウエンポケモンは0x0115(キモリ)から開始。

### 汎用計算式

```
1. 目標Species = X
2. チェックサム = X - 1
3. r3 = リトルエンディアン(X-1) の下位2バイト → Box4[5-6]の文字を逆引き
4. r4 = リトルエンディアン(X)   の下位2バイト → Box5[0-1]の文字を逆引き
5. 各バイトが入力可能な文字(0x00-0xEE, 0xB7-0xB9/0xEF-0xFE除く)に対応するか確認
6. 0xFFが必要な位置は文字未入力(終端子)で自然に得られる
```

## Gen3文字エンコーディング表 (日本語版)

デテロニー氏ブログより抽出:

```
0x00:空  0x01:あ 0x02:い 0x03:う 0x04:え 0x05:お
0x06:か 0x07:き 0x08:く 0x09:け 0x0A:こ 0x0B:さ
0x0C:し 0x0D:す 0x0E:せ 0x0F:そ 0x10:た 0x11:ち
0x12:つ 0x13:て 0x14:と 0x15:な 0x16:に 0x17:ぬ
0x18:ね 0x19:の 0x1A:は 0x1B:ひ 0x1C:ふ 0x1D:へ
0x1E:ほ 0x1F:ま 0x20:み 0x21:む 0x22:め 0x23:も
0x24:や 0x25:ゆ 0x26:よ 0x27:ら 0x28:り 0x29:る
0x2A:れ 0x2B:ろ 0x2C:わ 0x2D:を 0x2E:ん 0x2F:ぁ
0x30:ぃ 0x31:ぅ 0x32:ぇ 0x33:ぉ 0x34:ゃ 0x35:ゅ
0x36:ょ 0x37:が 0x38:ぎ 0x39:ぐ 0x3A:げ 0x3B:ご
0x3C:ざ 0x3D:じ 0x3E:ず 0x3F:ぜ 0x40:ぞ 0x41:だ
0x42:ぢ 0x43:づ 0x44:で 0x45:ど 0x46:ば 0x47:び
0x48:ぶ 0x49:べ 0x4A:ぼ 0x4B:ぱ 0x4C:ぴ 0x4D:ぷ
0x4E:ぺ 0x4F:ぽ 0x50:っ 0x51:ア 0x52:イ 0x53:ウ
0x54:エ 0x55:オ 0x56:カ 0x57:キ 0x58:ク 0x59:ケ
0x5A:コ 0x5B:サ 0x5C:シ 0x5D:ス 0x5E:セ 0x5F:ソ
0x60:タ 0x61:チ 0x62:ツ 0x63:テ 0x64:ト 0x65:ナ
0x66:ニ 0x67:ヌ 0x68:ネ 0x69:ノ 0x6A:ハ 0x6B:ヒ
0x6C:フ 0x6D:ヘ 0x6E:ホ 0x6F:マ 0x70:ミ 0x71:ム
0x72:メ 0x73:モ 0x74:ヤ 0x75:ユ 0x76:ヨ 0x77:ラ
0x78:リ 0x79:ル 0x7A:レ 0x7B:ロ 0x7C:ワ 0x7D:ヲ
0x7E:ン 0x7F:ァ 0x80:ィ 0x81:ゥ 0x82:ェ 0x83:ォ
0x84:ャ 0x85:ュ 0x86:ョ 0x87:ガ 0x88:ギ 0x89:グ
0x8A:ゲ 0x8B:ゴ 0x8C:ザ 0x8D:ジ 0x8E:ズ 0x8F:ゼ
0x90:ゾ 0x91:ダ 0x92:ヂ 0x93:ヅ 0x94:デ 0x95:ド
0x96:バ 0x97:ビ 0x98:ブ 0x99:ベ 0x9A:ボ 0x9B:パ
0x9C:ピ 0x9D:プ 0x9E:ペ 0x9F:ポ 0xA0:ッ 0xA1:０
0xA2:１ 0xA3:２ 0xA4:３ 0xA5:４ 0xA6:５ 0xA7:６
0xA8:７ 0xA9:８ 0xAA:９ 0xAB:！ 0xAC:？ 0xAD:。
0xAE:ー 0xAF:・ 0xB0:… 0xB1:『 0xB2:』 0xB3:「
0xB4:」 0xB5:♂ 0xB6:♀ 0xBA:／ 0xBB:Ａ 0xBC:Ｂ
0xBD:Ｃ 0xBE:Ｄ 0xBF:Ｅ 0xC0:Ｆ 0xC1:Ｇ 0xC2:Ｈ
0xC3:Ｉ 0xC4:Ｊ 0xC5:Ｋ 0xC6:Ｌ 0xC7:Ｍ 0xC8:Ｎ
0xC9:Ｏ 0xCA:Ｐ 0xCB:Ｑ 0xCC:Ｒ 0xCD:Ｓ 0xCE:Ｔ
0xCF:Ｕ 0xD0:Ｖ 0xD1:Ｗ 0xD2:Ｘ 0xD3:Ｙ 0xD4:Ｚ
0xD5:ａ 0xD6:ｂ 0xD7:ｃ 0xD8:ｄ 0xD9:ｅ 0xDA:ｆ
0xDB:ｇ 0xDC:ｈ 0xDD:ｉ 0xDE:ｊ 0xDF:ｋ 0xE0:ｌ
0xE1:ｍ 0xE2:ｎ 0xE3:ｏ 0xE4:ｐ 0xE5:ｑ 0xE6:ｒ
0xE7:ｓ 0xE8:ｔ 0xE9:ｕ 0xEA:ｖ 0xEB:ｗ 0xEC:ｘ
0xED:ｙ 0xEE:ｚ
0xFF:終端子(入力不可)
※ 0xB7-0xB9, 0xEF-0xFE は入力不可文字
```

## 参考

- pomeg-letterbombers JPN FRLG ACE Explanation: https://pomeg-letterbombers.github.io/pokemon-ace-notes/jpn-frlg-ace-explanation/
- pomeg-letterbombers ニドくんRoute: https://pomeg-letterbombers.github.io/pokemon-ace-notes/frlg-jpn-nido-route/
- pomeg-letterbombers Main Route: https://pomeg-letterbombers.github.io/pokemon-ace-notes/frlg-jpn-main-route/
- Bulbapedia Pokemon Data Structure Gen3: https://bulbapedia.bulbagarden.net/wiki/Pokémon_data_structure_(Generation_III)
- デテロニー氏ブログ Em汎用コード一覧: http://detelony.blog.fc2.com/blog-entry-20.html
