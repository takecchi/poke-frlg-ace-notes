# FRLG スクリプトコマンド・Special関数・フラグ リファレンス

pokefirered逆コンパイル (pret/pokefirered) より抽出。
ACEでスクリプトバイトコードを直接構築する際の参考資料。

> **ボックス名制約**: 1ボックス = 8バイト（終端0xFF除く）。入力可能範囲は0x00-0xEE（0xB7-0xB9, 0xEF-0xFE は入力不可）。0xFF = 文字列終端。

---

## 1. スクリプトコマンド一覧（ACE実用系）

### バイトエンコーディング凡例

| 表記 | サイズ | 説明 |
|------|--------|------|
| `.byte` | 1バイト | 8bit値 |
| `.2byte` | 2バイト | 16bit値 (リトルエンディアン) |
| `.4byte` | 4バイト | 32bit値 (リトルエンディアン) |

### 1.1 制御フロー

| Opcode | コマンド | バイト列 | 説明 |
|--------|----------|----------|------|
| `0x02` | `end` | `02` | スクリプト終了 |
| `0x03` | `return` | `03` | callから戻る |
| `0x04` | `call` | `04 [addr:4]` | サブルーチン呼び出し（4byte絶対アドレス） |
| `0x05` | `goto` | `05 [addr:4]` | 無条件ジャンプ（4byte絶対アドレス） |
| `0x06` | `goto_if` | `06 [cond:1] [addr:4]` | 条件付きジャンプ |
| `0x08` | `gotostd` | `08 [func:1]` | 標準関数へジャンプ |
| `0x09` | `callstd` | `09 [func:1]` | 標準関数を呼ぶ |
| `0x27` | `waitstate` | `27` | スクリプト実行をブロック（specialの完了待ち等） |

### 1.2 ネイティブ関数呼び出し（最重要）

| Opcode | コマンド | バイト列 | 説明 |
|--------|----------|----------|------|
| `0x23` | `callnative` | `23 [func:4]` | C関数を呼び出し（戻ってくる）**5バイト** |
| `0x24` | `gotonative` | `24 [func:4]` | C関数へジャンプ（TRUEで復帰）**5バイト** |

> **注意**: callnative/gotonativeは4byteアドレスを含むため、ボックス名でのエンコードが困難（0xFF等の制約）。

### 1.3 Special関数呼び出し

| Opcode | コマンド | バイト列 | 説明 |
|--------|----------|----------|------|
| `0x25` | `special` | `25 [index:2]` | specials.incテーブルの関数を呼ぶ **3バイト** |
| `0x26` | `specialvar` | `26 [outVar:2] [index:2]` | special呼び出し＋結果を変数に格納 **5バイト** |

### 1.4 変数操作

| Opcode | コマンド | バイト列 | 説明 |
|--------|----------|----------|------|
| `0x16` | `setvar` | `16 [var:2] [value:2]` | 変数に値を設定 **5バイト** |
| `0x17` | `addvar` | `17 [var:2] [value:2]` | 変数に加算 **5バイト** |
| `0x18` | `subvar` | `18 [var:2] [value:2]` | 変数から減算 **5バイト** |
| `0x19` | `copyvar` | `19 [dst:2] [src:2]` | 変数コピー **5バイト** |
| `0x1A` | `setorcopyvar` | `1A [dst:2] [src:2]` | srcが変数ならコピー、即値ならセット **5バイト** |

### 1.5 フラグ操作

| Opcode | コマンド | バイト列 | 説明 |
|--------|----------|----------|------|
| `0x29` | `setflag` | `29 [flag:2]` | フラグをTRUEに **3バイト** |
| `0x2A` | `clearflag` | `2A [flag:2]` | フラグをFALSEに **3バイト** |
| `0x2B` | `checkflag` | `2B [flag:2]` | フラグを確認 **3バイト** |

### 1.6 アイテム操作

| Opcode | コマンド | バイト列 | 説明 |
|--------|----------|----------|------|
| `0x44` | `additem` | `44 [itemId:2] [quantity:2]` | アイテム追加 **5バイト** |
| `0x45` | `removeitem` | `45 [itemId:2] [quantity:2]` | アイテム削除 **5バイト** |
| `0x46` | `checkitemspace` | `46 [itemId:2] [quantity:2]` | 空き確認 **5バイト** |
| `0x47` | `checkitem` | `47 [itemId:2] [quantity:2]` | 所持確認 **5バイト** |
| `0x49` | `addpcitem` | `49 [itemId:2] [quantity:2]` | PCにアイテム追加 **5バイト** |

