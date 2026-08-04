# Personal Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Turn the al-folio starter (Einstein demo content) into Jakub Tkaczuk's personal site — chronological Scholar publications, LinkedIn-derived About/CV, a tagged Projects + supervised-Theses showcase, curated repositories, and no demo content.

**Architecture:** Pure al-folio v1.x *content* customization — edit `_config.yml`, `_data/*`, `_pages/*`, `_bibliography/papers.bib`, `_projects/*`, and `assets/*`. **No** `_includes`/`_layouts`/`_sass`/`_scripts`/`assets/tailwind` files are created (keeps the `lint:style-contract` CI gate green). Tag pills and the Projects card grid are rendered by content-level Liquid + a self-contained `<style>` block inside the relevant `_pages/*` file.

**Tech Stack:** Jekyll + al-folio v1 gems (`al_folio_core`, `jekyll/scholar`, `al_citations`, `al_folio_cv`, `al_icons`), Ruby/Bundler, Node (prettier + style-contract), JSONResume.

## Global Constraints

- **Thin-starter boundary:** never create/modify `_includes`, `_layouts`, `_sass`, `_scripts`, `assets/tailwind`, `tailwind.config.js`, or add `build:css`/`build:tailwind` npm scripts. Keep `theme: al_folio_core` and the plugin list intact. (`npm run lint:style-contract` enforces this.)
- **Keep in `_config.yml`:** `al_folio.api_version: 1`, `style_engine: tailwind`, `tailwind.*`, `distill.*`, `third_party_libraries` SRI pins, the `al_math` Gemfile pin.
- **Hosting:** `url: https://jaktk.github.io`, `baseurl: ""` (root user site).
- **Name for jekyll-scholar bolding:** `scholar.last_name: [Tkaczuk]`, `scholar.first_name: [Jakub, J.]`. Scholar id `_8Rm4lEAAAAJ`. ORCID `0000-0001-7997-9423`.
- **Big source files stay out of the build:** `resources/` (≈650 MB) and the prep `*.md` files are git-ignored and excluded; only small images are copied into `assets/`.
- **Publications:** all Scholar works, newest-first, grouped by year, Jakub bolded, badges on; ~4 lead-author works `selected`.
- **Tags everywhere:** publications + projects + theses all get subtle pills (labels only, no filter bar).
- **Prettier:** `@shopify/prettier-plugin-liquid`, `printWidth: 150`. Run `npm run lint:prettier` before each commit that touches formatted files.
- **Build command (user site):** `bundle exec jekyll build --baseurl ""`.

---

## Tag vocabulary + color map

Domains carry a colored dot; methods use a neutral gray dot.

| Tag | Kind | Dot color |
|-----|------|-----------|
| cryogenics | domain | `#3b82f6` |
| thermodynamics | domain | `#6366f1` |
| biogas | domain | `#16a34a` |
| sanitation | domain | `#0d9488` |
| air quality | domain | `#64748b` |
| organic waste | domain | `#ca8a04` |
| anthropogenic waste | domain | `#ea580c` |
| water | domain | `#0ea5e9` |
| mathematical modelling | method | `#9ca3af` |
| optimization | method | `#9ca3af` |
| equations of state | method | `#9ca3af` |
| sensing & instrumentation | method | `#9ca3af` |
| prototyping / open hardware | method | `#9ca3af` |
| field deployment | method | `#9ca3af` |
| particle physics | method | `#9ca3af` |

## Reusable snippet A — pill `<style>` (theme-safe; used in `projects.md` and `publications.md`)

```html
<style>
  .tag-row { margin-top: .4rem; display: flex; flex-wrap: wrap; gap: .35rem; }
  .tag-pill {
    display: inline-flex; align-items: center; gap: .3rem;
    font-size: .72rem; line-height: 1; padding: .28rem .55rem;
    border-radius: 999px; background: rgba(127,127,127,.12);
    border: 1px solid rgba(127,127,127,.28); color: inherit; white-space: nowrap;
  }
  .tag-dot { width: .5rem; height: .5rem; border-radius: 50%; background: #9ca3af; flex: 0 0 auto; }
</style>
```

