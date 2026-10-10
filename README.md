# All Things AI Dev Newsletter

A practical, source-linked newsletter about using AI well and getting better at agentic software development.

**Read the latest issue and browse the archive:** [bobbygrdn.github.io/AI-and-Agentic-Development-Newsletter](https://bobbygrdn.github.io/AI-and-Agentic-Development-Newsletter/)

## What to expect

- **Monday–Friday:** a new article with useful developments, applied techniques, and ideas for improving agentic development.
- **Saturday:** a weekly recap that connects the week's research, product releases, and lessons for developers.
- **Every issue:** a one-line “Why this matters” under each item, a practical takeaway, linked sources, and a spotlight on a newly released or meaningfully updated AI tool.
- **A readable webpage:** responsive article layout with light and dark themes. The theme follows your device preference until you choose one; your choice is remembered in that browser.

## Browse the archive

Start at the [newsletter homepage](https://bobbygrdn.github.io/AI-and-Agentic-Development-Newsletter/). It links to each published article. Every issue is stored as its own dated HTML page, so later editions add to the archive rather than replacing earlier ones.

## How publishing works

A scheduled edition is researched and written with current, verifiable sources. Its HTML article is added under `site/issues/`, and the homepage is updated with a link while keeping previous issues. A GitHub Actions workflow deploys the complete `site/` folder to GitHub Pages. The email notification contains a short note and the article link; the full article stays on the webpage.

The workflow publishes after changes to `site/` reach the `main` branch. It can also be run manually from the repository's Actions tab.

## Repository map

| Path | Contents |
| --- | --- |
| `site/index.html` | Newsletter homepage and issue archive |
| `site/issues/` | Individual dated articles |
| `.github/workflows/pages.yml` | GitHub Pages deployment workflow |

## Sources and editorial approach

Issues aim to distinguish reported facts from interpretation. Links point to original research, official release notes, product documentation, and credible independent reporting. Vendor performance or product claims are identified as such when relevant; fast-moving details are checked against current sources for each edition.

## Public site

This repository and its GitHub Pages site are public. Articles may be shared by URL. The pages do not require a sign-in to read.
