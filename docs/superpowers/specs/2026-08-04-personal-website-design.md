# Personal website — design spec

**Owner:** Jakub Tkaczuk · **Repo:** `jaktk/personal-website` (al-folio v1.x) · **Date:** 2026-08-04

Turn the al-folio starter (currently full of Albert Einstein placeholder content) into
Jakub Tkaczuk's personal academic/engineering site: chronological publications from Google
Scholar, content adapted from LinkedIn, a project + supervised-thesis showcase, a curated
repository list, and a CV — with teaching and all other demo content removed.

## Confirmed decisions (from brainstorming)

| # | Decision | Choice |
|---|----------|--------|
| 1 | Publications scope | **All** Scholar works, newest-first, grouped by year; ~4 lead-author works marked `selected` for the homepage. |
| 2 | Publication order | **Newest first** (reverse-chronological). |
| 3 | Optional sections kept | **CV** + **Blog**. Removed: Teaching, Books, dropdown demo, News feed. |
| 4 | Hosting | **GitHub Pages user site** → `https://jaktk.github.io`, `baseurl: ""`. |
| 5 | Projects vs theses | **One `projects` collection**; Jakub's work and the 22 student theses are cards separated by **category** and by per-card student attribution. |
| 6 | Full-document links | **Link out**, PDFs stay **out of the repo**. Papers → journal DOI. Theses → **ETH Research Collection** record and/or **GitHub** repo, filled in **manually by Jakub** per thesis (some have both, some neither). Only small figures/result images are committed. |
| 7 | Thesis abstracts | **Concise, uniform, ~120 words** each, one neutral voice, written by reading each thesis. |
| 8 | Tag presentation | **Subtle pills** — soft neutral chip + tiny per-domain color dot — on project/thesis cards and detail pages. |
| 9 | Tag filtering | **Labels only**, no interactive filter bar. |

## Site map / navigation

Order via `nav_order`. Removed pages are deleted, not hidden.

1. **About** (`/`) — bio, photo, affiliation, socials, selected papers.
2. **Publications** (`/publications/`) — full bibliography, newest-first.
3. **Projects** (`/projects/`) — categorized cards: Jakub's projects + student theses.
4. **Repositories** (`/repositories/`) — "Developed" and "Supervised & co-developed" groups.
5. **CV** (`/cv/`) — from LinkedIn via JSONResume.
6. **Blog** (`/blog/`) — kept, emptied of demo posts.

> **Deploy prerequisite:** a GitHub *user* site is served only from a repo literally named
> `jaktk.github.io`. This repo is `personal-website`. Before publishing, either rename the
> repo to `jaktk.github.io` or attach a custom domain (CNAME). Config is written for the
> root/user-site case regardless.

## File-by-file plan