### 1.7 ポケモン関連

| Opcode | コマンド | バイト列 | 説明 |
|--------|----------|----------|------|
| `0x79` | `givemon` | `79 [species:2] [level:1] [item:2] [00 00 00 00] [00 00 00 00] [00]` | ポケモンをもらう **12バイト** |
| `0x7A` | `giveegg` | `7A [species:2]` | タマゴをもらう **3バイト** |
| `0x7B` | `setmonmove` | `7B [partyIdx:1] [slot:1] [move:2]` | 技を変更 **5バイト** |
| `0x7C` | `checkpartymove` | `7C [move:2]` | 手持ちに技があるか確認 **3バイト** |
| `0xB6` | `setwildbattle` | `B6 [species:2] [level:1] [item:2]` | 野生戦準備 **6バイト** |
| `0xB7` | `dowildbattle` | `B7` | 野生戦開始 **1バイト** (**入力不可: 0xB7**) |

> **givemonの注意**: 12バイトと長いが、末尾の9バイトは全て0x00なのでボックス名では扱いやすい。ただし2ボックス分必要。

> **dowildbattle (0xB7) は入力不可文字**。setwildbattleとセットで使う場合は別の手段が必要。

### 1.8 お金・コイン

| Opcode | コマンド | バイト列 | 説明 |
|--------|----------|----------|------|
| `0x90` | `addmoney` | `90 [amount:4] [disable:1]` | お金追加 **6バイト** |
| `0x91` | `removemoney` | `91 [amount:4] [disable:1]` | お金削除 **6バイト** |
| `0x92` | `checkmoney` | `92 [amount:4] [disable:1]` | 所持金確認 **6バイト** |
| `0xB4` | `addcoins` | `B4 [count:2]` | コイン追加 **3バイト** |
| `0xB5` | `removecoins` | `B5 [count:2]` | コイン削除 **3バイト** |

### 1.9 ワープ（テレポート）

| Opcode | コマンド | バイト列 | 説明 |
|--------|----------|----------|------|
| `0x39` | `warp` | `39 [mapGroup:1] [mapNum:1] [warpId:1] [x:2] [y:2]` | ワープ **8バイト** |
| `0x3A` | `warpsilent` | `3A [mapGroup:1] [mapNum:1] [warpId:1] [x:2] [y:2]` | 無音ワープ **8バイト** |
| `0x3B` | `warpdoor` | `3B [mapGroup:1] [mapNum:1] [warpId:1] [x:2] [y:2]` | ドアワープ **8バイト** |
| `0x3C` | `warphole` | `3C [mapGroup:1] [mapNum:1]` | 穴ワープ **3バイト** |
| `0x3D` | `warpteleport` | `3D [mapGroup:1] [mapNum:1] [warpId:1] [x:2] [y:2]` | テレポートワープ **8バイト** |
| `0x3E` | `setwarp` | `3E [mapGroup:1] [mapNum:1] [warpId:1] [x:2] [y:2]` | ワープ先設定 **8バイト** |
| `0x9F` | `setrespawn` | `9F [healLocation:2]` | リスポーン地点設定 **3バイト** |
| `0xC4` | `setescapewarp` | `C4 [mapGroup:1] [mapNum:1] [warpId:1] [x:2] [y:2]` | あなぬけ先設定 **8バイト** |
| `0xD1` | `warpspinenter` | `D1 [mapGroup:1] [mapNum:1] [warpId:1] [x:2] [y:2]` | 回転ワープ **8バイト** |

> **mapの指定**: `mapGroup` (1byte) + `mapNum` (1byte)。マップ定数は `MAP_GROUP(name) << 8 | MAP_NUM(name)` で構成される。

### 1.10 サウンド

