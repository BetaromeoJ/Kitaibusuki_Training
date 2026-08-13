# 北指宿中学校 ICT研修ポータル

吉野東小学校版ICT研修ポータルのデザイン・構成をベースに、指宿市立北指宿中学校のICT校内研修
（2026年8月21日（金）13:00〜15:00、テーマ「AI × Canva　授業づくりと校務を、もっと軽く。」）に
合わせて再構成した、1ページ完結のポータルサイトです。

## ファイル構成

```
/
├── index.html              全セクションをまとめた1ページ構成
├── assets/
│   ├── css/style.css       共通スタイル（配色・演出はすべてここで管理）
│   ├── js/main.js          共通スクリプト（コピー・アコーディオン・SESSION全画面ビュー・スプラッシュ等）
│   └── images/             講師写真・書影・バッジ画像（instructor-illustration.gif ほか、設定済み）
└── README.md
```

ビルド環境不要の静的HTMLです。ファイル一式をそのままアップロードするだけで動作します。
外部依存はGoogle Fonts（M PLUS Rounded 1c／Material Symbols）のみで、CDNライブラリは使用していません。
自治体ネットワークでGoogle Fontsが読み込めない場合も、フォールバックフォント（游ゴシック等）で
レイアウトは崩れません。

## セクション構成（index.html内のid、ページに表示される順）

| セクション | id | 内容 |
|---|---|---|
| ヒーロー | `#top` | Work Smarter. Teach Better. |
| 講師紹介 | `#instructor` | プロフィール・資格バッジ・資格取得推進リンク |
| 著作紹介 | `#book` | 書影・実績バッジ（Amazon1位／増刷決定） |
| 4つの使い方 | `#usage` | A当日に使う／B自分で学ぶ／C復習する／D今後使う |
| 今日の研修 | `#today` | 研修テーマ＋SESSION 1〜5（開くボタンで全画面表示） |
| SESSION 1 全画面ビュー | `#session1-view` | 音声×生成AI（演習・プロンプト・実践例・注意事項・よくあるトラブル）。メニュー等のリンクから開き、幕の演出で入場 |
| SESSION 2 全画面ビュー | `#session2-view` | Gemini Notebookで、同じ音声を面談記録・学級通信・管理職への報告など別の文書に変換する。同上 |
| SESSION 3 全画面ビュー | `#session3-view` | Gemini Notebookで資料（学習指導要領・授業資料等）を活用し、要点整理・授業案・確認問題を作成する。同上 |
| SESSION 4 全画面ビュー | `#session4-view` | 自分の授業音声をGeminiで分析し、振り返り・次時への改善案を作成する。同上 |
| SESSION 5 全画面ビュー | `#session5-view` | Gemini NotebookのStudio機能とCanvaのマジックレイヤーで、資料をインフォグラフィック・スライド教材へ仕上げる。同上 |
| Canva Basics | `#canva-basics` | 動画プレースホルダー10本 |
| 研修後に復習する | `#after` | クイックリンク・FAQ・参考リンク |
| 教科別活用例 | `#subjects` | 13教科・立場のカード |
| プロンプトライブラリ | `#prompts` | 音声／授業／校務／Canvaの16プロンプト |
| AI活用ロードマップ | `#roadmap` | STEP01〜07 |
| ツールの使い分け | `#tools` | ChatGPT／Gemini／Gemini Notebook／Canva |

## SESSION 1〜5の全画面ビューについて

ヘッダーメニュー・「SESSIONを開く」ボタン・「研修後に復習する」のクイックリンク・各SESSION末尾の
「次のSESSIONへ」リンクなど、`href="#session1"`〜`href="#session5"` を持つリンクをクリックすると、
通常のスクロールではなく、そのセッションだけを覆う全画面ビューが開きます（他のSESSIONが開いていた
場合は自動的に閉じ、常に1つだけが表示されます）。入場時にはサイトの青（`--color-blue-deep`）の幕が
下から上へ流れて消える演出が入ります。ビュー右上の「閉じる」ボタン、または Esc キーで元の画面に
戻れます。この動作は `assets/js/main.js` の `initSessionViews()`（対象idは `SESSION_VIEW_IDS`）で
制御しています。

