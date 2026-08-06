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
