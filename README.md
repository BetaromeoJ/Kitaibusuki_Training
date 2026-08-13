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
│   ├── js/main.js          共通スクリプト（コピー・アコーディオン・スプラッシュ等）
│   └── images/             講師写真・書影を置く場所（現在は空。無くても崩れません）
└── README.md
```

ビルド環境不要の静的HTMLです。ファイル一式をそのままアップロードするだけで動作します。
外部依存はGoogle Fonts（M PLUS Rounded 1c／Material Symbols）のみで、CDNライブラリは使用していません。
自治体ネットワークでGoogle Fontsが読み込めない場合も、フォールバックフォント（游ゴシック等）で
レイアウトは崩れません。

## セクション構成（index.html内のid）

| セクション | id | 内容 |
|---|---|---|
| ヒーロー | `#top` | Work Smarter. Teach Better. |
| 4つの使い方 | `#usage` | A当日に使う／B自分で学ぶ／C復習する／D今後使う |
| 今日の研修 | `#today` | 研修情報カード＋SESSION 01・02 |
| SESSION 01 | `#session01` | 音声×生成AI（演習・プロンプト・注意事項） |
| SESSION 02 | `#session02` | Gemini Notebook×Canva（ワークフロー） |
| Canva Basics | `#canva-basics` | 動画プレースホルダー10本 |
| 研修後に復習する | `#after` | クイックリンク・FAQ・参考リンク |
| 教科別活用例 | `#subjects` | 13教科・立場のカード |
| プロンプトライブラリ | `#prompts` | 音声／授業／校務／Canvaの16プロンプト |
| AI活用ロードマップ | `#roadmap` | STEP01〜07 |
| ツールの使い分け | `#tools` | ChatGPT／Gemini／Gemini Notebook／Canva |
| 講師紹介 | `#instructor` | 既存の吉野東小学校サイトの内容をそのまま使用 |
| 著作紹介 | `#book` | 既存の吉野東小学校サイトの内容をそのまま使用 |

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

`index.html`内の以下のコメントで囲まれた範囲を編集してください（内容は吉野東小学校版から変更していません）。

```html
<!-- 講師プロフィール：ここから編集 -->　…　<!-- 講師プロフィール：ここまで -->
<!-- 著作情報：ここから編集 -->　…　<!-- 著作情報：ここまで -->
```

写真・書影は `assets/images/instructor-illustration.png`・`google-trainer-badge.png`・
`canvassador-badge.png`・`book-cover.png` に置き換えてください。画像が無くてもアイコン表示で
レイアウトは崩れません。

## デモ音声の設定方法

`#session01`内の「デモ音声（準備中）」カード（`.audio-placeholder`）に、実際のリンクを追加してください。
研修では実際の生徒・保護者・教職員の音声は使用せず、デモ用音声のみを使用します。

## 配色の変更方法

`assets/css/style.css`先頭の`:root { ... }`ブロックの値だけを書き換えれば、サイト全体の色が変わります。

## 公開前の確認事項

- [ ] すべてのページ内リンク（`#today` `#prompts` など）が正しいセクションへ移動するか
- [ ] iPad・スマートフォンSafariで表示したときに横スクロールが発生しないか
- [ ] プロンプトのコピーボタンが動作し、「コピーしました」の通知が表示されるか
- [ ] オープニング演出（黒い幕が下から上へ流れて消える）が2秒程度で終わり、操作を妨げないか
- [ ] 講師写真・書影の画像が無い状態でもレイアウトが崩れないか
- [ ] Canva Basics動画のURLを設定した場合、正しく再生されるか
- [ ] デモ音声のリンクを設定したか
- [ ] GitHub Pages等で公開後、実機（スマートフォン・iPad・PC）で表示確認したか