Each pill: `<span class="tag-pill"><span class="tag-dot" style="background:#16a34a"></span>biogas</span>`.

## Reusable snippet B — project/thesis card front-matter templates

Own project (`_projects/cryo-magnetic-refrigeration.md` etc.):
```yaml
---
layout: page
title: Magnetic refrigeration for the FCC
description: Feasibility study of 1.6 K superfluid-helium magnetic refrigeration
img: assets/img/projects/magnetic-refrigeration.png
importance: 1
category: Cryogenics
tags: [cryogenics, thermodynamics, mathematical modelling]
related_publications: true
---
```

Student thesis (`_projects/thesis-<student>.md`):
```yaml
---
layout: page
title: <exact thesis title>
description: <MSc> thesis · <Full Name> · <year>
img: assets/img/projects/<image-basename>.png
importance: <n>
category: <Biogas|Air Quality|Organic Waste|Anthropogenic Waste|Cryogenics>
student: <Full Name>
degree: <BSc|MSc|Semester project>
year: <year>
role: <Supervisor|Co-supervisor>
eth_collection:            # ETH Research Collection URL — Jakub fills manually
repo:                      # GitHub URL — Jakub fills manually
tags: [<domain>, <method>, ...]
related_publications: false
---
<~120-word abstract>

<!-- links rendered from eth_collection / repo when present -->
```

---

## File structure (created / modified)

- **Modify** `_config.yml` — identity, hosting, scholar, collections, excludes, purge Einstein.
- **Modify** `_data/socials.yml` — real socials + ORCID.
- **Rewrite** `_pages/about.md` — bio + profile.
- **Rewrite** `_pages/publications.md` — add pill `<style>` above `{% bibliography %}`.
- **Rewrite** `_bibliography/papers.bib` — all Scholar works with previews, DOIs, `selected`, pills via `additional_info`.
- **Rewrite** `_pages/projects.md` — `display_categories`, custom card grid loop, card+pill `<style>`.
- **Create** `_projects/cryo-*.md` (4) + `_projects/biogas-sensing.md` (1) + `_projects/thesis-*.md` (22).
- **Modify** `_data/repositories.yml` + **rewrite** `_pages/repositories.md` — two labelled groups.
- **Rewrite** `assets/json/resume.json` + **modify** `_pages/cv.md` — CV from LinkedIn.
- **Copy** images → `assets/img/publication_preview/`, `assets/img/projects/`, `assets/img/prof_pic.jpg`.
- **Add** `.gitignore` entries; **modify** `_config.yml` `exclude:`.
- **Delete** demo/Einstein content.

---

## Task 1: Repo hygiene + config identity

**Files:** Modify `.gitignore`, `_config.yml`.

- [ ] **Step 1 — git-ignore big inputs.** Append to `.gitignore`:
```
# working inputs, not part of the site
resources/
linkedin-content.md
projects-to-showcase.md
repos-to-showcase.md
claude_sessions.sh
```
- [ ] **Step 2 — `_config.yml` identity.** Set `first_name: Jakub`, `middle_name: ""`, `last_name: Tkaczuk`, `title: blank`. Replace `contact_note`, `description` (cryogenics · thermodynamics · global health engineering · biogas · low-cost instrumentation), `keywords`, `footer_text` (drop the al-folio boilerplate credit if desired — keep the Jekyll/al-folio attribution per license), `icon: ❄️`.
- [ ] **Step 3 — hosting.** `url: https://jaktk.github.io`, `baseurl: ""`.
- [ ] **Step 4 — scholar.** `scholar.last_name: [Tkaczuk]`, `scholar.first_name: [Jakub, J.]`.
- [ ] **Step 5 — collections.** Remove the `teachings` and `books` collection blocks; keep `news`, `projects`.
- [ ] **Step 6 — excludes.** Add to `exclude:`: `resources/`, `linkedin-content.md`, `projects-to-showcase.md`, `repos-to-showcase.md`, `claude_sessions.sh`, `docs/superpowers/`.
- [ ] **Step 7 — purge Einstein.** Remove/blank `disqus_shortname`, the demo `external_sources` entries (medium/google), and any Einstein-specific values.
- [ ] **Step 8 — build.** Run `bundle exec jekyll build --baseurl ""`. Expected: build succeeds. `grep -ri einstein _config.yml` → no matches.
- [ ] **Step 9 — commit.** `git add -A && git commit -m "chore: site identity + config for jaktk.github.io"`

