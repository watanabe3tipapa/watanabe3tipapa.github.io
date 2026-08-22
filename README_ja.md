[![watanabe3tipapa.github.io](https://img.shields.io/badge/Quarto-Website-4488cc.svg)](https://quarto.org)
[![License](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](LICENSE)
[![GitHub Pages](https://img.shields.io/badge/Hosted-GitHub%20Pages-222222.svg)](https://pages.github.com)
[![Version](https://img.shields.io/badge/version-v0.2.1-637d92.svg)](CHANGELOG.md)

[English](README.md) | [日本語](README_ja.md)

# watanabe3tipapa.github.io

[Quarto](https://quarto.org/) で構築した公開サイト・サービス一覧とToolsmithポータルです。GitHub Pages で公開しています。

## v0.2.1

3つの関連リポジトリの役割と導線を整理しました。このリポジトリは、現在公開しているサイト、サービス、記事、プロジェクトの一覧を担う**現行資産の正本**です。個人としての活動紹介は `watanabe3tipapa`、構築・公開・運用の記録は `next` を参照します。

| リポジトリ | 公開先 | 役割 |
| --- | --- | --- |
| `watanabe3tipapa` | [個人ポータル](https://watanabe3tipapa.github.io/watanabe3tipapa/) | 活動、制作、連絡先への入口 |
| `watanabe3tipapa.github.io` | [公開サイト・サービス一覧](https://watanabe3tipapa.github.io/index/) | 現在公開している資産と更新状況の正本 |
| `next` | [next.watanabe3ti.com](https://next.watanabe3ti.com/) | 設計意図、構築方法、公開経路、運用判断の記録 |

## 特徴

- Quarto による静的サイト
- ソフト・ネオブルータリズムのカスタムテーマ
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
│   └── archive/         # 旧版アーカイブ（v1.0.tar.gz）
├── docs/                # ビルド出力（公開）
├── DEV-MEMO.md          # 開発メモ（非公開）
├── ECOSYSTEM.md         # 3リポジトリの役割分担
```

## ライセンス

コンテンツは [CC BY-SA 4.0](LICENSE) のもとで提供されています。

## 連絡先

GitHub: [https://github.com/watanabe3tipapa/watanabe3tipapa.github.io](https://github.com/watanabe3tipapa/watanabe3tipapa.github.io)
