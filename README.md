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
│   ├── js/main.js          共通スクリプト（コピー・アコーディオン・Session全画面ビュー・スプラッシュ等）
│   ├── images/             書影・バッジ画像（book-cover.png ほか、設定済み）
│   └── video/              講師紹介動画（instructor-illustration.mp4、設定済み）
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
| 講師紹介 | `#instructor` | プロフィール・資格バッジ（Google認定トレーナー／Canva Canvassador）・資格取得推進リンク |
| 著作紹介 | `#book` | 書影・実績バッジ（Amazon1位／増刷決定） |
| 4つの使い方 | `#usage` | A当日に使う／B自分で学ぶ／C復習する／D今後使う |
| 今日の研修 | `#today` | 研修テーマ＋Session 1〜3のカード（数字順に表示、開くボタンで全画面表示。すべて本日実施） |
| Session 1 全画面ビュー | `#session1-view` | 音声×生成AI。iPadでの録音とGeminiへの渡し方（方法A：文字起こしをコピー貼り付け／方法B：音声データをそのまま共有）を案内したうえで、Part A（単発の音声を要約・議事録・ToDoへ）とPart B（ロールプレイ音声をGemini Notebookで面談記録・学級通信・管理職への報告へ変換）の2部構成。メニュー等のリンクから開き、幕の演出で入場 |
| Session 2 全画面ビュー | `#session2-view` | Gemini Notebookで資料（学習指導要領・授業資料等）を活用し、要点整理・授業案・確認問題を作成する。末尾に応用編として、自分の授業音声をGemini Notebookにソースとして追加し、セルフで振り返る内容を追加。同上 |
| Session 3 全画面ビュー | `#session3-view` | Gemini NotebookのStudio機能とCanvaのマジックレイヤーで、資料をインフォグラフィック・スライド教材へ仕上げる。Canvaに未ログインの先生向けに「Canvaを開く」ボタンと県域教育アカウント（@kago.ed.jp）でのログイン案内を設置。I Love PDFへのリンクあり。同上 |
| Canva Basics | `#canva-basics` | Canva公式の学習コンテンツ（無料）3件へのリンクカード |
| 研修後に復習する | `#after` | クイックリンク・FAQ・参考リンク |
| 教科別活用例 | `#subjects` | 13教科・立場のカード |
| プロンプトライブラリ | `#prompts` | 音声／授業／校務／Canvaの16プロンプト |
| AI活用ロードマップ | `#roadmap` | STEP01〜07 |
| ツールの使い分け | `#tools` | ChatGPT／Gemini／Gemini Notebook／Canva |

## Session 1〜3の全画面ビューについて

ヘッダーメニュー（モバイル）・「Sessionを開く」ボタン・「研修後に復習する」のクイックリンク・各Session末尾の
「次のSessionへ」リンクなど、`href="#session1"`〜`href="#session3"` を持つリンクをクリックすると、
通常のスクロールではなく、そのセッションだけを覆う全画面ビューが開きます（他のSessionが開いていた
場合は自動的に閉じ、常に1つだけが表示されます）。入場時にはサイトの青（`--color-blue-deep`）の幕が
下から上へ流れて消える演出が入ります。ビュー右上の「閉じる」ボタン、または Esc キーで元の画面に
戻れます。この動作は `assets/js/main.js` の `initSessionViews()`（対象idは `SESSION_VIEW_IDS`）で
制御しています。

もとは吉野東小学校ICT研修ポータルの第1〜5講座（音声×生成AI／ロールプレイ音声の文書変換／資料活用／
授業音声の振り返り／StudioとCanvaで教材作成）をもとに、北指宿中学校向けに内容を調整したものです
（`児童`→`生徒`、`小学校`→`中学校` 等の表記変更を含む）。2026年8月20日の改訂で、研修時間（120分）に
実施順を一致させるため、次のように再構成しました。

- 旧SESSION 2（ロールプレイ音声の文書変換）の内容を、旧SESSION 1（音声×生成AI）に統合し、
  新しい **Session 1** としました。Part A（単発の音声を要約・議事録・ToDoへ）と
  Part B（ロールプレイ音声を面談記録・学級通信・管理職への報告へ）の2部構成です。
- 旧SESSION 4（授業音声を振り返りに生かす）の内容を、Gemini Notebookにソースとして追加する方式に
  書き換えたうえで、旧SESSION 3（資料の活用）の応用編として統合し、新しい **Session 2** としました。
- 旧SESSION 5（StudioとCanvaで教材を作る）は **Session 3** としてそのまま繰り上がりました。

これにより、旧SESSION 1・4のような「自分のペースで（研修前後に）」の自己学習用セッションはなくなり、
Session 1〜3のすべてを本日実施します。表記も、それまで混在していた大文字表記「SESSION」を、
サイト全体で「Session」に統一しています。なお、当初は各SessionカードやSessionビューに「本日 STEP 1
／2／3」のバッジも付けていましたが、2026年8月20日の追加修正でこのバッジ表記は廃止し、「Session 1」
「Session 2」「Session 3」の表示のみに統一しています。