| Opcode | コマンド | バイト列 | 説明 |
|--------|----------|----------|------|
| `0x2F` | `playse` | `2F [song:2]` | SE再生 **3バイト** |
| `0x30` | `waitse` | `30` | SE待ち **1バイト** |
| `0x31` | `playfanfare` | `31 [song:2]` | ファンファーレ再生 **3バイト** |
| `0x32` | `waitfanfare` | `32` | ファンファーレ待ち **1バイト** |
| `0x33` | `playbgm` | `33 [song:2] [save:1]` | BGM再生 **4バイト** |
| `0x36` | `fadenewbgm` | `36 [song:2]` | 新BGMへフェード **3バイト** |
| `0x37` | `fadeoutbgm` | `37 [speed:1]` | BGMフェードアウト **2バイト** |
| `0x38` | `fadeinbgm` | `38 [speed:1]` | BGMフェードイン **2バイト** |
| `0xA1` | `playmoncry` | `A1 [species:2] [mode:2]` | 鳴き声再生 **5バイト** |

### 1.11 画面効果

| Opcode | コマンド | バイト列 | 説明 |
|--------|----------|----------|------|
| `0x97` | `fadescreen` | `97 [mode:1]` | 画面フェード **2バイト** |
| `0x98` | `fadescreenspeed` | `98 [mode:1] [speed:1]` | 速度指定フェード **3バイト** |
| `0x9C` | `dofieldeffect` | `9C [anim:2]` | フィールドエフェクト **3バイト** |
| `0xA4` | `setweather` | `A4 [type:2]` | 天候設定 **3バイト** |
| `0xA5` | `doweather` | `A5` | 天候適用 **1バイト** |

### 1.12 メッセージ・UI

| Opcode | コマンド | バイト列 | 説明 |
|--------|----------|----------|------|
| `0x66` | `waitmessage` | `66` | メッセージ待ち **1バイト** |
| `0x67` | `message` | `67 [text:4]` | メッセージ表示 **5バイト** |
| `0x68` | `closemessage` | `68` | メッセージを閉じる **1バイト** |
| `0x69` | `lockall` | `69` | 全NPCロック **1バイト** |
| `0x6B` | `releaseall` | `6B` | 全NPCリリース **1バイト** |
| `0x6D` | `waitbuttonpress` | `6D` | ボタン入力待ち **1バイト** |
| `0x75` | `showmonpic` | `75 [species:2] [x:1] [y:1]` | ポケモン画像表示 **5バイト** |
| `0x76` | `hidemonpic` | `76` | ポケモン画像非表示 **1バイト** |

### 1.13 その他の便利コマンド

| Opcode | コマンド | バイト列 | 説明 |
|--------|----------|----------|------|
| `0x00` | `nop` | `00` | 何もしない **1バイト** |
| `0x28` | `delay` | `28 [frames:2]` | フレーム待ち **3バイト** |
| `0x43` | `getpartysize` | `43` | 手持ち数取得→VAR_RESULT **1バイト** |
| `0x8F` | `random` | `8F [limit:2]` | 乱数生成 **3バイト** |
| `0xA0` | `checkplayergender` | `A0` | 性別確認 **1バイト** |
| `0xA2` | `setmetatile` | `A2 [x:2] [y:2] [tile:2] [impass:2]` | マップタイル変更 **9バイト** |
| `0xC3` | `incrementgamestat` | `C3 [stat:1]` | ゲーム統計カウントアップ **2バイト** |
| `0xD0` | `setworldmapflag` | `D0 [flag:2]` | ワールドマップフラグ設定 **3バイト** |

### 1.14 比較コマンド

| Opcode | コマンド | バイト列 | 説明 |
|--------|----------|----------|------|
| `0x21` | `compare_var_to_value` | `21 [var:2] [value:2]` | 変数と即値を比較 **5バイト** |
| `0x22` | `compare_var_to_var` | `22 [var1:2] [var2:2]` | 変数同士を比較 **5バイト** |

---

## 2. Special関数インデックス（ACE実用系）

`special` コマンド (opcode `0x25`) で呼び出す。バイト列: `25 [index_lo] [index_hi]`

### 2.1 実用Special一覧（確認済みインデックス）

