# FRLG ACE Knowledge Base

このディレクトリはポケットモンスター ファイアレッド・リーフグリーン（FRLG）の任意コード実行（ACE）に関する知識ベースである。

## Claudeへの指示

- ACEに関する質問や作業を求められた場合、`knowledge/` 配下のファイルを参照せよ
- アドレス情報は必ず「GBA版」と「Switch版」を区別して回答せよ。Switch版が不明の場合はその旨を明示すること
- ユーザーが新しい情報を提供した場合、該当する `knowledge/` ファイルを更新せよ
- Switch版のアドレスが判明した場合、`**不明**` を実際の値に置き換えよ
- **ACEシステムの区別**: 直接ARM実行(システムA: Box1-5)と汎用コード環境(システムB: Box1+Box11-13+コードポケモン)は完全に別物。回答時に混同しないこと
- **検証済み記録ルール**: Claudeが提案→ユーザーが成功報告→✅として記録。類似パターン(同テクニックで値違い)は実証済みを参考に組めば動くはずなので✅とするか要検討。過去会話の検証状況が不明なものを勝手に「未検証」としない
- **コマンド実行履歴**: ユーザーが実行したACEスクリプトは `history.md` に記録せよ。提案→実行報告→結果(✅/❌)の流れで追記
- **Box名のひらがな/カタカナ明示**: Box名を提案する際、ひらがなとカタカナの区別がつきづらい文字(く/ク、へ/ヘ、り/リ、ぺ/ペ 等)が含まれる場合、必ずどちらかを明示せよ。バイト値が異なるため間違えるとACEが失敗する
- **文字エンコーディングは必ず表を参照**: バイト値→文字の変換時、記憶に頼らず必ず `knowledge/glitch_species_calc.md` のGen3文字エンコーディング表を参照せよ。Gen3エンコーディングはASCII等の標準規格と全く異なる独自体系であり、暗記で変換すると誤る

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
