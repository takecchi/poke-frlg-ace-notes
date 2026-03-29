# FRLG ACE Knowledge Base

このディレクトリはポケットモンスター ファイアレッド・リーフグリーン（FRLG）の任意コード実行（ACE）に関する知識ベースである。

## Claudeへの指示

- ACEに関する質問や作業を求められた場合、`knowledge/` 配下のファイルを参照せよ
- アドレス情報は必ず「GBA版」と「Switch版」を区別して回答せよ。Switch版が不明の場合はその旨を明示すること
- ユーザーが新しい情報を提供した場合、該当する `knowledge/` ファイルを更新せよ
- Switch版のアドレスが判明した場合、`**不明**` を実際の値に置き換えよ

## 知識ファイル一覧

| ファイル | 内容 |
|---------|------|
| `knowledge/memory_map.md` | GBAメモリマップ、IWRAM/EWRAMアドレス、gPokemonStorage構造体 |
| `knowledge/ace_methods.md` | ACE発動方法（メールバグ、つかむ/いれかえACE、HOCKルート） |
| `knowledge/box_name_coding.md` | ボックス名コーディング、文字制約、Hex Writer、ペイロードアーキテクチャ |
| `knowledge/arm7tdmi.md` | ARM/Thumb命令セット、暗号化、PRNG |
| `knowledge/platform_diff.md` | GBA版とSwitch版の差異 |
| `knowledge/payloads.md` | 具体的なACEペイロード実例 |
| `knowledge/glitch_species_calc.md` | グリッチ種族生成の計算方法、文字エンコーディング表 |
| `knowledge/references.md` | 外部参考リンク集 |
| `knowledge/script_commands.md` | スクリプトコマンドopcode、Special関数インデックス、フラグ定義 |
| `knowledge/item_ids.md` | アイテムID一覧（10進・16進）、ボール・HM・TM・きのみ・どうぐ全375種 |
| `knowledge/game_constants.md` | 技ID全355種、マップID（グループ:番号形式）全マップ、ヒールロケーションID（setrespawn用） |
| `knowledge/species_ids.md` | ポケモン内部種族番号一覧（全411種+アンノーン）、入力不可バイト該当種族 |
| `knowledge/script_authoring.md` | スクリプト作成手順書（コマンド選択→バイト組立→文字変換→Box名設定） |
