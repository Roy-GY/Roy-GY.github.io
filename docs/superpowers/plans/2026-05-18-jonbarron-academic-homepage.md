# Jon Barron-Style Academic Homepage Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the Hexo blog with a pure HTML/CSS academic homepage styled after Jon Barron's template.

**Architecture:** Single-page static site — `index.html` (all content in table-based layout, max-width 800px), `stylesheet.css` (Lato font, blue/orange accent links), `images/` (profile photo), `data/` (CV/BibTeX placeholders). No build step, no framework, served directly by GitHub Pages.

**Tech Stack:** HTML5, CSS3, Google Fonts (Lato)

**Things to confirm during implementation:**
- Google Scholar ID (currently using placeholder; ask user)
- Advisor name for bio (currently using placeholder; ask user)
- Full author lists for each paper (currently using "Chengru Wu, et al."; ask user)

---

### Task 1: Save profile photo before cleanup

**Files:**
- Create: `D:/Desktop/blog/images/me.png`

- [ ] **Step 1: Ensure images directory exists and copy photo**

```bash
mkdir -p "D:/Desktop/blog/images"
cp "D:/Desktop/blog/source/images/me.png" "D:/Desktop/blog/images/me.png"
```

---

### Task 2: Clean up old Hexo files

**Files:**
- Delete: `_config.yml`, `_config.landscape.yml`, `package.json`, `package-lock.json`, `db.json`, `CLAUDE.md`
- Delete: `node_modules/`, `scaffolds/`, `source/`, `themes/`, `public/`

- [ ] **Step 1: Remove old Hexo files**

```bash
cd "D:/Desktop/blog"
rm -rf _config.yml _config.landscape.yml package.json package-lock.json db.json CLAUDE.md
rm -rf node_modules/ scaffolds/ source/ themes/ public/
```

- [ ] **Step 2: Verify remaining files**

```bash
ls -la "D:/Desktop/blog"
```

Expected: Only `.gitignore`, `.deploy_git/`, `.github/`, `docs/`, `images/` should remain.

---

### Task 3: Copy template files from Jon Barron's repo

**Files:**
- Create: `D:/Desktop/blog/index.html` (copy from template)
- Create: `D:/Desktop/blog/stylesheet.css` (copy from template)

- [ ] **Step 1: Copy stylesheet**

```bash
cp "/tmp/jonbarron-template/stylesheet.css" "D:/Desktop/blog/stylesheet.css"
```

- [ ] **Step 2: Copy index.html**

```bash
cp "/tmp/jonbarron-template/index.html" "D:/Desktop/blog/index.html"
```

---

### Task 4: Customize index.html — header and bio section

**Files:**
- Modify: `D:/Desktop/blog/index.html`

- [ ] **Step 1: Update meta tags and title**

Replace everything from `<!DOCTYPE HTML>` through `</head>` (lines 1-12) with:

```html
<!DOCTYPE HTML>
<html lang="en">
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">

    <title>Chengru Wu</title>

    <meta name="author" content="Chengru Wu">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" type="text/css" href="stylesheet.css">
    
  </head>
```

- [ ] **Step 2: Update name**

Find `<p class="name" style="text-align: center;">` block and change the text to `Chengru Wu`.

Old:
```html
                <p class="name" style="text-align: center;">
                  Jon Barron
                </p>
```

New:
```html
                <p class="name" style="text-align: center;">
                  Chengru Wu
                </p>
```

- [ ] **Step 3: Update bio paragraph**

