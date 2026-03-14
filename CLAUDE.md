# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-file static HTML media player for Washing Apples band practice sessions and live sets. No build step, no dependencies, no package manager — just `index.html` served as a static site.

## Architecture

Everything lives in `index.html`:
- **CSS** in `<style>` — black/white minimal design, responsive at 580px breakpoint
- **HTML** — static shell with `#sessions` container populated by JS
- **JS** — self-executing IIFE, no framework or external libraries

Audio files are stored in `media/<folder-name>/` (e.g. `media/3-14-2026/`).

## Adding a New Session

Edit the `SESSIONS` array at the top of the `<script>` block in `index.html`. Add a new object with `date`, `name`, `folder`, and `tracks`. Use `unshift` to add at the top (newest first):

```js
{
  date:   "MAR 14, 2026",
  name:   "PRACTICE",
  folder: "media/3-14-2026",
  tracks: [
    { title: "Song Name", file: "Song Name.mp3" }
  ]
}
```

File paths use `encodeURIComponent` per segment, so spaces in filenames are handled automatically.

## Deployment

The site is a static file — deploy by serving `index.html` and the `media/` directory from any static host. Merging to `main` triggers deployment.
