[![watanabe3tipapa.github.io](https://img.shields.io/badge/Quarto-Website-4488cc.svg)](https://quarto.org)
[![License](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](LICENSE)
[![GitHub Pages](https://img.shields.io/badge/Hosted-GitHub%20Pages-222222.svg)](https://pages.github.com)
[![Version](https://img.shields.io/badge/version-v0.2.1-637d92.svg)](CHANGELOG.md)

[English](README.md) | [日本語](README_ja.md)

# watanabe3tipapa.github.io

Public-site catalog and Toolsmith portal built with [Quarto](https://quarto.org/). This is the source repository for the website published via GitHub Pages.

## v0.2.1

The roles and links across three related repositories have been clarified. This repository is the **canonical catalog** for currently published sites, services, articles, and projects. `watanabe3tipapa` introduces the person and their work, while `next` records architecture, publishing, and operational decisions.

| Repository | Public destination | Role |
| --- | --- | --- |
| `watanabe3tipapa` | [Personal portal](https://watanabe3tipapa.github.io/watanabe3tipapa/) | Entry point for activity, work, and contact information |
| `watanabe3tipapa.github.io` | [Current sites & services](https://watanabe3tipapa.github.io/index/) | Canonical catalog of currently published assets and their update status |
| `next` | [next.watanabe3ti.com](https://next.watanabe3ti.com/) | Record of design intent, architecture, publishing paths, and operations |

## Features

- Static website powered by Quarto
- Soft Neo-Brutalism theme with custom SCSS
- "Terminal no Shiwaza" workshop series
- Toolsmith project portfolio

## Local Development

```bash
# Prerequisites: Install Quarto
# https://quarto.org/docs/get-started/

# Preview the site locally
quarto preview

# Render to docs/ directory
quarto render

# Output directory: docs/ (published to GitHub Pages)
```

## Project Structure

```
.
├── _quarto.yml          # Site configuration
├── index.qmd            # Top page
├── articles/            # Articles / Notes
├── projects/            # Project pages
│   ├── project.qmd
│   ├── HowtoexecutefromTerminal/  # Terminal workshop series
│   └── extra/
├── link/                # Internal link collection
├── html/styles.scss     # Custom industrial theme
├── assets/              # Images and static files
│   └── archive/         # Archived legacy version (v1.0.tar.gz)
├── docs/                # Build output (published)
├── DEV-MEMO.md          # Development notes (not published)
└── ECOSYSTEM.md         # Role split across the three repositories
```

## License

Content is licensed under [CC BY-SA 4.0](LICENSE).

## Contact

GitHub: [https://github.com/watanabe3tipapa/watanabe3tipapa.github.io](https://github.com/watanabe3tipapa/watanabe3tipapa.github.io)
