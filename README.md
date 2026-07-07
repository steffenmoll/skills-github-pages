# writing

Personal digital garden, built with [Jekyll](https://jekyllrb.com/) (using the [digital-garden-jekyll-template](https://github.com/maximevaillancourt/digital-garden-jekyll-template)) and hosted on [GitHub Pages](https://pages.github.com/).

Live at: https://steffenmoll.github.io/writing/

## Local development

```
bundle install
bundle exec jekyll serve
```

## Writing notes

Notes live in `_notes/`, and can be organized in subdirectories. Each note needs a `title` in its front matter:

```
---
title: "My note title"
---
```

Link between notes with double-bracket syntax, e.g. `[[my note title]]` or `[[my-note-filename]]`. Unresolved links are shown as greyed-out placeholders. Backlinks and a graph visualization are generated automatically.

Pages (like `about`) live in `_pages/`.

## Deployment

The site is built via the GitHub Actions workflow in `.github/workflows/pages.yml`, since the digital garden template relies on custom Jekyll plugins that aren't allowed by GitHub Pages' default build. In the repository's **Settings &rarr; Pages**, the source must be set to **GitHub Actions** (not "Deploy from a branch") for this to work.