### Config & identity — `_config.yml`
- `first_name/middle_name/last_name` → `Jakub` / (blank) / `Tkaczuk`; `title` blank (uses full name).
- `url: https://jaktk.github.io`, `baseurl: ""`.
- `description`, `keywords` → cryogenics, thermodynamics, global health engineering, biogas, low-cost instrumentation.
- `icon` → an emoji favicon (proposed ❄️; swappable).
- `scholar.last_name: [Tkaczuk]`, `scholar.first_name: [Jakub, J.]` so jekyll-scholar bolds him.
- Collections: **remove** `teachings` and `books`; keep `projects`, `news` (feed disabled on homepage), `posts`. No new collection needed (decision #5).
- Remove Einstein leftovers: `disqus_shortname`, demo `external_sources`, Einstein-specific values.
- Exclude `resources/` from the build (add to `exclude:`), plus `.gitignore` it (decision #6).

### Socials — `_data/socials.yml`
- `email: jtkaczuk@ethz.ch`, `scholar_userid: _8Rm4lEAAAAJ`, GitHub `jaktk`, LinkedIn `jakubtkaczuk`.
- Remove `inspirehep_id` unless a personal InspireHEP author id is provided; remove Einstein `custom_social`.
- **ORCID:** `0000-0001-7997-9423` (rendered via the academicons ORCID icon).

### About — `_pages/about.md`
- `subtitle` → role + affiliation (e.g. "Senior Researcher, Global Health Engineering, ETH Zürich").
- `profile.image` ← `resources/pictures/profile-pic-square.png` (copied to `assets/img/prof_pic.jpg`, circular crop); `profile-pic-rectangular.jpeg` reserved for the CV / Open-Graph preview. `more_info` → ETH GHE address / contact.
- Body: first-person bio adapted from `linkedin-content.md` "About" + a short thread on the arc cryogenics → speech tech → global health engineering.
- `selected_papers: true`; `announcements.enabled: false`; `latest_posts.enabled: false` (until a post exists).

### Publications — `_bibliography/papers.bib`
Rebuild from the Scholar list. One BibTeX entry per work with:
- Correct authors (collaboration reports: first authors + `others` so "et al." renders; `max_author_limit: 3` already set).
- `preview` thumbnail from `resources/pictures/papers/*` (copied into `assets/img/publication_preview/`).
- `html`/`doi`/`url` → journal DOI or landing page (no committed PDFs).
- `selected={true}` on: 2020 *JPCRD* equations-of-state (`jpcrd-hene`), 2017 magnetic refrigeration, PhD dissertation, and one recent ETH paper.

Thumbnail ↔ paper map (images already provided):
`autocrime, fcc-ee, fcc-hh, fcc-physics, he-lhc, jpcrd-hene, magnetic-refrigeration, phd-thesis, policy-brief-cape-maclear, waste-bin-placement, willingness-to-pay`.

**De-duplication:** Several "CERN/ETH" Scholar entries are actually student technical reports
that also appear in the Theses showcase. Keep the genuine publications here (journal papers,
FCC/LHC collaboration reports, dissertation, policy brief, patent-pending) and represent the
student reports in Projects/Theses instead of duplicating them. (Confirm during the pass.)

### Projects collection — `_projects/*.md` + `_pages/projects.md`
- `_pages/projects.md`: `display_categories: [Cryogenics, Biogas, Air Quality, Organic Waste, Anthropogenic Waste]` (final taxonomy settled during the thesis read pass; an "Incineration" bucket may be added). `horizontal: false`, masonry on.
- Delete the 9 demo `_projects/*.md`.
- **Jakub's own project cards** (category `Cryogenics` / `Biogas`):
  - Magnetic Refrigeration feasibility for the FCC (img `magnetic-refrigeration`).
  - Cryogenic Moderator System for the ESS (img `cms-fat.png`; text from LinkedIn TU-Dresden role —
    thermal calcs, procurement, control-system design, FAT prep, redundant pressure control, APEX).
  - Equations of State for cryogenic mixtures (img `jpcrd-hene`).
  - Large pressure-drop Joule–Thomson coefficient measurements (img `jt-coefficient.png`).
  - Biogas flow & composition sensing (current ETH project + pending patent EP25224614) —
    **default:** image-light or reuse a neutral figure until a dedicated prototype photo is supplied.
- **Student thesis cards** — one `_projects/thesis-<student>.md` per thesis. Front matter:
  ```yaml
  title: <exact thesis title>
  description: <Degree> thesis · <Student full name> · <year>
  img: assets/img/projects/<student>.png   # result image (placeholder if not yet supplied)
  category: <theme>
  importance: <n>
  student: <full name>
  degree: BSc | MSc | Semester project
  year: <year>
  role: Supervisor            # or Co-supervisor, per title page
  eth_collection: <url or empty>    # ETH Research Collection record of the final thesis (Jakub fills manually)
  repo: <url or empty>              # GitHub repo, often Global-Health-Engineering (Jakub fills manually)
  tags: [<domain>, <method>, ...]   # from the tag vocabulary; assigned on read
  related_publications: false
  ```
  Body = the ~120-word abstract + the result figure + a "Supervised by Jakub Tkaczuk" note +
  whichever of the **ETH Research Collection** / **GitHub** links are present (rendered as two
  labelled buttons; card shows abstract + image only when neither is set).

### Thesis metadata + abstract generation (the 22)
Source: `resources/student_theses/**`. Process (implementation phase): fan out one lightweight
subagent per thesis; each reads the title page + Abstract + Conclusions pages and returns
`{student full name, degree (from filename prefix bsc/msc/sp), year (from title page), exact
title, theme, ~120-word abstract, whether Jakub is primary or co-supervisor}`. Results are
assembled into the `_projects/thesis-*.md` files. Provisional roster (titles/themes finalized
on read):

- **air-quality/** serena-loggia (MSc, bcMeter black-carbon monitor).
- **biogas/** luca-jakobs (MSc, continuous AD pasteurization plant, Malawi), jent-imelman (BSc,
  biogas-powered faecal-sludge pasteuriser), tim-luan-grimont (MSc, solar pasteurisation),
  recep-polat (MSc, solar pasteuriser), deniz-cinar (MSc, solar pasteuriser), elia-weber (MSc,
  biogas flow/composition sensor), flurin-vital (BSc), gianluca-lotti (MSc).
- **incineration/** mose-peduzzi (MSc, low-cost incinerator), raphael-bahisson (MSc, air-quality
  monitoring of open/incinerator burning), joel-kocher (Semester project, incineration guidelines).
- **(unsorted)** moreno-gabriel (BSc), dominic-waelti (MSc), emma-steinke (MSc, solar glass
  tumbler), fernand-braam (MSc), jonas-biner (MSc, black-soldier-fly larvae counter),
  josch-stricker (MSc), patrick-faessler (MSc), philippe-colbach (MSc, glass crusher),
  sven-prinz (MSc, sink-float plastic separator), teymour-dandrea (MSc).

Result images: **all 22 provided** in `resources/pictures/student_theses/` (one per student;
filenames encode topic + student). Copied into `assets/img/projects/` on build.

## Tagging system (decisions #8–9)

A cross-cutting topical vocabulary applied to **every publication, project, and thesis** — for
consistency, everything gets pills. **Categories** remain the page's section grouping; **tags**
are the finer labels rendered as **subtle pills** (neutral chip + tiny per-domain color dot),
**non-interactive** (labels only).

- **Domain tags:** `cryogenics` · `thermodynamics` · `biogas` · `sanitation` · `air quality` ·
  `organic waste` · `anthropogenic waste` · `water` (each maps to a color for the dot).
- **Method tags:** `mathematical modelling` · `optimization` · `equations of state` ·
  `sensing & instrumentation` · `prototyping / open hardware` · `field deployment` · `particle physics`.
- **Storage:** a `tags:` list in each `_projects/*.md` front matter; values assigned during the
  thesis/paper read pass.
- **Rendering (boundary-safe):** cards are rendered by a **content-level Liquid loop in
  `_pages/projects.md`** (not the gem's `projects.liquid` include) with a **self-contained
  `<style>` block** in the page for the pill/card styling. This keeps everything in starter-owned
  content — no `_includes`/`_layouts`/`_sass`/`assets/tailwind` files are created, so the
  `lint:style-contract` CI gate stays green. Detail-page pills reuse the same inline markup.
- **Publications pills (boundary-safe):** publications render through jekyll-scholar's gem-owned
  bib template, which we must **not** override (style contract). Instead, each bib entry carries
  its pills as inline HTML in the scholar **`additional_info`** field, styled by a `<style>`
  block in `_pages/publications.md`. Result: per-entry pills with **no template override and no
  JS**, contract stays green. *Fallback* if `additional_info` escapes the HTML: a small inline
  `<script>` in `publications.md` that appends pills to each entry keyed by citekey — still
  page-level content, no gem files. Confirm which path works during the build.

### Repositories — `_data/repositories.yml` + `_pages/repositories.md`
- `github_users: [jaktk]` (optionally the `Global-Health-Engineering` org).
- Render two labelled groups from `repos-to-showcase.md`: **Developed** (5) and
  **Supervised & co-developed** (16). Requires a small content-level edit to `repositories.md`
  to show two named lists (data keys `github_repos_developed` / `github_repos_supervised`).

### CV — `assets/json/resume.json` + `_pages/cv.md`
- `cv.md`: `cv_format: jsonresume`, `nav_order` after Repositories, drop the example PDF button
  (or point to a real CV PDF if supplied).
- Populate `resume.json` (JSONResume schema) from `linkedin-content.md`: `basics`, `work` (9
  roles), `education` (3), `certificates` (4), `skills`, `languages`, plus patent-pending under
  `awards`/`publications`. Delete Einstein `_data/cv.yml` (unused once on jsonresume).

### Blog
- Delete demo `_posts/*`. Keep `_pages/blog.md` and pagination. Homepage `latest_posts` stays
  off until a first post exists.

### Removals / cleanup
`_pages/teaching.md`, `_pages/books.md`, `_pages/dropdown.md`, `_pages/about_einstein.md`,
`_pages/profiles.md` (Einstein demo), `_teachings/`, `_books/`, demo `_news/*`, demo `_posts/*`,
demo `_projects/*`, `_data/cv.yml`. Purge Einstein strings from `_config.yml`.

## Repo hygiene
- `resources/` (theses + paper PDFs, ~650 MB) → add to `.gitignore` and `_config.yml` `exclude:`.
  It is the working source for extraction only; never built or committed.
- Commit only: paper preview thumbnails (→ `assets/img/publication_preview/`) and thesis result
  images (→ `assets/img/projects/`), all small PNGs.
- Move the prep files (`linkedin-content.md`, `projects-to-showcase.md`, `repos-to-showcase.md`,
  `claude_sessions.sh`) out of the build too (they're already excluded by not being in `_pages`,
  but confirm they don't get published; git-ignore or relocate to `resources/`).

## Assets — status
**Provided:** headshot (`profile-pic-square.png` + rectangular), CMS render (`cms-fat.png`),
Joule–Thomson figure (`jt-coefficient.png`), all 22 thesis result images, 12 paper thumbnails,
ORCID `0000-0001-7997-9423`.

**Still open (non-blocking; sensible defaults in place):**
1. **Own biogas-sensing prototype photo** — default is image-light until supplied.
2. **Thesis links** — Jakub adds **ETH Research Collection** + **GitHub** URLs manually per thesis
   (fields scaffolded in each card; some have both, some neither).
3. **CMS enrichment** — optional headline numbers (temp / cooling power / LH₂ inventory).
4. **Real CV PDF** (optional; otherwise the JSONResume page stands alone).
5. **InspireHEP author id** (optional).

## Validation
Per `al-folio-bootstrap` skill + AGENTS.md:
```
npm ci
npm run lint:prettier
bundle exec al-folio upgrade audit --no-fail
bundle exec jekyll build --baseurl ""      # user-site: root baseurl
```
Plus `npm run lint:style-contract` (must stay green — no starter-owned runtime added). Spot-check
the built `_site/` for: bolded author name in publications, category grouping on projects, two
repo groups, CV rendering, no Einstein strings, `resources/` absent from output.

## Open items / risks
- **Category taxonomy** finalizes only after reading the theses (some "unsorted" titles unknown).
- **Author lists** for the mega-collaboration reports are huge; enter a short prefix + `and others`.
- **Thesis links**: many theses may have no public URL → abstract + image only (acceptable).
- **Tailwind purge**: pill/card styling uses a self-contained `<style>` block in `projects.md`
  (not Tailwind utilities) to avoid depending on the gem's prebuilt/purged CSS.
- Publications de-duplication vs. the "All works" decision — keep genuine pubs; route student
  reports to Projects. Flag any the user wants shown in both.