Find the first `<p>` after the name (Jon Barron's bio starting with "I'm a principal research scientist...") and replace with:

```html
                <p>
                  I'm an undergraduate student at <a href="https://www.buaa.edu.cn/">Beihang University</a> (北京航空航天大学), majoring in Computer Science and Technology.
                  My research interests include code language models, scientific computing, person re-identification, and multi-agent systems for code generation.
                </p>
```

- [ ] **Step 4: Update link row**

Replace the link row (Email / CV / Bio / Scholar / Twitter / Github) with:

```html
                <p style="text-align:center">
                  <a href="mailto:chengru_wu@buaa.edu.cn">Email</a> &nbsp;/&nbsp;
                  <a href="data/ChengruWu-CV.pdf">CV</a> &nbsp;/&nbsp;
                  <a href="https://github.com/Roy-GY">Github</a>
                </p>
```

- [ ] **Step 5: Update profile photo**

Replace the `<a>` wrapping the profile `<img>`:

Old: `<a href="images/JonBarron.jpg"><img ... src="images/JonBarron.jpg" ...></a>`
New:
```html
                <a href="images/me.png"><img style="width:100%;max-width:100%;object-fit: cover; border-radius: 50%;" alt="profile photo" src="images/me.png" class="hoverZoomLink"></a>
```

---

### Task 5: Replace research section with user's papers

**Files:**
- Modify: `D:/Desktop/blog/index.html`

- [ ] **Step 1: Keep the Research header table, replace its description**

Find the table containing `<h2>Research</h2>` (around lines 45-54). Keep it but update the description `<p>`:

```html
          <table style="width:100%;border:0px;border-spacing:0px;border-collapse:separate;margin-right:auto;margin-left:auto;"><tbody>
              <tr>
              <td style="padding:16px;width:100%;vertical-align:middle">
                <h2>Research</h2>
                <p>
                  I'm interested in code language models, scientific computing, person re-identification, and multi-agent systems for code generation. Representative papers are listed below.
                </p>
              </td>
            </tr>
          </tbody></table>
```

- [ ] **Step 2: Delete all existing paper `<tr>` blocks**

Remove everything from the opening `<table>` tag after the Research header (the table with `border-spacing:0px 10px`) through its closing `</tbody></table>` just before the Miscellanea section. This removes all of Jon Barron's ~50 paper entries.

- [ ] **Step 3: Insert user's paper table**

In place of the deleted paper entries, insert:

```html
          <table style="width:100%;border:0px;border-spacing:0px;border-collapse:separate;margin-right:auto;margin-left:auto;"><tbody>

            <tr>
              <td style="padding:16px;width:100%;vertical-align:middle">
                <a href="https://ieeexplore.ieee.org/document/10977820">
                  <span class="papertitle">On the Applicability of Code Language Models to Scientific Computing Programs</span>
                </a>
                <br>
                <strong>Chengru Wu</strong>, et al.
                <br>
                <em>IEEE Transactions on Software Engineering (TSE)</em>, 2025
                <br>
                <a href="https://ieeexplore.ieee.org/document/10977820">IEEE</a>
                <p></p>
              </td>
            </tr>

            <tr>
              <td style="padding:16px;width:100%;vertical-align:middle">
                <a href="https://ieeexplore.ieee.org/document/11209188">
                  <span class="papertitle">CCUP: A Controllable Synthetic Data Generation Pipeline for Pretraining Cloth-Changing Person Re-Identification Models</span>
                </a>
                <br>
                <strong>Chengru Wu</strong>, et al.
                <br>
                <em>IEEE International Conference on Multimedia and Expo (ICME)</em>, 2025
                <br>
                <a href="https://ieeexplore.ieee.org/document/11209188">IEEE</a>
                <p></p>
              </td>
            </tr>

            <tr>
              <td style="padding:16px;width:100%;vertical-align:middle">
                <a href="https://arxiv.org/abs/2506.10525">
                  <span class="papertitle">AdaptiveLLM: A Framework for Selecting Optimal Cost-Efficient LLM for Code-Generation Based on CoT Length</span>
                </a>
                <br>
                <strong>Chengru Wu</strong>, et al.
                <br>
                <em>Internetware</em>, 2025
                <br>
                <a href="https://arxiv.org/abs/2506.10525">arXiv</a>
                <p></p>
              </td>
            </tr>

            <tr>
              <td style="padding:16px;width:100%;vertical-align:middle">
                <a href="https://arxiv.org/abs/2511.03404">
                  <span class="papertitle">Towards Realistic Project-Level Code Generation via Multi-Agent Collaboration and Semantic Architecture Modeling</span>
                </a>
                <br>
                <strong>Chengru Wu</strong>, et al.
                <br>
                <em>arXiv</em>, 2025
                <br>
                <a href="https://arxiv.org/abs/2511.03404">arXiv</a>
                <p></p>
              </td>
            </tr>

          </tbody></table>
```

---

### Task 6: Add Awards section

**Files:**
- Modify: `D:/Desktop/blog/index.html`

- [ ] **Step 1: Insert Awards section after the paper table**

Insert between the paper table's closing `</tbody></table>` and the Miscellanea section:

```html
          <table style="width:100%;border:0px;border-spacing:0px;border-collapse:separate;margin-right:auto;margin-left:auto;"><tbody>
            <tr>
              <td style="padding:16px;width:100%;vertical-align:middle">
                <h2>Honors & Awards</h2>
              </td>
            </tr>
          </tbody></table>
          <table style="width:100%;border:0px;border-spacing:0px;border-collapse:separate;margin-right:auto;margin-left:auto;"><tbody>
            <tr>
              <td style="padding:8px 16px;width:100%;vertical-align:middle">
                <ul style="margin:0;padding-left:20px;">
                  <li>National Scholarship, 2025</li>
                  <li>National Scholarship, 2024</li>
                  <li>Beihang University Academic Excellence Scholarship (Special Prize), 2025</li>
                  <li>Beihang University Academic Excellence Scholarship (Special Prize), 2024</li>
                  <li>Beihang University Merit Student, 2025</li>
                  <li>Mathematical Contest in Modeling (MCM) — Meritorious Winner (M Award), 2025</li>
                  <li>Mathematical Contest in Modeling (MCM) — Honorable Mention (H Award), 2024</li>
                </ul>
              </td>
            </tr>
          </tbody></table>
```

---

### Task 7: Simplify Miscellanea section

**Files:**
- Modify: `D:/Desktop/blog/index.html`

- [ ] **Step 1: Replace entire Miscellanea block**

Find and replace the Miscellanea section (contains Micropapers, Recorded Talks, Academic Service, Teaching sub-sections) with:

```html
          <table style="width:100%; margin:0 auto; border:0; border-spacing:0; padding:16px;"><tbody>
            <tr>
              <td>
                <h2>Miscellanea</h2>
              </td>
            </tr>
          </tbody></table>
          <table style="width:100%;border:0px;border-spacing:0px;border-collapse:separate;margin-right:auto;margin-left:auto;"><tbody>
            <tr>
              <td style="padding:8px 16px;width:100%;vertical-align:middle">
                <ul>
                  <li>Hobbies: Volleyball, Gaming</li>
                </ul>
              </td>
            </tr>
          </tbody></table>
```

---

### Task 8: Update footer

**Files:**
- Modify: `D:/Desktop/blog/index.html`

- [ ] **Step 1: Update the footer credit line**

Find the last `<p style="text-align:right;font-size:small;">` and replace with:

```html
                <p style="text-align:right;font-size:small;">
                  Template adapted from <a href="https://github.com/jonbarron/jonbarron.github.io">Jon Barron's website</a>.
                </p>
```

---

### Task 9: Update .gitignore

**Files:**
- Modify: `D:/Desktop/blog/.gitignore`

- [ ] **Step 1: Replace .gitignore content**

```bash
rm "D:/Desktop/blog/.gitignore"
```

Then create `D:/Desktop/blog/.gitignore` with:
```
.DS_Store
Thumbs.db
*.log
.deploy*/
```

---

### Task 10: Create data/ directory

**Files:**
- Create: `D:/Desktop/blog/data/.gitkeep`

- [ ] **Step 1: Create data directory**

```bash
mkdir -p "D:/Desktop/blog/data" && touch "D:/Desktop/blog/data/.gitkeep"
```

---

### Task 11: Write new CLAUDE.md

**Files:**
- Create: `D:/Desktop/blog/CLAUDE.md`

- [ ] **Step 1: Write CLAUDE.md**

```markdown
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
```

---

### Task 12: Verify in browser

- [ ] **Step 1: Open index.html**

```bash
start "D:/Desktop/blog/index.html"
```

- [ ] **Step 2: Manual checklist**

Verify each item in the browser:
- [ ] Name "Chengru Wu" is displayed
- [ ] Profile photo loads (images/me.png)
- [ ] Bio text is correct
- [ ] Email link works: `mailto:chengru_wu@buaa.edu.cn`
- [ ] 4 papers listed under Research with correct titles and working links
- [ ] 7 awards listed under Honors & Awards
- [ ] Footer credits shown
- [ ] Lato font renders, links are blue (#1772d0), hover turns orange (#f09228)
- [ ] Page is responsive (resize to mobile width — layout still readable)
```