| Index (dec) | Index (hex) | 関数名 | 説明 | バイト列例 |
|-------------|-------------|--------|------|-----------|
| 0 | 0x0000 | `HealPlayerParty` | 手持ち全回復 | `25 00 00` |
| 60 | 0x003C | `ShowPokemonStorageSystemPC` | ポケモンボックスPC起動 | `25 3C 00` |
| 93 | 0x005D | `Field_AskSaveTheGame` | セーブ画面表示 | `25 5D 00` |
| 131 | 0x0083 | `CalculatePlayerPartyCount` | 手持ち数算出 | `25 83 00` |
| 159 | 0x009F | `ChoosePartyMon` | 手持ち選択画面 | `25 9F 00` |
| 171 | 0x00AB | `RockSmashWildEncounter` | いわくだき野生エンカウント | `25 AB 00` |
| 193 | 0x00C1 | `ScriptHatchMon` | タマゴ孵化 | `25 C1 00` |
| 194 | 0x00C2 | `EggHatch` | タマゴ孵化アニメーション | `25 C2 00` |
| 200 | 0x00C8 | `SetCB2WhiteOut` | ホワイトアウト（全滅処理） | `25 C8 00` |
| 212 | 0x00D4 | `GetPokedexCount` | 図鑑数取得 | `25 D4 00` |
| 236 | 0x00EC | `StartSpecialBattle` | 特殊バトル開始 | `25 EC 00` |
| 251 | 0x00FB | `ShowTownMap` | タウンマップ表示 | `25 FB 00` -- **注: 0xFBは入力不可の可能性あり** |
| 271 | 0x010F | `DoSoftReset` | ソフトリセット | `25 0F 01` |
| **272** | **0x0110** | **`EnterHallOfFame`** | **殿堂入り** | **`25 10 01`** |
| 273 | 0x0111 | `AnimateElevator` | エレベーターアニメ | `25 11 01` |
| 297 | 0x0129 | `InitRoamer` | 徘徊ポケモン初期化 | `25 29 01` |
| 312 | 0x0138 | `StartLegendaryBattle` | 伝説バトル開始 | `25 38 01` |
| 319 | 0x013F | `DoFallWarp` | 落下ワープ | `25 3F 01` |
| 331 | 0x014B | `LoadPlayerBag` | バッグ画面表示 | `25 4B 01` |
| 335 | 0x014F | `HasAllKantoMons` | カントー図鑑完成確認 | `25 4F 01` |
| 341 | 0x0155 | `SetPostgameFlags` | クリア後フラグ設定（1回目） | `25 55 01` |
| 343 | 0x0157 | `ForcePlayerOntoBike` | 強制自転車乗車 | `25 57 01` |
| 353 | 0x0161 | `ForcePlayerToStartSurfing` | 強制なみのり開始 | `25 61 01` |
| 354 | 0x0162 | `GetStarterSpecies` | 御三家種族取得 | `25 62 01` |
| 355 | 0x0163 | `SetSeenMon` | 図鑑「見た」登録 | `25 63 01` |
| **367** | **0x016F** | **`EnableNationalPokedex`** | **全国図鑑有効化** | **`25 6F 01`** |
| 385 | 0x0181 | `SetUnlockedPokedexFlags` | 図鑑アンロックフラグ設定 | `25 81 01` |
| 403 | 0x0193 | `IsNationalPokedexEnabled` | 全国図鑑有効か確認 | `25 93 01` |
| 410 | 0x019A | `SetPostgameFlags` | クリア後フラグ設定（2回目） | `25 9A 01` |
| 421 | 0x01A5 | `DoCredits` | エンドクレジット再生 | `25 A5 01` |
| 427 | 0x01AB | `DoDeoxysTriangleInteraction` | デオキシス三角パズル | `25 AB 01` |
| 432 | 0x01B0 | `HasAllMons` | 全ポケモン所持確認 | `25 B0 01` |

### 2.2 ACEで特に有用なSpecial

#### 手持ち全回復 (最小3バイト)
```
25 00 00    special HealPlayerParty
02          end
```
合計4バイト。1ボックスに余裕で収まる。

#### 殿堂入り (最小3バイト + waitstate)
```
25 10 01    special EnterHallOfFame
27          waitstate
02          end
```
合計5バイト。1ボックスに収まる。

#### 全国図鑑有効化 (最小3バイト)
```
25 6F 01    special EnableNationalPokedex
02          end
```
合計4バイト。1ボックスに収まる。

#### クリア後フラグ一括設定
```
25 55 01    special SetPostgameFlags
02          end
```
合計4バイト。

### 2.3 その他の全Specialインデックス（主要なもの）

