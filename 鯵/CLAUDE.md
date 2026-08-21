# CLAUDE.md — 鯵（アジ）説明ページ

## このフォルダについて
[[魚種別説明ページ]]の一つ。鯵（アジ）の説明ページ。
親フォルダのCLAUDE.mdも参照: `../CLAUDE.md`

## 状態
完成・公開済み。鯛と同じフォーマット（動画トップ＋説明カード4枚）。
**2026-08-07に多言語版（8言語）を本番へ昇格済み**＝本番URLがそのまま多言語ページ。
公開URL: https://arlemcompany-lang.github.io/zauo-seabream/鯵/

日本語のみだった旧版はコミット `cc0ba07` 以前の `index.html`（戻す場合はそこから復元）。

## 構成
- `index.html` — 本番ページ（多言語・8言語）
- `multi/index.html` — 本番へリダイレクトするだけのページ。昇格前に確認用としてURL・QRコードを配ってしまったため、そのリンクを生かす目的で残している。**ページ本体を複製しない**（二重管理になるため）
- `aji.mp4` — トップの縦長動画
- `aji-tataki.jpg` / `aji-fry.jpg` — 調理法カードの料理写真（1000px幅にリサイズ済み）

## 多言語の仕様
- **対応言語は釣りゲーム（`../../ざうおスマホゲーム/index.html`）と完全に同じ8言語・同じ並び順**：
  `ja` 日本語 / `en` English / `zh` 中文（簡体） / `ko` 한국어 / `es` Español / `it` Italiano / `vi` Tiếng Việt / `tl` Tagalog
  - 言語コードもゲームと同一。魚名もゲームの `FISH_NAMES.aji` に合わせている
    （en: Horse Mackerel / zh: 竹荚鱼 / ko: 전갱이 / es: Chicharro / it: Suro / vi: Cá nục / tl: Alumahan）
  - 繁體中文の全訳も一度作ったが、ゲームに合わせて外した。必要になったらコミット `cc0ba07` から復元できる
- 動画の**上**に言語切替バー（`.langbar`）。`position: sticky` でスクロール中も追従
- 国旗は**インラインSVG**（絵文字の国旗はWindowsのChrome/Edgeで「JP」等の文字にしか描画されないため使わない）。配色はゲームのCanvas描画関数（`drawFlagSpain`等）と揃えてある
- **開いたときは常に日本語**。選択は localStorage 等に保存しない（クライアント要件）
- 翻訳は `<script>` 内の `I18N` オブジェクトに集約。要素側は `data-i18n="キー"`（textContent 差し替え）と `data-i18n-html="キー"`（innerHTML 差し替え／`<strong>`や`<br>`を含む豆知識用）
- 評価記号（◎〇△✕）はHTML側に固定で置き、翻訳対象はメニュー名のみ
- 言語切替時に `<html lang>` と `document.title` も切り替え、`html[lang="ko"]` 等で各言語のフォントスタックを指定
- `.lang-name`（国旗の下のラベル）のフォントは**ラテン系を先頭**にする。CJKフォントを先頭にするとベトナム語の「ế」が ê＋アクセントの合成表示になって崩れる
- 言語バーはスマホで4列×2段、640px以上で8列×1段のグリッド。その高さぶん動画を縮めるため `.video-wrap` は `height: calc(80vh - var(--langbar-h))`（スマホ111px／640px以上61px、Playwrightで実測した値）。これで日本語のみだった旧版と同じ位置にタイトル＋キャッチが見える
- 言語を増減する場合は `<button class="lang-btn">` と `I18N` の該当キー、`--langbar-h` の実測値を合わせて調整する
- 画像・動画は同階層（`aji.mp4`）。波柄背景は2026-08-21に廃止し、動画の背景は `var(--bg)`
