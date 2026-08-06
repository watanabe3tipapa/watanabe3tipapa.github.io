# DEV-MEMO

リポジトリ改訂作業の進行メモ。

## 対象リポジトリ
- watanabe3tipapa.github.io (Quarto 製ポートフォリオ/ポータルサイト)
- ブランチ: `main` / デプロイ: GitHub Pages (gh-pages / docs 出力)

---

## 2026-08-06 : v1.0 塩漬け（手法B・単一アーカイブ化）

### 背景
`v1.0/` は旧世代 Jekyll ソース一式（`.md` 8 + `.github/workflows/` 2 + `_config.yml` + `assets/`画像 5 + `README.md` = 17ファイル）。
過去コミット `06dca1c` 由来で、コミット `be29e4c` にて subtree として導入済み。

**問題点**: Quarto がプロジェクト内 `.md` を自動ビルドするため、`v1.0/*.md` が現行サイトの
`docs/v1.0/*.html` としてビルドされ、`search.json` / `sitemap.xml` に露出していた。
ナビ等からの参照は無いが、ライブサイト上に紛れ込んでいる状態。

### 決定事項
1. 手法 **B（単一アーカイブファイル化）** で塩漬け
2. `docs/v1.0/` のビルド産物は **削除**
3. Git タグ名: **`v1.0-archive`**（二重の保険）

### 手順（実績）
- [x] 1. `v1.0/` を `tar.gz` に圧縮し `assets/archive/v1.0.tar.gz` を生成
- [x] 2. 復元手順を記載した `assets/archive/README.md` を設置
- [x] 3. タグ `v1.0-archive` を付与・push（リモート反映済み）
- [x] 4. `v1.0/`（ソース）を削除
- [x] 5. Quarto 再ビルドし `docs/v1.0/`・`search.json`・`sitemap.xml` から v1.0 を除去
- [x] 6. 検証（アーカイブ生成・露出除去・リンク切れなし）
- [ ] 7. コミット・push（本記録時点で残作業）

### 復元方法（将来）
- **アーカイブ**: `tar xzf assets/archive/v1.0.tar.gz` で展開
- **Git タグ**: `git checkout v1.0-archive -- v1.0/` で当時状態を復元

### 付随設定変更（`_quarto.yml`）
`DEV-MEMO.md` 自体も Quarto にビルドされる問題への対処として以下を追加:
- `website: site-url: https://watanabe3tipapa.github.io` → sitemap.xml / robots.txt の自動生成を有効化
- `project.render` に `"!DEV-MEMO.md"` を追加 → 内部メモをビルド対象外に
- `project.resources: assets/archive/` → 参照されないアーカイブを docs にコピー

### 補足: 注意点
- この `DEV-MEMO.md` は `project.render` で除外しているため、サイトには公開されない。
- 新たに `.md`/`.qmd` を追加する際、非公開にしたいファイルは `project.render` の除外パターンに追加すること。

---

## 2026-08-06 : push 時のトラブル記録

- **SSH 公開鍵拒否**: ローカルの SSH キーが GitHub に未登録だったため、`git push`（SSH）が `Permission denied (publickey)` で失敗。
  - 対処: 認証済みの `gh` CLI（HTTPS）を利用。`gh auth setup-git` + remote を HTTPS に変更。
- **リモート main との分岐**: 作業開始後にリモートへ navbar デザイン変更が 5 件 push されていた（`12782f2`〜`a8858d6`）。
  - 最初の rebase は docs ビルド産物で大量の modify/delete・rename 衝突。
  - 対処: rebase を破棄し `origin/main` にリセット → ソース変更を再適用 → `quarto render` で docs を再生成する方針に切替。
- **教訓**: docs は Quarto の生成物なので、ブランチ統合ではソース（.qmd / _quarto.yml）のみを扱い、docs は必ず再生成すること。

---

## 2026-08-06 : navbar 導線整理