| Index | Hex | 関数名 |
|-------|-----|--------|
| 1 | 0x01 | SetCableClubWarp |
| 59 | 0x3B | ShowPokemonStorageSystemPC の前後 |
| 92 | 0x5C | Field_AskSaveTheGame |
| 130 | 0x82 | CalculatePlayerPartyCount |
| 157 | 0x9D | ChangePokemonNickname |
| 180 | 0xB4 | GetBattleOutcome |
| 196 | 0xC4 | ShowBattleRecords |
| 204 | 0xCC | EnterSafariMode |
| 205 | 0xCD | ExitSafariMode |
| 218 | 0xDA | ChooseMonForMoveRelearner |
| 219 | 0xDB | SelectMoveDeleterMove |
| 223 | 0xDF | TeachMoveRelearnerMove |
| 229 | 0xE5 | GetLeadMonFriendship |
| 275 | 0x113 | SpawnCameraObject |
| 298 | 0x12A | PlayerHasGrassPokemonInParty |
| 303 | 0x12F | IsThereRoomInAnyBoxForMorePokemon |

---

## 3. 重要フラグ一覧

`setflag` (0x29) / `clearflag` (0x2A) で使用。バイト列: `29 [flag_lo] [flag_hi]`

### 3.1 バッジフラグ (0x820-0x827)

| フラグ値 | 名前 | バイト列 (setflag) |
|----------|------|-------------------|
| 0x0820 | FLAG_BADGE01_GET (グレー) | `29 20 08` |
| 0x0821 | FLAG_BADGE02_GET (ハナダ) | `29 21 08` |
| 0x0822 | FLAG_BADGE03_GET (クチバ) | `29 22 08` |
| 0x0823 | FLAG_BADGE04_GET (タマムシ) | `29 23 08` |
| 0x0824 | FLAG_BADGE05_GET (セキチク) | `29 24 08` |
| 0x0825 | FLAG_BADGE06_GET (ヤマブキ) | `29 25 08` |
| 0x0826 | FLAG_BADGE07_GET (グレン) | `29 26 08` |
| 0x0827 | FLAG_BADGE08_GET (トキワ) | `29 27 08` |

### 3.2 システムフラグ

| フラグ値 | 名前 | 説明 | バイト列 (setflag) |
|----------|------|------|-------------------|
| 0x0828 | FLAG_SYS_POKEMON_GET | ポケモンを入手した | `29 28 08` |
| 0x0829 | FLAG_SYS_POKEDEX_GET | 図鑑を入手した | `29 29 08` |
| 0x082C | FLAG_SYS_GAME_CLEAR | ゲームクリア済み | `29 2C 08` |
| 0x082F | FLAG_SYS_B_DASH | Bダッシュ有効 | `29 2F 08` |
| 0x0839 | FLAG_SYS_MYSTERY_GIFT_ENABLED | ふしぎなおくりもの有効 | `29 39 08` |
| 0x0840 | FLAG_SYS_NATIONAL_DEX | 全国図鑑有効 | `29 40 08` |
| 0x0845 | FLAG_SYS_SEVII_MAP_123 | ナナシマ1-3解放 | `29 45 08` |
| 0x0846 | FLAG_SYS_SEVII_MAP_4567 | ナナシマ4-7解放 | `29 46 08` |
| 0x0848 | FLAG_SYS_DEOXYS_AWAKENED | デオキシス覚醒 | `29 48 08` |
| 0x0849 | FLAG_SYS_UNLOCKED_TANOBY_RUINS | アスカナ遺跡解放 | `29 49 08` |

### 3.3 一時システムフラグ (0x800-0x808)

| フラグ値 | 名前 | 説明 |
|----------|------|------|
| 0x0800 | FLAG_SYS_SAFARI_MODE | サファリモード中 |
| 0x0801 | FLAG_SYS_VS_SEEKER_CHARGING | バトルサーチャー充電中 |
| 0x0802 | FLAG_SYS_CRUISE_MODE | サントアンヌ号モード |
| 0x0805 | FLAG_SYS_USE_STRENGTH | かいりき使用中 |
| 0x0806 | FLAG_SYS_FLASH_ACTIVE | フラッシュ使用中 |

### 3.4 伝説ポケモン戦闘フラグ

