# Kerning the Chaos

A working studio for web craft: interactive guides, reusable Claude skills, notes worth keeping, and practice pieces. The site is published with GitHub Pages from this repository.

## How it's organized

| Folder | On the site | What goes here |
| --- | --- | --- |
| `guides/` | **Specimens** | Self-contained interactive HTML guides with live demos. Open them in a browser. |
| `skills/` | **Sorts** | Reusable Claude skills, one folder each, with a `SKILL.md` and a short README. |
| `notes/` | **Proofs** | Distilled write-ups of conversations worth keeping. Named `YYYY-MM-DD-topic.md`. |
| `studies/` | **Studies** | Small pieces built from the guides' practice plans, one folder per study. |

`index.html` is the landing page and links to everything. When something is added to a folder, it also gets a line on the landing page.

## Conventions

Notes are write-ups, not transcripts: the question, what was learned, and the code or values worth reusing. Personal topics stay out of this repository, because it's public.

Guides load GSAP, Three.js and Anime.js from jsDelivr and fonts from Google Fonts, so they need internet access.