## Task 2: Remove demo & Einstein content

**Files:** Delete demo pages/collections/data.

- [ ] **Step 1 — delete pages:** `_pages/teaching.md`, `_pages/books.md`, `_pages/dropdown.md`, `_pages/about_einstein.md`, `_pages/profiles.md`.
- [ ] **Step 2 — delete collections/dirs:** `_teachings/`, `_books/`, all demo `_projects/*.md` (1–9), demo `_news/announcement_*.md`, demo `_posts/*`.
- [ ] **Step 3 — delete data:** `_data/cv.yml` (Einstein; JSONResume replaces it).
- [ ] **Step 4 — build.** `bundle exec jekyll build --baseurl ""` succeeds; `grep -rli einstein _site | grep -v resources` → empty.
- [ ] **Step 5 — commit.** `git commit -am "chore: remove al-folio demo and Einstein content"`

## Task 3: Copy images into the build

**Files:** Create `assets/img/publication_preview/*`, `assets/img/projects/*`, `assets/img/prof_pic.jpg`.

- [ ] **Step 1 — profile pic.** Copy `resources/pictures/profile-pic-square.png` → `assets/img/prof_pic.jpg` (keep `.jpg` name that about.md references; a PNG renamed `.jpg` is fine for browsers, but prefer `magick convert` to real jpg if ImageMagick present). Copy `resources/pictures/profile-pic-rectangular.jpeg` → `assets/img/prof_pic_rect.jpg`.
- [ ] **Step 2 — paper thumbnails.** `mkdir -p assets/img/publication_preview` and copy all `resources/pictures/papers/*.png` there (keep basenames).
- [ ] **Step 3 — project/thesis images.** `mkdir -p assets/img/projects`; copy all `resources/pictures/student_theses/*.png` and the own-project figures (`magnetic-refrigeration.png`, `jpcrd-hene.png`, `cms-fat.png`, `jt-coefficient.png`) into `assets/img/projects/`.
- [ ] **Step 4 — remove Einstein prof pics** (`assets/img/prof_pic_color.png` if unused).
- [ ] **Step 5 — build & commit.** Build succeeds; `git add assets/img && git commit -m "assets: add profile, publication, and project images"`.

## Task 4: Socials + About page

**Files:** Modify `_data/socials.yml`, `_pages/about.md`.

- [ ] **Step 1 — socials.yml.** Set `email: jtkaczuk@ethz.ch`, `scholar_userid: _8Rm4lEAAAAJ`, `orcid_id: 0000-0001-7997-9423`, `github_username: jaktk`, `linkedin_username: jakubtkaczuk`. Remove `inspirehep_id` (no personal author page) and the Einstein `custom_social`; set `cv_pdf:` empty (or a real CV pdf if supplied).
- [ ] **Step 2 — about front matter.** `subtitle:` → "Senior Researcher · Global Health Engineering, ETH Zürich · cryogenics → global health engineering". `profile.image: prof_pic.jpg`, `image_circular: true`, `more_info:` → ETH GHE, Zürich + contact. `selected_papers: true`, `announcements.enabled: false`, `latest_posts.enabled: false`.
- [ ] **Step 3 — about body.** Rewrite (first person) from `linkedin-content.md` "About": the arc from cryogenics (FCC magnetic refrigeration, ESS cryogenic moderator, PhD equations of state at CEA/NIST) through speech tech (Idiap/ROXANNE) to leading biogas sensing & low-cost engineering for global health at ETH; mention supervising ~50 theses and the CC-BY open-hardware policy. ~150–200 words.
- [ ] **Step 4 — build & verify.** Build succeeds; About renders photo + socials + selected papers (once bib exists). No lorem/einstein text.
- [ ] **Step 5 — prettier + commit.** `npm run lint:prettier -- --write _pages/about.md _data/socials.yml`; `git commit -am "feat: about page + socials"`.

