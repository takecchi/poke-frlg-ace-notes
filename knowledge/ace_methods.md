# ace_methods: ACE発動方法

## 方法A: わざ/攻撃ACE (旧手法)

バグポケモンの不正な攻撃アニメーションのコールバックポインタがgPokemonStorage内に着地し発動。

## 方法B: つかむ/いれかえACE (2023年12月〜主流)

グリッチ種族名のバッファオーバーフローでgStorage内のmonPlaceChangeFuncポインタが上書きされる。

手順:
1. PC「ポケモンをいどうさせる」モード
2. SELECT → ならべかえモード(オレンジカーソル)
3. グリッチ種族をAで掴む
4. いれかえ操作 → 実行がgPokemonStorageにリダイレクト

## 前提: メールバグ (Mail Glitch)

ACE用グリッチポケモン作成の基礎exploit。

必要技: はたきおとす(Knock Off), リサイクル(Recycle)
必要道具: 消費アイテム(オボンのみ等), レトロメール×100+

メカニズム: ダブルバトルで以下が同時発生しメールID追跡が非同期化:
1. きのみ自動消費
2. はたきおとすがメール除去
3. リサイクルが消費アイテム回収

→ 「?メール」(QMM)が発生 → Box3 Slot1のポケモンデータを指す
→ QMMでPID/TIDを書き換え → 任意グリッチ種族作成可能

## HOCKルート (非日本語版・殿堂入り前)

1. メールバグでBox3 Slot1にグリッチ種族0x0200("HOCK")作成
2. 努力値付与: HP EV 80(タウリン8個) + HP EV 1(キャタピー) + Atk EV 1(ドードー/マンキー)
3. メールバグ再実行(ワード位置入替) → 0x0200をACE種族0x0351に変換
4. 性格値変遷: 0x00000000 → 0x1E000000 → 0x20000000 (GBA版 / Switch版: **不明**)
5. 種族計算: hpEV + (atkEV × 256) = 0x0351 (GBA版 / Switch版: **不明**)

## 日本語版: ニドくんチャート (0xFFC9セットアップ)

おせけん氏(@vs_prof_oak)が解説。pomeg-letterbombersでは "Japanese ACE Setup: ニドくん Route" として記載。

### 材料ポケモン
ニドラン♂(NN:ニドくん): 5番道路地下通路入口でNPC交換で入手。
PID固定=0x4C970B9E, TID=63184 → 乱数調整不要。

### 手順

1. ニドくんをふしぎなアメでLv9(経験値419) → 育て屋に預けて74歩 → 引き取ると経験値493
2. ニドくんをBox3 Slot1に配置
3. メールバグ(はたきおとす+リサイクル)でQMM生成
4. メール書き込み: メールスロット255がBox3 Slot1の40バイト目(growthサブストラクチャのspecies)を上書き
   - 経験値493の場合: 3番目の言葉=「レベル」、5番目の言葉=削除
5. ニドくんが中間グリッチ種族に変化 → 通称「天元」(元ニドくん)
6. ボックス名コード(Box1〜5)を設定し、ならべかえモードで掴む→入れ替え×2→あずけるモードに切替
7. → 手持ちにグリッチ種族0xFFC9が生成される

### 0xFFC9の詳細
- 表示名: LG=「みみぅむぅ」、FR=「むぅァいァい」
- 性別: メス、Lv0
- ACE発動モード: Thumbモード
- エントリーポイント: 0x0203027F付近 (Box12 Slot29付近)
- 以降、ボックス名にペイロードを書いて0xFFC9を入れ替えるだけでACE繰り返し実行可能

### 0xFFC9セットアップ用ボックス名 (Box1〜5)

※ `空` = 空白文字 (FRLGには漢字がないため、空白を「空」と表記する)

GBA版:
```
Box 1: リ空び…ｏく空ゼｎ
Box 2: 空…ｔま空１ｔほ
Box 3: ぁｍ空空あい
Box 4: アＢぢいいＮ
Box 5: Ｏ
```

Switch版 (1.0.0):
```
Box 1: リ空び…ｏく空ゼｎ
Box 2: 空…ｔま空１ｔほ
Box 3: ぁｍ空空あい
Box 4: ア／ぢいいＮ  ← Ｂ→／ に変更
Box 5: Ｏ
```

### 参考
- おせけん動画: https://www.youtube.com/watch?v=1b2hJQ1ErPk
- pomeg-letterbombers ニドくんRoute: https://pomeg-letterbombers.github.io/pokemon-ace-notes/frlg-jpn-nido-route/
- pomeg-letterbombers Main Route: https://pomeg-letterbombers.github.io/pokemon-ace-notes/frlg-jpn-main-route/