### 背景
navbar 右側の **github アイコン**が GitHub プロフィールではなく、別リポジトリ `watanabe3tipapa/watanabe3tipapa` の
GitHub Pages（Astro 製ブログサンプル LP、`watanabe3tipapa.github.io/watanabe3tipapa`）を指していた。
アイコンと行き先の意味が不一致だった。

### 決定事項
- ブログはサンプル LP として今後も配置（削除せず継続）。
- github アイコン → **GitHub プロフィール** `https://github.com/watanabe3tipapa` に修正。
- ブログ（`watanabe3tipapa.github.io/watanabe3tipapa`）へは navbar 左側に **「Blog」テキストリンク**を追加。

### 変更内容（_quarto.yml）
- `navbar.left` に `- text: "Blog" href: https://watanabe3tipapa.github.io/watanabe3tipapa` を追加
- `navbar.right` の github アイコン href を `https://github.com/watanabe3tipapa` に変更
- `quarto render` で再ビルド・検証済み（Blog / github リンクが正しく反映）

---

## 2026-08-06 : v2 ブラッシュアップ計画

### 決定事項（ユーザー指定）
- **範囲**: すべて（トップページ / デザインテーマ / コンテンツ / 構造）
- **デザイン方向性**: 従来の「Toolsmith Portal — Brutalist-soft」とは **別のもの** に刷新する。

### 作業項目
- [x] 1. デザインテーマ刷新（neo-Brutalism） — `html/styles.scss` + `_quarto.yml`
- [x] 2. トップページ（index.qmd）の刷新 — ポータル化 + INDEX 誘導
- [x] 3. Projects / Articles / Link ページの整理・刷新
- [x] 4. 構造・ナビの整理（navbar に INDEX 追加、footer 変更）
- [x] 5. README の Contributing セクション削除（追加タスク）
- [ ] 6. `quarto render` + 検証
- [ ] 7. コミット・push

### 実装内容（v2 初回）
**デザイン（html/styles.scss）**
- index LP（watanabe3tipapa.github.io/index/）の **neo-brutalism** を踏襲。
- 太い黒ボーダー（3-4px）+ オフセットハードシャドウ（8px 8px 0 等）+ 角丸なし。
- パレット: 黒 #000 / レモン黄 #ffe14d / ライム #9ef01a / パウダーブルー #7ec8e3 / サーモン #ffadad / ピンク #ff2d75 / 背景 #f6f6f4。
- タイポグラフィ: 'Arial Black' 系 + weight 900。見出しは塗りつぶし+影のブロック。
- カード: ホバーで translate(-4px,-4px) の浮き上がり。

**_quarto.yml**
- description を "Neo-Brutalism Portal" に変更。
- theme: `flatly` → `cosmo`。
- navbar.left 先頭に **INDEX**（→ /index/）を追加。
- footer center を「All Sites / Services → INDEX」に変更。

**ページ刷新**
- index.qmd: "Welcome to my portal!" + INDEX 誘導カード + Quick Links。
- link.qmd: 3カテゴリに整理、INDEX 誘導カード追加。
- note.qmd: 記事一覧 + 自由帳 + Quarto メモ。
- project.qmd: INDEX 誘導カード追加。
- README.md / README_ja.md: Contributing セクション削除。

### 未使用アセット整理（追加タスク）
- 参照なしの画像を削除: `assets/IMG_q_p_g.jpg`（434KB）、`assets/UC900.png`（93KB）、`assets/demo-badge.svg`。
- 削除後も `quarto render` が正常であることを確認。

### v2 精錬（第2回） — プロフィール + INDEX 一本化
- **プロフィール（index.qmd）**: About セクション追加。実データに基づき
  "Bricoleur & Toolsmith — Toru Watanabe（小樽・北海道）"、Toolsmith/Bricoleur/Workshop の 3 活動を明記。
  （出典: GitHub profile bio "Bricoleur & Toolsmith"、index リポジトリ説明）