| フラグ値 | 名前 | 説明 |
|----------|------|------|
| 0x02BC | FLAG_FOUGHT_MEWTWO | ミュウツー戦闘済み |
| 0x02BD | FLAG_FOUGHT_MOLTRES | ファイヤー戦闘済み |
| 0x02BE | FLAG_FOUGHT_ARTICUNO | フリーザー戦闘済み |
| 0x02BF | FLAG_FOUGHT_ZAPDOS | サンダー戦闘済み |
| 0x02E4 | FLAG_FOUGHT_DEOXYS | デオキシス戦闘済み |
| 0x02F2 | FLAG_FOUGHT_LUGIA | ルギア戦闘済み |
| 0x02F3 | FLAG_FOUGHT_HO_OH | ホウオウ戦闘済み |

> **伝説再戦**: `clearflag` で戦闘済みフラグをクリアすると、伝説ポケモンと再戦可能になる。
> 例: ミュウツー再戦 = `2A BC 02` (clearflag 0x02BC)

### 3.5 ジムリーダー撃破フラグ (0x4B0-0x4BC)

| フラグ値 | 名前 |
|----------|------|
| 0x04B0 | FLAG_DEFEATED_BROCK |
| 0x04B1 | FLAG_DEFEATED_MISTY |
| 0x04B2 | FLAG_DEFEATED_LT_SURGE |
| 0x04B3 | FLAG_DEFEATED_ERIKA |
| 0x04B4 | FLAG_DEFEATED_KOGA |
| 0x04B5 | FLAG_DEFEATED_SABRINA |
| 0x04B6 | FLAG_DEFEATED_BLAINE |
| 0x04B7 | FLAG_DEFEATED_LEADER_GIOVANNI |
| 0x04B8 | FLAG_DEFEATED_LORELEI |
| 0x04B9 | FLAG_DEFEATED_BRUNO |
| 0x04BA | FLAG_DEFEATED_AGATHA |
| 0x04BB | FLAG_DEFEATED_LANCE |
| 0x04BC | FLAG_DEFEATED_CHAMP |

### 3.6 重要アイテム取得フラグ

| フラグ値 | 名前 |
|----------|------|
| 0x0237 | FLAG_GOT_HM01 (いあいぎり) |
| 0x0238 | FLAG_GOT_HM02 (そらをとぶ) |
| 0x0239 | FLAG_GOT_HM03 (なみのり) |
| 0x023A | FLAG_GOT_HM04 (かいりき) |
| 0x023B | FLAG_GOT_HM05 (フラッシュ) |
| 0x02EF | FLAG_GOT_HM06 (いわくだき) |
| 0x0234 | FLAG_GOT_SS_TICKET |
| 0x02A6 | FLAG_GOT_TEA |
| 0x02A7 | FLAG_RECEIVED_AURORA_TICKET |
| 0x02A8 | FLAG_RECEIVED_MYSTIC_TICKET |
| 0x02A9 | FLAG_RECEIVED_OLD_SEA_MAP |
| 0x02F4 | FLAG_OAK_SAW_DEX_COMPLETION |

### 3.7 テンポラリフラグ (0x00-0x1F)

マップ切り替えごとにクリアされる。NPC会話制御や一時的な障害物に使用。
`FLAG_TEMP_1` (0x01) ~ `FLAG_TEMP_1F` (0x1F)

---

## 4. ACE ボックス名エンコーディング実例

### 4.1 手持ち全回復
```
Box 1: 25 00 00 02 xx xx xx xx
        special HealPlayerParty / end
```
(xx = 0x00 パディングまたは他コマンド)

### 4.2 殿堂入り
```
Box 1: 25 10 01 27 02 xx xx xx
        special EnterHallOfFame / waitstate / end
```

### 4.3 全国図鑑有効化
```
Box 1: 25 6F 01 02 xx xx xx xx
        special EnableNationalPokedex / end
```

### 4.4 全バッジ取得 (8個)
```
Box 1: 29 20 08 29 21 08 29 22
        setflag BADGE01 / setflag BADGE02 / setflag BADGE03 (途中)
Box 2: 08 29 23 08 29 24 08 xx
        (BADGE03完) / setflag BADGE04 / setflag BADGE05 (途中)
Box 3: 29 25 08 29 26 08 29 27
        setflag BADGE06 / setflag BADGE07 / setflag BADGE08 (途中)
Box 4: 08 02 xx xx xx xx xx xx
        (BADGE08完) / end
```
合計25バイト = 4ボックス必要