## Task 5: Publications bibliography

**Files:** Rewrite `_bibliography/papers.bib`, modify `_pages/publications.md`.

**Scholar → bib source of truth** (all works; newest first is handled by config `group_order: descending`). Enter each with `title`, `author` (collaboration reports: 3–4 names + `and others`), `journal/booktitle`, `year`, `doi`/`url`/`html`, `preview` (thumbnail basename in `assets/img/publication_preview/`), `abbr` (venue), and `additional_info` pills (snippet C). Mark `selected={true}` on: `tkaczuk2020eos` (JPCRD), `tkaczuk2017magnetic`, `tkaczuk2021phdthesis`, and one recent ETH paper (`abgottspon2025willingness` or `schweizer2026wastebin`).

Preview map: `jpcrd-hene`→EoS mixtures 2020; `magnetic-refrigeration`→2017; `phd-thesis`→2021 dissertation; `fcc-ee`,`fcc-hh`,`fcc-physics`,`he-lhc`→collaboration reports 2019; `autocrime`→Autocrime 2025; `waste-bin-placement`→2026; `willingness-to-pay`→2025; `policy-brief-cape-maclear`→policy brief.

**Snippet C — `additional_info` pills (single line, no line breaks):**
```
additional_info = {<span class="tag-row"><span class="tag-pill"><span class="tag-dot" style="background:#3b82f6"></span>cryogenics</span><span class="tag-pill"><span class="tag-dot" style="background:#9ca3af"></span>equations of state</span></span>},
```

- [ ] **Step 1 — write `papers.bib`** with all Scholar entries per the map above; add `additional_info` pills per entry using the tag vocabulary; DOIs looked up from each landing page (no committed PDFs). Remove all Einstein entries.
- [ ] **Step 2 — publications.md `<style>`.** Insert snippet A `<style>` block above `{% include bib_search.liquid %}`.
- [ ] **Step 3 — build & verify.** Build succeeds. Open `_site/publications/`: Jakub's name is **bold**; thumbnails show; entries grouped by year descending; **pills render** under entries; citation badges present. If `additional_info` HTML is escaped, apply the fallback JS (snippet D) in `publications.md` keyed by citekey and rebuild.
- [ ] **Step 4 — prettier (skip .bib) + commit.** `git commit -am "feat: publications from Google Scholar with tag pills"`.

**Snippet D — fallback pill injector (only if Step 3 shows escaped HTML):** a `<script>` in `publications.md` holding `{citekey: [["biogas","#16a34a"],...]}` that, on `DOMContentLoaded`, finds each `li[id]` in `.bibliography` and appends a `.tag-row`.

## Task 6: Own project cards

**Files:** Create `_projects/cryo-magnetic-refrigeration.md`, `cryo-moderator-ess.md`, `cryo-eos-mixtures.md`, `cryo-joule-thomson.md`, `biogas-sensing.md`.

- [ ] **Step 1 — create the 5 cards** using snippet B (own-project template). Categories: first four `Cryogenics`, last `Biogas`. Images: `magnetic-refrigeration`, `cms-fat`, `jpcrd-hene`, `jt-coefficient`, (biogas-sensing image-light or reuse). Bodies: 100–150 words each from LinkedIn (CMS from the TU-Dresden paragraph; biogas-sensing notes patent EP25224614). `importance` 1–5. Tags per vocabulary (e.g. magnetic-refrigeration → `[cryogenics, thermodynamics, mathematical modelling]`; EoS → `[cryogenics, thermodynamics, equations of state, optimization]`; CMS → `[cryogenics, thermodynamics, prototyping / open hardware]`; JT → `[cryogenics, equations of state, sensing & instrumentation]`; biogas-sensing → `[biogas, sensing & instrumentation, prototyping / open hardware, field deployment]`).
- [ ] **Step 2 — build & commit.** Build succeeds; `git add _projects && git commit -m "feat: own project cards (cryogenics + biogas sensing)"`.

