# Setup notes for this skeleton

This is the [al-folio](https://github.com/alshedivat/al-folio) Jekyll theme, trimmed down to
the sections you asked for: **about, publications, talks, gallery, cv, contact**.
Blog, teaching, and research-group pages from the default theme were removed.

## What was changed from stock al-folio

- **`_config.yml`** — `title`/`first_name`/`last_name` set to Millend Roy, `url` set to
  `https://millendroy.github.io`, `baseurl` cleared (this is a GitHub *user* page, served
  from the repo root, not a project page under a subpath).
- **`_pages/about.md`** — subtitle/affiliation filled in, announcements & latest-posts
  disabled (no blog), bio left with a `TODO` for you to expand.
- **`_pages/publications.md`** — untouched. It auto-renders `_bibliography/papers.bib` —
  replace the example entries with your own BibTeX.
- **`_pages/talks.md`** *(new)* — loops over `_data/talks.yml`. Add one YAML entry per talk.
- **`_pages/gallery.md`** *(renamed from `projects.md`)* — same underlying `_projects/`
  collection and grid layout, repointed to `/gallery/` with categories renamed to
  `sketches` / `paintings`. Add one file per artwork in `_projects/` (see the two samples).
- **`_pages/cv.md`** — points at `assets/pdf/CV.pdf` (drop your CV there, or swap in an
  external link).
- **`_pages/contact.md`** *(new)* — hand-written email + social links pulled from
  `_data/socials.yml`, since the exact social-icon include name lives inside the
  `al_folio_core` gem and wasn't visible from this repo to verify. Swap in the theme's
  own include once you confirm its name (see `docs/CUSTOMIZE.md`).
- **`_data/socials.yml`** — email and a few usernames filled in from your old site
  (GitHub, LinkedIn, Twitter, Google Scholar ID). Double-check the key names this theme
  version expects — the plugin is `jekyll-socials`.
- Removed unused demo content to keep the repo light: `_posts`, `_news`, `_books`,
  `_teachings`, and their pages; `test/`, `lighthouse_results/`, `readme_preview/`,
  `docs/releases/`; and unused demo media (`assets/video`, `assets/plotly`,
  `assets/audio`, `assets/jupyter`, `assets/html`) that only the removed blog posts used.

## What still needs your content

- `_pages/about.md` — full bio, past experience, education.
- `_bibliography/papers.bib` — your publications (BibTeX).
- `_data/talks.yml` — your talks (currently one placeholder entry).
- `_projects/*.md` — your sketches/paintings (currently two placeholder entries).
- `_data/cv.yml` — your CV content (or drop a PDF at `assets/pdf/CV.pdf`).
- `assets/img/prof_pic.jpg` — replace with your own photo.
- `_data/socials.yml` — confirm the keys against `jekyll-socials` docs and add ResearchGate/
  YouTube if you want them (may need a `custom_social` entry — see the comments in that file).

## Running it locally

```bash
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`. Full install instructions (including Docker, which
avoids needing Ruby installed) are in `docs/INSTALL.md`; theme customization details are
in `docs/CUSTOMIZE.md`.

## Deploying to GitHub Pages

Since `millendroy.github.io` is already a GitHub *user* page, you can push this directly
to that repo's default branch (replacing its current contents) and GitHub Pages will build
it automatically via the theme's included GitHub Action — no separate `gh-pages` branch
needed. Double check `docs/INSTALL.md` for the current recommended deploy workflow, since
al-folio's setup has changed over theme versions.
