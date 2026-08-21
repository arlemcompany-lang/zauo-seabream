# CLAUDE.md — 伊勢海老（イセエビ）説明ページ

## このフォルダについて
[[魚種別説明ページ]]の一つ。伊勢海老（イセエビ）の説明ページ。
親フォルダのCLAUDE.mdも参照: `../CLAUDE.md`

## 状態
完成・公開済み。鯛と同じフォーマット（動画トップ＋説明カード4枚）。
**2026-08-07に8言語対応済み**（鯵と同じ仕組み）。
公開URL: https://arlemcompany-lang.github.io/zauo-seabream/伊勢海老/

## 構成
- `index.html` — ページ本体（調理法／どんな海老？／どこにいる？旬はいつ？／豆知識）
- `ise-ebi.mp4` — トップの縦長動画

## 残タスク
- 調理法カードの料理写真が未設定（`.photo-placeholder`「写真準備中」のまま）。
  写真が届いたら鯵ページと同じ`.photo-grid`構成に差し替える

## 多言語の仕様（3ページ共通）
- **対応言語は釣りゲーム（`../../ざうおスマホゲーム/index.html`）と完全に同じ8言語・同じ並び順**：
  `ja` 日本語 / `en` English / `zh` 中文（簡体） / `ko` 한국어 / `es` Español / `it` Italiano / `vi` Tiếng Việt / `tl` Tagalog
  - 言語コードもゲームと同一。名称もゲームの `FISH_NAMES` に合わせている
- 動画の**上**に言語切替バー（`.langbar`）。`position: sticky` でスクロール中も追従
- 国旗は**インラインSVG**（絵文字の国旗はWindowsのChrome/Edgeで「JP」等の文字にしか描画されないため使わない）。配色はゲームのCanvas描画関数と揃えてある
- **開いたときは常に日本語**。選択は localStorage 等に保存しない（クライアント要件）
- 翻訳は `<script>` 内の `I18N` に集約。要素側は `data-i18n`（textContent）と `data-i18n-html`（innerHTML／`<strong>`や`<br>`を含む豆知識用）
- 評価記号（◎〇△✕）はHTML側に固定。翻訳対象はメニュー名のみ
- `.lang-name` のフォントは**ラテン系を先頭**にする。CJKフォントが先頭だとベトナム語の「ế」が合成表示になって崩れる
- 言語バーはスマホ4列×2段／640px以上8列×1段。その高さぶん `.video-wrap` を `calc(80vh - var(--langbar-h))` で縮める（スマホ111px／640px以上61px、Playwrightで実測）
