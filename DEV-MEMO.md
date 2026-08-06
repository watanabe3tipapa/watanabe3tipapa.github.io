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

### 心がけ
- ソース（.qmd / _quarto.yml / scss）のみを編集し、`docs/` は必ず `quarto render` で再生成する。
- 更新は DEV-MEMO にこまめに追録する。

---
