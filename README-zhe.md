# Editing this site — cheat-sheet

Built on [al-folio](https://github.com/alshedivat/al-folio) v1.x (Jekyll). Everything you normally touch is plain Markdown/YAML; layouts and styles live in the `al_folio_*` gems, so you rarely need to touch them. Before changing anything structural, read `AGENTS.md` (the template's rules).

## Preview locally

```bash
export PATH="/opt/homebrew/opt/ruby/bin:$PATH"   # Homebrew Ruby (system Ruby 2.6 is too old)
bundle install                                    # first time only
bundle exec jekyll serve --livereload             # → http://localhost:4000
```

Edits to `_config.yml` need a server restart; everything else reloads automatically.

## Write a blog post

Create `_posts/YYYY-MM-DD-short-slug.md`:

```yaml
---
layout: post
title: My idea about X
date: 2026-11-02
description: one-line teaser shown in the blog list
tags: decomposition optimization # space-separated
categories: research-notes # or: explainers
related_publications: true # needed if you use {% cite key %}
toc:
  sidebar: left # optional table of contents
mermaid:
  enabled: true # optional diagrams
---
```

- **Math:** `$$ x^\top Q x $$` (inline or display), `\begin{equation}…\end{equation}` with `\label`/`\eqref`.
- **Cite your papers:** `{% cite li2025learning %}`; keys are in `_bibliography/papers.bib`.
- **Images:** put files in `assets/img/` and use `{% include figure.liquid path="assets/img/foo.png" class="img-fluid rounded" %}`.
- **Jupyter notebooks:** put the `.ipynb` in `assets/jupyter/` and use `{::nomarkdown}{% jupyter_notebook "/assets/jupyter/foo.ipynb" %}{:/nomarkdown}`.
- **Drafts:** add `published: false` to the front matter to keep a post off the live site.
- **Link two posts:** `[text]({% post_url 2026-10-13-why-learn-to-control-benders %})`.

Worked examples of every feature (math, Distill-style articles, notebooks, charts, pseudocode, tabs, citations, TikZ, …) are in `docs/post-examples/`. They are not built; copy one into `_posts/` to try it out.

## Research page

`_pages/research.md` is a single long-form page for your research story. It supports the same Markdown, math, figures and `{% cite key %}` citations as blog posts, and once you cite something, set `related_publications: true` in its front matter to get a reference list at the bottom. To cite other people's work (e.g. Bertsekas, Powell, LeCun), add their BibTeX entries to `_bibliography/papers.bib` too, but note those will then also show up on your publications page. If you'd rather keep them separate, ask Claude to set up a second `.bib` file.

## Model gallery

The model gallery is at `/gallery/`. Each model has a page in `_models/`, its notebook copy in `assets/jupyter/gallery/`, and a 4:3 thumbnail in `assets/img/gallery/`. The site renders the notebooks as they are and never runs them.

To add a model:

1. Copy the `.ipynb` into `assets/jupyter/gallery/`.
2. Copy one of the `_models/*.md` files and edit its `title`, `description`, `img`, `github` and notebook path. `importance` sets the card order.

The notebook copies are separate from the [Model-Gallery repo](https://github.com/BambooSticker/Model-Gallery). If you update a notebook there, copy it here again. Two site copies differ slightly from the originals so their math renders:

- `benders_mpc.ipynb`: `\R` was replaced with `\mathbb{R}`.
- `dual_partition_2slp.ipynb`: `bmatrix*` was replaced with `bmatrix`.

## Add a paper

Add a BibTeX entry to `_bibliography/papers.bib`. The extra fields shown on the site are:

- `abbr` sets the venue badge; colors and links come from `_data/venues.yml`.
- `selected = {true}` marks a paper as selected (shown on About only if `selected_papers: true` in `_pages/about.md`; currently off).
- `html`, `pdf`, `code`, `arxiv`, `slides`, `poster` add buttons. A `pdf` file name is looked up in `assets/pdf/`.
- `abstract` adds an "Abs" button, and `bibtex_show = {true}` adds a "Bib" button.

Only post a PDF if you're allowed to: for most journals that means the preprint or accepted manuscript, not the publisher's typeset version. Coauthor homepages are linked via `_data/coauthors.yml`.

## Add a favorite paper

Add a BibTeX entry to `_bibliography/favorites.bib`. These show on `/favorite-papers/`, not on the publications page. Set `keywords` to `optimization`, `learning` or `control` to pick the section; an entry without one of these won't show. Optionally add `note = {…}` for a line under the entry (e.g. why you like it). Add a `doi`, or an `html` link if there's no DOI.

## Add a news item

Create `_news/YYYY-MM-DD-slug.md` with `layout: post`, `date:`, and `inline: true`, followed by a single line of text.

## Other things you might change

| What | Where |
| --- | --- |
| Bio, research questions | `_pages/about.md` |
| Photo | replace `assets/img/prof_pic.jpg` |
| Tab icon (favicon) | `icon:` and `apple_touch_icon:` in `_config.yml`; images in `assets/img/` (Squirtle: Emerald sprite, scaled 4× with nearest-neighbor) |
| Email/GitHub/Scholar/LinkedIn icons | `_data/socials.yml` |
| Nav order | `nav_order:` in each `_pages/*.md` |
| Blog comments | fill `giscus:` in `_config.yml` (see giscus.app) |

## Deploy

Pushing to `main` on `BambooSticker/bamboosticker.github.io` triggers the "Deploy site" GitHub Action, which builds into the `gh-pages` branch. To set this up the first time:

1. Under **Settings → Actions → General → Workflow permissions**, select **Read and write**.
2. Under **Settings → Pages**, choose **Deploy from a branch** and select `gh-pages`.