- **INDEX 活用**: GitHub Actions が毎日自動更新する `watanabe3tipapa.github.io/index/` に一本化。
  - project.qmd の手動カード（公開サイト / 検証サイト now 系）を削除し、INDEX 誘導カードに集約。
  - ターミナルの仕業・Extra の手動コンテンツは残す（INDEX に載らない独自コンテンツ）。
- **検証**: `quarto render` 成功、外部リンク重複なし、壊れリンクなし、ターミナルの仕業カード正常。

### v2 精錬（第3回） — トップから INDEX へ自動遷移
- `index.qmd` の `include-in-header` に `<meta http-equiv="refresh" content="5; url=https://watanabe3tipapa.github.io/index/">` を追加。
- トップページ表示から **5秒後に INDEX へ自動遷移**。
- ページ下部に「5秒後に移動」「すぐ移動するリンク」の案内カードを追加。
- **注意**: トップ（/）を開くと必ず INDEX に遷移する仕様。トップに留まりたい場合は `Projects` 等のサブページへ直リンクでアクセスする。

### 心がけ
- ソース（.qmd / _quarto.yml / scss）のみを編集し、`docs/` は必ず `quarto render` で再生成する。
- 更新は DEV-MEMO にこまめに追録する。

---

## 2026-08-06 : GitHub Pages 配信設定の大変更（Actions デプロイ化）

### 経緯（重要）
ライブ `https://watanabe3tipapa.github.io` が **古いまま** で、`main` の `docs/` への変更が全く反映されていなかった。
原因は **GitHub Pages の配信元が `gh-pages` ブランチ（ルート `/`）** になっていたため。
- 旧 `gh-pages` は quarto 1.9.37 でビルドされた v1.0 時代の遺物（旧 navbar / UC900.png / demo-badge.svg 等を配信中）。
- これまで `main` の `docs/` を編集・push していても、配信元が違うので一切無意味だった。

### 決定事項（ユーザー指示に基づく手順）
1. **Pages 配信元を `main` の `/docs` に切替** → その後ユーザーが **「Build and deployment: Actions」** に変更。
   - 最終形: `build_type: workflow`（GitHub Actions がビルドして配信）。
2. `.github/workflows/pages.yml` を新規作成してデプロイを自動化。

### 作成した workflow（.github/workflows/pages.yml）
- トリガー: `push: branches: [main]` + `workflow_dispatch`（手動実行可）。
- 手順:
  1. `actions/checkout@v4`
  2. **`quarto-dev/quarto-actions/setup@v2`** で Quarto インストール（`version: 1.8.27` でローカルと一致させている）
  3. `quarto render` → 出力 `docs/`
  4. `actions/upload-pages-artifact@v3`（path: `./docs`）
  5. `actions/deploy-pages@v4`
- `permissions`: `contents: read` / `pages: write` / `id-token: write` 必須。
- `concurrency: group: pages, cancel-in-progress: false`。

### ハマりどころ（重要）
- **`quarto-dev/quarto-cli/setup@v2` は存在しない**（`v2` タグが無くビルド失敗）。
  正しくは **`quarto-dev/quarto-actions/setup@v2`**（`quarto-actions` リポジトリ）。
  エラー例: `Unable to resolve action quarto-dev/quarto-cli@v2, unable to find version v2`。
- setup の `version:` 指定で、ローカル（1.8.27）と CI の Quarto バージョンを揃える方針。

### 現在の状態（追記時点）
- workflow は commit 済み・push 済み（コミット `1354422`）。
- 直近の Actions run は **進行中**。完了後にライブへ反映される。

### 今後の運用
- `main` への push だけで Quarto ビルド → Pages デプロイまで自動化された。
- ローカルで `docs/` を手動 commit する必要は技術的には無くなったが、既存の docs/ 追跡は維持（変更差分で挙動に注意）。
- Pages の配信元設定（Actions / ブランチ）は GitHub 上で変わると挙動が変わる。変更時は要確認。

---