SESSION 1・2・3・4は吉野東小学校ICT研修ポータルの第1〜4講座をもとに、北指宿中学校向けに内容を
調整したものです（`児童`→`生徒`、`小学校`→`中学校` 等の表記変更を含む）。SESSION 5は同ポータルの
第5講座「StudioとCanvaで教材を作る」をもとにしています。

## Canva Basics動画の設定方法

`index.html`内の各動画カードにある以下のコメント箇所を編集します。

```html
<!-- <div class="video-frame"><iframe src="https://www.youtube.com/embed/XXXXXXXXXXX" ...></iframe></div> -->
<div class="video-placeholder-frame">...</div>
```

1. `<div class="video-frame">...</div>` 行のコメント（`<!--` `-->`）を外す
2. `src` の `XXXXXXXXXXX` を実際のYouTube動画ID（`https://www.youtube.com/embed/`の後ろの文字列）に差し替える
3. 直後の `<div class="video-placeholder-frame">...</div>`（プレースホルダー表示）は削除してください

## プロンプトの追加方法

`#prompts`内の各カテゴリー（音声・授業・校務・Canva）の`<div class="accordion-panel">`内に、
`.prompt-card`ブロックをコピーして追加してください。`.prompt-body`の`id`は、ページ内で重複しない
ユニークな値にしてください。`.copy-btn`の`data-copy-target`に対応する`id`を`#`付きで指定すると、
コピー機能が自動的に有効になります。

## 講師プロフィール・著作情報の編集箇所

`index.html`内の以下のコメントで囲まれた範囲を編集してください。

```html
<!-- 講師プロフィール：ここから編集 -->　…　<!-- 講師プロフィール：ここまで -->
<!-- 資格取得の推進：ここから編集 -->　…　<!-- 資格取得の推進：ここまで -->
<!-- 著作情報：ここから編集 -->　…　<!-- 著作情報：ここまで -->
```

写真・書影は `assets/images/instructor-illustration.gif`・`google-trainer-badge.png`・
`canvassador-badge.png`・`book-cover.png` に設定済みです（差し替える場合は同名で上書き）。
画像が読み込めない場合もアイコン表示でレイアウトは崩れません。

講師紹介の紹介文の下には、Google認定教育者・Gemini認定教育者の資格取得を案内するボタン
（`https://edu.google.com/intl/ALL_jp/learning-center/certifications/` へのリンク）を設置しています。

## デモ音声の設定方法

`#session1`内の「デモ音声（準備中）」カード（`.audio-placeholder`）に、実際のリンクを追加してください。
研修では実際の生徒・保護者・教職員の音声は使用せず、デモ用音声のみを使用します。

## 配色の変更方法

`assets/css/style.css`先頭の`:root { ... }`ブロックの値だけを書き換えれば、サイト全体の色が変わります。

## 公開前の確認事項

- [ ] すべてのページ内リンク（`#today` `#prompts` など）が正しいセクションへ移動するか
- [ ] iPad・スマートフォンSafariで表示したときに横スクロールが発生しないか
- [ ] プロンプトのコピーボタンが動作し、「コピーしました」の通知が表示されるか
- [ ] オープニング演出（サイトの青い幕が下から上へ流れて消える）が2秒程度で終わり、操作を妨げないか
- [ ] SESSION 1〜5の全画面ビューが、メニューやボタンから正しく開くか。幕の演出のあとに内容が表示されるか
- [ ] 各SESSION末尾の「次のSESSIONへ」リンクで、正しく次のSESSIONへ切り替わるか
- [ ] SESSION全画面ビューの「閉じる」ボタン・Escキーで元の画面に戻れるか
- [ ] 講師写真・書影の画像が正しく表示されるか（読み込めない場合もレイアウトが崩れないか）
- [ ] Canva Basics動画のURLを設定した場合、正しく再生されるか
- [ ] デモ音声のリンクを設定したか
- [ ] GitHub Pages等で公開後、実機（スマートフォン・iPad・PC）で表示確認したか
