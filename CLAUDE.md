# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static academic personal homepage for Chengru Wu (吴承儒), styled after Jon Barron's website. Pure HTML/CSS — no build step, no framework. Hosted on GitHub Pages at `Roy-GY.github.io`.

## File Structure

```
index.html          # Single-page site: bio, research, awards
stylesheet.css      # Lato font, blue/orange accent, responsive
images/             # Profile photo (me.png) + paper thumbnails
data/               # CV PDF, BibTeX files
```

## Making Changes

- All content is in `index.html`. Edit directly with any text editor.
- To preview: open `index.html` in a browser (no server needed).
- To add a paper: copy an existing `<tr>` block in the Research section and update the title, authors, venue, and links.
- To update styles: edit `stylesheet.css`.

## Deployment

Push to the `master` branch. GitHub Pages serves the root of the repo directly.
