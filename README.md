# website-eturkes-origin

Personal academic website for [eturkes.com](https://eturkes.com/), built with [Hugo](https://gohugo.io/) using a fork of the [Origin](https://github.com/eturkes/origin-hugo-theme) theme.

## Prerequisites

- [Hugo](https://gohugo.io/installation/) (extended edition, for SCSS support)
- Git

## Setup

```sh
git clone --recurse-submodules git@github.com:eturkes/website-eturkes-origin.git
cd website-eturkes-origin
```

If you already cloned without `--recurse-submodules`:

```sh
git submodule update --init
```

Create the required `env.js` for the Get Started page:

```sh
cp static/get-started/env.js.example static/get-started/env.js
```

## Development

Start the local dev server:

```sh
hugo server
```

The site will be available at `http://localhost:1313/` with live reload.

Build the static site to `public/`:

```sh
hugo
```

## Project Structure

```
.
├── archetypes/
│   └── default.md          # Template for new content
├── content/
│   ├── about.md            # About page
│   └── post/               # Publications (blog-style posts)
│       ├── _index.md       # Section title ("Publications")
│       └── *.md            # Individual publication entries
├── static/
│   ├── favicon-32.png      # Site favicon
│   ├── pubs.bib            # BibTeX bibliography
│   ├── get-started/               # AI assistant setup tool (git submodule)
│   └── media/
│       ├── avatar.jpg
│       ├── emir-turkes-cv.pdf
│       ├── genefunnel-manuscript/   # PDF viewer page + manuscript
│       ├── masters-thesis/          # PDF viewer page + thesis
│       └── phd-thesis/              # PDF viewer page + thesis
├── themes/
│   └── origin/             # Theme (git submodule)
├── hugo.toml               # Site configuration
└── LICENSE                 # MIT
```

## Configuration

All site configuration is in `hugo.toml`:

- **`baseURL`** — Production URL (`https://eturkes.com/`)
- **`title`** — Site-wide title shown in the header
- **`copyright`** — Footer copyright text
- **`[params]`**
  - `description` — Tagline displayed below the title
  - `featured` — `true` to show the 3 most recent posts as featured cards on the homepage
- **`[params.socials]`** — Social links rendered in the footer (supports `x`, `github`, `linkedin`, and others defined by the theme)
- **`[menu.main]`** — Top navigation items (Home, About, Publications, Get Started, CV)
- **`[markup.goldmark.renderer]`** — `unsafe = true` allows raw HTML in Markdown content

## Adding Content

### New publication

```sh
hugo new post/author-year-keyword.md
```

Edit the generated file. Front matter fields used by the theme:

```toml
+++
title = "Full publication title"
date = "2025-01-01"
description = "Journal — Author list"
tags = ["neuroscience", "bioinformatics"]
+++
```

Post body typically includes authors, journal info, a DOI link, and an optional abstract. Also add a corresponding BibTeX entry to `static/pubs.bib`.

### PDF viewer pages

Documents under `static/media/` use lightweight `index.html` wrappers that embed PDFs via [PDF.js](https://mozilla.github.io/pdf.js/):

```html
<!doctype html>
<meta charset="utf-8">
<title>Document Title — Emir Turkes</title>
<style>html,body,iframe{height:100%;margin:0;width:100%;border:0}</style>
<iframe src="/pdfjs/web/viewer.html?file=%2Fmedia%2Fpath%2Fto%2Ffile.pdf#zoom=page-fit"></iframe>
```

## Theme

The site uses a [personal fork](https://github.com/eturkes/origin-hugo-theme) of the Origin Hugo theme, included as a git submodule at `themes/origin/`. Key theme features:

- SCSS-based styling (compiled by Hugo Pipes)
- Featured post cards on the homepage
- Responsive mobile navigation
- Social media icon links in the footer
- Optional JS-free mode (`params.cssonly = true`)

To update submodules:

```sh
git submodule update --remote themes/origin
git submodule update --remote static/get-started
```

## License

[MIT](LICENSE)
