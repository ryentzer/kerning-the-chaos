---
name: "level-up-guide"
description: "Use when Rick asks to level up on, master, or deeply learn a topic: builds a multi-chapter interactive HTML field guide with live demos, traps, and a practice plan."
---

# Level-Up Guide

The benchmark is the "Motion & Matter" GSAP/Three.js field guide, which Rick called perfect. The goal is mastery-level understanding, not a surface tour. Every guide should leave him able to predict how the thing behaves, know the traps practitioners hit, and have a concrete path to build skill with his own hands.

## 1. Calibrate before building

Find out what he already knows, because the guide starts there. Check the profile and memory for relevant background (for example: 15-20 years of CSS/HTML/JS, a design and art core, 3D work from about 23 years ago, a role as a design engineer at a GPU cloud company). If his current level in the topic is unclear, ask one or two short questions before writing. A wrong guess about his level is the most expensive mistake, because it skews the whole curriculum. Once he answers, adjust the plan in a sentence or two and go.

When his existing knowledge maps onto the new topic, lean on it explicitly. Use translation tables ("You know it as / The new tool / Notes") and analogies from his own domains: animation timing and spacing, compositing, lighting, typography, print.

## 2. Research what changes

Look up anything version-dependent or fast-moving before stating it: current library versions, licensing, product integrations, platform support, award criteria. Verify CDN paths for the exact pinned versions you'll load. Anything you can't verify gets a plain hedge in the text ("check the current state before relying on this"). Rick strongly prefers hedged accuracy over confident guesses.

## 3. Design the curriculum

Organize into 3-4 parts with roughly 10-14 numbered chapters, ordered so each chapter adds one new idea on top of the last. A pattern that works:

- Foundations: the core mental model, exactly how the machinery works underneath
- Expansion: the main tools and techniques, one per chapter
- Integration: where the pieces combine into real work
- Craft: what separates excellent work from competent work, then a practice plan and reference tables

Each chapter contains:

- Explanatory prose in conversational paragraphs (no bullet-heavy sections). Explain *why* things work, not just the API.
- A live "bench": a working demo that runs the real library, with controls he can adjust and a readout of internal values. Include a live code panel that regenerates to match the current control settings, so the code and the behavior are always in sync.
- Practitioner depth: the details people learn only from shipping (performance costs, gotchas, how studios structure real projects).
- Callouts, used sparingly: "Trap" for common mistakes and why they happen, and an insight callout for the non-obvious principle behind high-quality work.
- Concrete experiments to run on the bench ("push X to 1 and watch Y; here's why").

Close with:

- A Craft chapter: quality standards, accessibility (reduced motion and similar), performance, how to study and deconstruct others' work, and how it applies in his tools (such as Webflow).
- A practice plan as a table: Study / What it trains / The constraint that makes it hard. Order from smallest to largest, each adding one idea, and favor small playful finished pieces over one big project.
- Reference tables for syntax and vocabulary he'll look up later.
- Where to read further, with real links.

## 4. Visual design (the "Craft Blueprint" standard)

- Editorial reference-doc layout: a sticky chapter index on the left (collapsing to a toggle on phones), a ~68ch reading column, demo benches slightly wider than the text.
- A natural, well-worn palette: parchment, walnut, moss, brass. Never dark-blue-with-white-text. Dark mode uses deep walnut, not blue.
- A distinctive, specific type pairing: a characterful display face, a readable serif or sans for body, and a mono for labels, readouts and code. Avoid default-AI faces.
- No Mermaid diagrams. Use tables, callouts, and custom canvas or SVG drawings that show the actual mechanism.
- Add a topic-appropriate study aid where it fits, such as a global slow-motion switch for animation topics.
- Benches must be complete at rest. Each shows a meaningful state before any interaction, with no blank shells.

## 5. Build quality

- Load libraries from allowed CDNs, pinned to exact versions, using builds that define a global. Note in the text if the version used differs from what a modern project would import, and what changed.
- Respect `prefers-reduced-motion` for anything that autoplays. Pause rendering when it's off screen. Provide fallbacks (for example, WebGL unavailable).
- Use theme tokens throughout so light and dark both read well. Canvas drawings read colors from the tokens and redraw on theme change.
- Test headless before publishing: install the same library versions locally with npm, route the CDN URLs to the local files in Playwright, render at desktop and phone widths in light and dark, check for console errors and horizontal overflow, and screenshot the key benches. Fix what the screenshots show (exposure, overlapping labels, clipping) in one pass, then publish.

## 6. Writing voice

Plain, direct sentences in conversational paragraphs. Teach deliberately, with reasoning and examples. Avoid em-dash asides and stock filler phrases. Write "we/you" from the learner's side, and name things the way practitioners do.

## 7. Delivery

Publish as an HTML artifact with a real product-style name. In the reply, keep it short:

- one line on what the guide covers
- where to start and why
- what was hedged
- an offer to critique what he builds from the practice plan

Offer markdown reference notes for his "The Stack" Obsidian vault when the topic is CSS, HTML, JS or Webflow.