### 4.5 マスターボール99個 (実機検証済み: Switch版LG, 2026-03)
```
Box 1: であ空テ空い
        44 01 00 63 00 02
        additem ITEM_MASTER_BALL(0x01) qty=99(0x63) / end
```
で=0x44(additem), あ=0x01, 空=0x00, テ=0x63(=99), 空=0x00, い=0x02(end)
※ quantity省略(`であ空い`=4バイト)だと不正な数量になる。必ず6バイト全て指定すること。

### 4.6 ゲームクリアフラグ設定
```
Box 1: 29 2C 08 02 xx xx xx xx
        setflag FLAG_SYS_GAME_CLEAR / end
```

### 4.7 伝説再戦（ミュウツー）
```
Box 1: 2A BC 02 02 xx xx xx xx
        clearflag FLAG_FOUGHT_MEWTWO / end
```

### 4.8 お金MAX (999999 = 0x000F423F)
```
Box 1: 90 3F 42 0F 00 00 02 xx
        addmoney 999999 disable=0 / end
```

---

## 5. 入力制約に関する注意

### 5.1 入力不可バイト
- `0xB7` (dowildbattle) - 野生戦開始が直接入力できない
- `0xB8` (setvaddress) - 入力不可
- `0xB9` (vgoto) - 入力不可
- `0xEF`-`0xFE` - 入力不可範囲
- `0xFF` - 文字列終端（ボックス名の終わり）

### 5.2 ボックス名での多バイト値の注意
- 2byte/4byte値はリトルエンディアン
- フラグ `0x0820` = バイト列 `20 08` (低位バイトが先)
- species/item IDも同様にリトルエンディアン
- 値に0xFF, 0xB7-0xB9, 0xEF-0xFEが含まれる場合は直接入力不可

### 5.3 0x00 (nop) の活用
- `0x00` = nop（何もしない）なので、ボックス名の空きバイトは0x00で埋めても安全

---

## 6. スクリプトコマンド全一覧 (0x00-0xD4)

簡易リスト。パラメータ詳細は上記セクション参照。

