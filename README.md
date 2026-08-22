[![watanabe3tipapa.github.io](https://img.shields.io/badge/Quarto-Website-4488cc.svg)](https://quarto.org)
[![License](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](LICENSE)
[![GitHub Pages](https://img.shields.io/badge/Hosted-GitHub%20Pages-222222.svg)](https://pages.github.com)
[![Version](https://img.shields.io/badge/version-v0.2.1-637d92.svg)](CHANGELOG.md)

[English](README.md) | [日本語](README_ja.md)

# watanabe3tipapa.github.io

Public-site catalog and Toolsmith portal built with Quarto. This repository is the source for the website published via GitHub Pages and serves as the canonical catalog of currently published sites, services, articles, and projects.

## Current status (v0.2.1)

The roles and links across three related repositories are clarified. This repository is the canonical catalog for currently published assets and their update status. Related repositories and roles:

- `watanabe3tipapa` — Personal portal; entry point for activity, work, and contact information
- `watanabe3tipapa.github.io` — Current sites & services; canonical catalog of published assets (this repository)
- `next` — Record of design intent, architecture, publishing paths, and operations

(Referenced public destinations are listed in the site content.)

## Overview

- Static website powered by Quarto
- Soft Neo-Brutalism theme with custom SCSS
- "Terminal no Shiwaza" workshop series
- Toolsmith project portfolio

## Local development

Prerequisite: Install Quarto (https://quarto.org/docs/get-started/)

To preview the site locally and to render the site (these commands are used in this project):

```bash
# Preview the site locally
quarto preview

# Render to docs/ directory
quarto render

# Output directory: docs/ (published to GitHub Pages)
```

## Project structure

A high-level view of files and directories in this repository:

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

## Development & maintenance

This repository is presented as the canonical catalog and the source for the published site. See CHANGELOG.md for version history and ECOSYSTEM.md for notes about the repository role relative to other related repositories.

## License

Content is licensed under CC BY-SA 4.0. See LICENSE for details.

## Contact

Repository: https://github.com/watanabe3tipapa/watanabe3tipapa.github.io

Site (published): https://watanabe3tipapa.github.io/