## Task 7: Thesis read-pass + 22 thesis cards

**Files:** Create `_projects/thesis-*.md` (22).

- [ ] **Step 1 — dispatch parallel read-pass.** One subagent per thesis PDF under `resources/student_theses/**`. Each returns strict JSON: `{ student_full_name, degree (BSc|MSc|Semester project — from filename prefix bsc/msc/sp), year (from title page), exact_title, category (one of Biogas|Air Quality|Organic Waste|Anthropogenic Waste|Cryogenics), tags (2–4 from the vocabulary), abstract (~120 words, neutral third person, objective→method→result), role (Supervisor|Co-supervisor — Jakub primary vs Prof. Tilley primary on title page) }`. Give each agent the tag vocabulary + category list + image basename.
- [ ] **Step 2 — assemble 22 cards** with snippet B (thesis template); `img` = matching `assets/img/projects/<basename>.png` (see image↔student map below); leave `eth_collection`/`repo` blank for Jakub. Order `importance` within each category (newest first).
- [ ] **Step 3 — build & verify.** Build succeeds; 22 thesis pages exist; each shows abstract + image + pills + student credit.
- [ ] **Step 4 — commit.** `git add _projects && git commit -m "feat: 22 supervised-thesis showcase cards"`.

**Image ↔ student map:** `black-carbon-serena-loggia`, `biogas-pasteurizer-luca-jakobs`, `biogas-pasteurizer-jent-imelman`, `solar-pasteurizer-tim-luan-grimont`, `solar-pasteurizer-recep-polat`, `solar-pasteurizer-deniz-cinar`, `solar-pasteurizer-gianluca-lotti`, `biogas-sensor-elia-weber`, `h2s-sensor-flurin-vital`, `incineration-mose-peduzzi`, `incineration-raphael-bahisson`, `incineration-joel-kocher`, `3dplam-moreno-gabriel`, `tipping-aid-dominic-waelti`, `glass-emma-steinke`, `water-cooling-fernand-braam`, `jonas-biner-bsf-counting`, `waste-collection-josch-stricker`, `patrick-faessler-bike-charging`, `glass-philippe-colbach`, `sven-prinz-plastic-separation`, `uddt-teymour-dandrea`.

## Task 8: Projects page — custom grid + pills

**Files:** Rewrite `_pages/projects.md`.

- [ ] **Step 1 — front matter.** `display_categories: [Cryogenics, Biogas, Air Quality, Organic Waste, Anthropogenic Waste]`, `horizontal: false`.
- [ ] **Step 2 — body.** Add snippet A `<style>` + card `<style>` (grid, card, image, title, meta line). Replace the `{% include projects.liquid %}` calls with an inline Liquid loop: for each category, header + a responsive grid of cards; each card renders `project.img` (via `figure.liquid` or plain `<img>` with `relative_url`), title (link to the project page), the `description`/student-meta line, and a `.tag-row` of pills built from `project.tags` (dot color via a Liquid `case`/`assign` mapping the tag→color from the table). Group by `category`, sort by `importance`.
- [ ] **Step 3 — build & verify.** Build succeeds; `/projects/` shows all categories, cards, images, and pills; student cards show name + degree + year; layout responsive (no horizontal page scroll).
- [ ] **Step 4 — prettier + commit.** `npm run lint:prettier -- --write _pages/projects.md`; `git commit -am "feat: projects+theses showcase grid with tag pills"`.

## Task 9: Repositories page — two groups

**Files:** Modify `_data/repositories.yml`, rewrite `_pages/repositories.md`.