| Opcode | コマンド | サイズ |
|--------|----------|--------|
| 0x00 | nop | 1 |
| 0x01 | nop1 | 1 |
| 0x02 | end | 1 |
| 0x03 | return | 1 |
| 0x04 | call | 5 |
| 0x05 | goto | 5 |
| 0x06 | goto_if | 6 |
| 0x07 | call_if | 6 |
| 0x08 | gotostd | 2 |
| 0x09 | callstd | 2 |
| 0x0A | gotostd_if | 3 |
| 0x0B | callstd_if | 3 |
| 0x0C | returnram | 1 |
| 0x0D | endram | 1 |
| 0x0E | setmysteryeventstatus | 2 |
| 0x0F | loadword | 6 |
| 0x10 | loadbyte | 3 |
| 0x11 | setptr | 6 |
| 0x12 | loadbytefromptr | 6 |
| 0x13 | setptrbyte | 6 |
| 0x14 | copylocal | 3 |
| 0x15 | copybyte | 9 |
| 0x16 | setvar | 5 |
| 0x17 | addvar | 5 |
| 0x18 | subvar | 5 |
| 0x19 | copyvar | 5 |
| 0x1A | setorcopyvar | 5 |
| 0x1B | compare_local_to_local | 3 |
| 0x1C | compare_local_to_value | 4 |
| 0x1D | compare_local_to_ptr | 6 |
| 0x1E | compare_ptr_to_local | 6 |
| 0x1F | compare_ptr_to_value | 8 |
| 0x20 | compare_ptr_to_ptr | 9 |
| 0x21 | compare_var_to_value | 5 |
| 0x22 | compare_var_to_var | 5 |
| 0x23 | callnative | 5 |
| 0x24 | gotonative | 5 |
| 0x25 | special | 3 |
| 0x26 | specialvar | 5 |
| 0x27 | waitstate | 1 |
| 0x28 | delay | 3 |
| 0x29 | setflag | 3 |
| 0x2A | clearflag | 3 |
| 0x2B | checkflag | 3 |
| 0x2C | initclock | 5 |
| 0x2D | dotimebasedevents | 1 |
| 0x2E | gettime | 1 |
| 0x2F | playse | 3 |
| 0x30 | waitse | 1 |
| 0x31 | playfanfare | 3 |
| 0x32 | waitfanfare | 1 |
| 0x33 | playbgm | 4 |
| 0x34 | savebgm | 3 |
| 0x35 | fadedefaultbgm | 1 |
| 0x36 | fadenewbgm | 3 |
| 0x37 | fadeoutbgm | 2 |
| 0x38 | fadeinbgm | 2 |
| 0x39 | warp | 8 |
| 0x3A | warpsilent | 8 |
| 0x3B | warpdoor | 8 |
| 0x3C | warphole | 3 |
| 0x3D | warpteleport | 8 |
| 0x3E | setwarp | 8 |
| 0x3F | setdynamicwarp | 8 |
| 0x40 | setdivewarp | 8 |
| 0x41 | setholewarp | 8 |
| 0x42 | getplayerxy | 5 |
| 0x43 | getpartysize | 1 |
| 0x44 | additem | 5 |
| 0x45 | removeitem | 5 |
| 0x46 | checkitemspace | 5 |
| 0x47 | checkitem | 5 |
| 0x48 | checkitemtype | 3 |
| 0x49 | addpcitem | 5 |
| 0x4A | checkpcitem | 5 |
| 0x4B-0x4E | decoration cmds | varies |
| 0x4F-0x52 | applymovement/waitmovement | varies |
| 0x53-0x56 | removeobject/addobject | varies |
| 0x57 | setobjectxy | 6 |
| 0x58-0x59 | showobjectat/hideobjectat | varies |
| 0x5A | faceplayer | 1 |
| 0x5B | turnobject | 3 |
| 0x5C | trainerbattle | varies |
| 0x5D | dotrainerbattle | 1 |
| 0x60-0x62 | trainer flag cmds | 3 |
| 0x63-0x65 | object position cmds | varies |
| 0x66 | waitmessage | 1 |
| 0x67 | message | 5 |
| 0x68 | closemessage | 1 |
| 0x69 | lockall | 1 |
| 0x6A | lock | 1 |
| 0x6B | releaseall | 1 |
| 0x6C | release | 1 |
| 0x6D | waitbuttonpress | 1 |
| 0x6E | yesnobox | 3 |
| 0x6F-0x71 | multichoice variants | varies |
| 0x75 | showmonpic | 5 |
| 0x76 | hidemonpic | 1 |
| 0x79 | givemon | 12 |
| 0x7A | giveegg | 3 |
| 0x7B | setmonmove | 5 |
| 0x7C | checkpartymove | 3 |
| 0x7D-0x85 | buffer cmds | varies |
| 0x86 | pokemart | 5 |
| 0x8F | random | 3 |
| 0x90 | addmoney | 6 |
| 0x91 | removemoney | 6 |
| 0x92 | checkmoney | 6 |
| 0x93 | showmoneybox | 4 |
| 0x94 | hidemoneybox | 1 |
| 0x97 | fadescreen | 2 |
| 0x98 | fadescreenspeed | 3 |
| 0x9F | setrespawn | 3 |
| 0xA0 | checkplayergender | 1 |
| 0xA1 | playmoncry | 5 |
| 0xA2 | setmetatile | 9 |
| 0xA4 | setweather | 3 |
| 0xA5 | doweather | 1 |
| 0xB3 | checkcoins | 3 |
| 0xB4 | addcoins | 3 |
| 0xB5 | removecoins | 3 |
| 0xB6 | setwildbattle | 6 |
| 0xB7 | dowildbattle | 1 |
| 0xC0 | showcoinsbox | 5 |
| 0xC3 | incrementgamestat | 2 |
| 0xC4 | setescapewarp | 8 |
| 0xD0 | setworldmapflag | 3 |
| 0xD1 | warpspinenter | 8 |
| 0xD4 | bufferitemnameplural | 5 |

---

## 7. 参考情報

- **ソース**: [pret/pokefirered](https://github.com/pret/pokefirered) (master branch)
- **ファイル**:
  - `asm/macros/event.inc` - スクリプトコマンドマクロ定義
  - `asm/macros/map.inc` - マップマクロ (`map` = group:1byte + num:1byte)
  - `data/specials.inc` - Special関数テーブル (全444エントリ、0-443)
  - `include/constants/flags.h` - フラグ定義 (全0x900 = 2304個)
  - `src/scrcmd.c` - スクリプトコマンドハンドラ実装
- **FLAGS_COUNT**: 0x900 (2304)
- **Specials総数**: 444 (インデックス 0-443)
