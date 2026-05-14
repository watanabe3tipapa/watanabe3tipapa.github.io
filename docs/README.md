[![watanabe3tipapa.github.io](https://img.shields.io/badge/Quarto-Website-4488cc.svg)](https://quarto.org)
[![License](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](LICENSE)
[![GitHub Pages](https://img.shields.io/badge/Hosted-GitHub%20Pages-222222.svg)](https://pages.github.com)

[English](README.md) | [日本語](README_ja.md)

# watanabe3tipapa.github.io

Personal portal site built with [Quarto](https://quarto.org/). This is the source repository for the website published via GitHub Pages.

## Features

- Static website powered by Quarto
- Industrial dark theme with custom SCSS
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
├── docs/                # Build output (published)
└── v1.0/                # Legacy version (archive)
```

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) and [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) first.

## License

Content is licensed under [CC BY-SA 4.0](LICENSE).

## Contact

GitHub: [https://github.com/watanabe3tipapa/watanabe3tipapa.github.io](https://github.com/watanabe3tipapa/watanabe3tipapa.github.io)
