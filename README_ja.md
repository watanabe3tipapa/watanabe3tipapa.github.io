[![watanabe3tipapa.github.io](https://img.shields.io/badge/Quarto-Website-4488cc.svg)](https://quarto.org)
[![License](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](LICENSE)
[![GitHub Pages](https://img.shields.io/badge/Hosted-GitHub%20Pages-222222.svg)](https://pages.github.com)

[English](README.md) | [日本語](README_ja.md)

# watanabe3tipapa.github.io

[Quarto](https://quarto.org/) で構築した個人ポータルサイトです。GitHub Pages で公開しています。

## 特徴

- Quarto による静的サイト
- カスタム工業デザインテーマ（ダークカラー）
- 「ターミナルの仕業」ワークショップシリーズ
- Toolsmith プロジェクトポートフォリオ

## ローカル開発

```bash
# 前提: Quarto のインストール
# https://quarto.org/docs/get-started/

# ローカルプレビュー
quarto preview

# docs/ にビルド
quarto render

# 出力先: docs/（GitHub Pages に公開）
```

## プロジェクト構成

```
.
├── _quarto.yml          # サイト設定
├── index.qmd            # トップページ
├── articles/            # 記事・ノート
├── projects/            # プロジェクトページ
│   ├── project.qmd
│   ├── HowtoexecutefromTerminal/  # ターミナルの仕業シリーズ
│   └── extra/
├── link/                # 内部リンク集
├── html/styles.scss     # カスタム工業テーマ
├── assets/              # 画像・静的ファイル
├── docs/                # ビルド出力（公開）
└── v1.0/                # 旧バージョン（保存）
```

## コントリビューション

コントリビューションは大歓迎です！まず [CONTRIBUTING.md](CONTRIBUTING.md) と [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) をお読みください。

## ライセンス

コンテンツは [CC BY-SA 4.0](LICENSE) のもとで提供されています。

## 連絡先

GitHub: [https://github.com/watanabe3tipapa/watanabe3tipapa.github.io](https://github.com/watanabe3tipapa/watanabe3tipapa.github.io)