## iPadでの録音とGeminiへの渡し方

北指宿中学校のタブレットはiPadです。録音には標準の「ボイスメモ」アプリを使います。Session 1冒頭で、
録音した音声をGeminiに渡す2つの方法を案内しています。

- **方法A**：ボイスメモの文字起こしを開く → 全選択してコピー → Geminiに貼り付けて送信
- **方法B**：ボイスメモの共有ボタンからGemini（またはGemini Notebook）を選び、音声データをそのまま
  添付・追加して送信

単発の内容をすぐ整理したいときはどちらでもかまいませんが、同じ音声から複数の文書を作り直したい
Part B（ロールプレイ音声の文書変換）やSession 2の応用編（授業音声の振り返り）では、音声データを
Gemini Notebookに追加する方法Bが向いています。

## 研修当日の進め方

`#today`のSessionカードは1〜3の数字順に並び、すべて研修時間内（13:00〜15:00）に実際に扱います。

| 時間 | 内容 |
|---|---|
| 10分 | 開会・講師紹介・研修の趣旨説明 |
| 30分 | Session 1 |
| 30分 | Session 2 |
| 20分 | Session 3 |
| 30分 | クロージング・おかわりタイム |

合計120分で、研修時間「13:00〜15:00」と一致します。ヘッダーメニュー・「研修後に復習する」の
クイックリンクも、この数字順（1〜3）に統一しています。

## Canva Basicsについて

`#canva-basics`（Canva Basics）は自作動画ではなく、Canva公式の学習コンテンツ（無料）3件へのリンクカードです。

- Canva使い方完全ガイド（`https://www.canva.com/ja_jp/learn/how-to/`）：リンクボタンあり
- Canvaデザインスクール（動画）（`https://www.canva.com/ja_jp/design-school/videos/`）：リンクボタンあり
- Canva日本公式ブログ（`https://www.canva.com/ja_jp/learn/`）：本文中のテキストリンク

リンク先を変更する場合は、`index.html`内 `<!-- ===== LEARN BY YOURSELF：Canva Basics ===== -->` 以下の
`.tool-card`（3枚）の`href`とテキストを書き換えてください。

なお、Canvaに未ログインの先生向けに、Session 3冒頭に「Canvaを開く」ボタン（`https://www.canva.com/login`）
と「県域教育アカウント（@kago.ed.jp）でログインしてください」という案内を設置しています。

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

講師紹介の写真は動画に変更し、`assets/video/instructor-illustration.mp4` に設定済みです
（自動再生・ミュート・ループ・インライン再生。差し替える場合は同名で上書き）。
書影・バッジは `assets/images/google-trainer-badge.png`・`canvassador-badge.png`・`book-cover.png`
に設定済みです（差し替える場合は同名で上書き）。動画・画像が読み込めない場合もアイコン表示で
レイアウトは崩れません。

資格バッジ（Google for Education 認定トレーナー／Canva Canvassador）は、各`.badge-row`内でラベルの
pillとバッジ画像を横並びにし、`.badge-img`（トレーナー）／`.badge-img-round`（Canvassador）とも
高さ88pxに揃え、`object-fit: contain`でバッジ全体が切れずに表示されるようにしています
（`assets/css/style.css`）。サイズを変える場合はこの2つのクラスの`height`/`width`を書き換えてください。

講師紹介の紹介文の下には、Google認定教育者・Gemini認定教育者の資格取得を案内するボタン
（`https://edu.google.com/intl/ALL_jp/learning-center/certifications/` へのリンク）を設置しています。

## 配色の変更方法

`assets/css/style.css`先頭の`:root { ... }`ブロックの値だけを書き換えれば、サイト全体の色が変わります。

## 公開前の確認事項

- [ ] すべてのページ内リンク（`#today` `#prompts` など）が正しいセクションへ移動するか
- [ ] iPad・スマートフォンSafariで表示したときに横スクロールが発生しないか
- [ ] プロンプトのコピーボタンが動作し、「コピーしました」の通知が表示されるか
- [ ] オープニング演出（サイトの青い幕が下から上へ流れて消える）が2秒程度で終わり、操作を妨げないか
- [ ] Session 1〜3の全画面ビューが、メニューやボタンから正しく開くか。幕の演出のあとに内容が表示されるか
- [ ] 各Session末尾の「次のSessionへ」リンクで、正しく次のSessionへ切り替わるか（Session 3は「Session一覧に戻る」のみ）
- [ ] Session全画面ビューの「閉じる」ボタン・Escキーで元の画面に戻れるか
- [ ] 講師紹介の動画・書影・資格バッジが正しいサイズ・位置で表示されるか（読み込めない場合もレイアウトが崩れないか）
- [ ] Canva Basicsの3つのリンク（ガイド・動画・ブログ）が正しく開くか
- [ ] Session 3の「Canvaを開く」ボタン・I Love PDFリンクが正しく開くか
- [ ] GitHub Pages等で公開後、実機（スマートフォン・iPad・PC）で表示確認したか
