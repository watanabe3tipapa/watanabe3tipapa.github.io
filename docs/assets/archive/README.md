# Archive: v1.0（旧世代 Jekyll ソース）

`v1.0/`（旧世代のポートフォリオ/ポータルソース一式）を単一アーカイブファイルとして塩漬け保存したもの。

## 内容
- `v1.0.tar.gz` — 旧世代 Jekyll ソース一式（.md 記事、_config.yml、.github/workflows、assets 画像 等）
- 過去コミット `06dca1c` 由来。Git タグ `v1.0-archive` にも同一状態を保存済み。

## 復元方法

### アーカイブから復元
リポジトリのルートで展開すると `v1.0/` ディレクトリが復元される。

```bash
tar xzf assets/archive/v1.0.tar.gz
```

### Git タグから復元（当時の状態を完全に再現）
```bash
git checkout v1.0-archive -- v1.0/
```

## 経緯
- 2026-08-06 に現行 Quarto サイトのビルド対象から外すため塩漬け。
- 詳細はリポジトリルートの `DEV-MEMO.md` を参照。