- [ ] **Step 1 — data.** `github_users: [jaktk]`; add `github_repos_developed:` (5 from repos-to-showcase "Developed") and `github_repos_supervised:` (16 from "Supervised and co-developed"). Keep `repo_description_lines_max`.
- [ ] **Step 2 — page.** Rewrite `_pages/repositories.md` to render two `## Developed` / `## Supervised & co-developed` sections, each looping its list with `{% include repository/repo.liquid repository=repo %}` (gem include — allowed to *use*, not override). Keep the `github_users` block for the profile card + trophies.
- [ ] **Step 3 — build & commit.** Build succeeds; both groups render; `git commit -am "feat: repositories page with developed/supervised groups"`.

## Task 10: CV — JSONResume from LinkedIn

**Files:** Rewrite `assets/json/resume.json`, modify `_pages/cv.md`.

- [ ] **Step 1 — resume.json.** Populate JSONResume schema from `linkedin-content.md`: `basics` (name, label "Senior Researcher / Engineer", email, url, ORCID profile, location Zürich, summary), `work` (9 roles with dates + highlights), `education` (3, with thesis links to Zenodo), `certificates` (4), `skills`, `languages` (Polish native, English full, French professional, German basic), and the pending patent EP25224614 under `awards` or `publications`. Remove all Einstein data.
- [ ] **Step 2 — cv.md.** Confirm `cv_format: jsonresume`; set `nav_order` after Repositories; remove the example `cv_pdf` button (or point to a real CV pdf).
- [ ] **Step 3 — build & verify.** Build succeeds; `/cv/` renders experience/education/skills; no Einstein.
- [ ] **Step 4 — commit.** `git commit -am "feat: CV from LinkedIn via JSONResume"`.

## Task 11: Blog + homepage tidy

**Files:** `_pages/blog.md`, confirm homepage flags.

- [ ] **Step 1 — blog empty state.** Ensure no demo posts remain; `_pages/blog.md` intact. Since blog is empty, homepage `latest_posts.enabled: false` (set in Task 4) prevents an empty section.
- [ ] **Step 2 — nav order.** Verify nav order across pages: About(0/home), Publications(1), Projects(2), Repositories(3), CV(4). Adjust `nav_order` front matter as needed. Blog appears via its own nav.
- [ ] **Step 3 — build & commit.** Build succeeds; nav correct; `git commit -am "chore: blog/homepage tidy + nav order"`.

## Task 12: Full validation

**Files:** none (fixes as needed).

- [ ] **Step 1 — prettier.** `npm run lint:prettier` → passes (run `--write` then re-check).
- [ ] **Step 2 — style contract.** `npm run lint:style-contract` → passes (proves no starter-owned runtime added).
- [ ] **Step 3 — upgrade audit.** `bundle exec al-folio upgrade audit --no-fail` → review output.
- [ ] **Step 4 — final build.** `bundle exec jekyll build --baseurl ""` → clean.
- [ ] **Step 5 — spot-check `_site/`:** bolded author in publications; pills on publications + projects; 5 own + 22 thesis cards across 5 categories; two repo groups; CV renders; `resources/` absent from `_site`; no "einstein"/"lorem" anywhere.
- [ ] **Step 6 — commit.** `git commit -am "chore: pass prettier, style-contract, and build validation"`.

---

## Self-review notes
- **Spec coverage:** identity/config (T1), removals (T2), images (T3), about+socials (T4), publications+pills (T5), own projects (T6), theses (T7), projects grid (T8), repos (T9), CV (T10), blog (T11), validation (T12) — every spec section maps to a task.
- **Boundary:** T5/T8 render pills via page `<style>` + content Liquid; no gem-file creation → style contract safe (verified in T12).
- **Deferred-by-design:** exact thesis titles/categories/abstracts produced by the T7 read-pass; thesis `eth_collection`/`repo` links filled by Jakub later.
- **Deploy note (out of plan scope):** repo must be renamed `jaktk.github.io` (or custom domain) for the user-site URL to serve at root.
