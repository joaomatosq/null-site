# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Static website for the band **null** (Instagram: @nullgaze), served at `www.nullgaze.com` (see `CNAME`) via GitHub Pages. Plain HTML + one shared CSS file — no build tooling, package manager, JavaScript, or tests.

## Development

- Preview: open `index.html` directly in a browser, or serve the folder with any static server (e.g. `python -m http.server`).
- CI: `.github/workflows/jekyll-docker.yml` runs `jekyll build --future` in the `jekyll/builder` Docker image on pushes/PRs to `main`. It only checks that the site builds; there is no Jekyll config or templating in use.

## Structure

- `index.html` — landing page: band name + `.links` nav to the subpages (Tour, Music, Merch, Midia).
- `tour.html` — shows, each one a boxed `<a>` button:
  - `.buy-link2` — upcoming show (plain box).
  - `.buy-link` — rendered with `text-decoration: line-through`, used for shows that already happened; their Sympla ticket `href`s were removed.
- `music.html` — current setlist; each song is an `<h1 class="musics">` numbered by hand.
- `merch.html` — placeholder ("Soon...").
- `social_media.html` — social links page linked as "Midia" from the home nav; back-link + a `.buy-link2` box per social profile (currently Instagram).
- `style.css` — all styling, shared by every page.
- `assets/Leche de Mipalo.gif` — full-screen background GIF (referenced from `style.css` with an escaped space).

Every page repeats the same `<head>` (Poppins from Google Fonts + `style.css`) and the same skeleton: `<div class="glitch-bg"></div>` followed by `<main class="content">`. Subpages start with `<a href="index.html" class="back-link">null</a>`. There are no includes/partials, so a change to the shared head or layout — or a new nav entry — must be made in each relevant HTML file by hand.

## Conventions and gotchas

- Content and the `lang` attribute are Brazilian Portuguese (`pt-br`); CSS comments are in Portuguese too. Text is styled lowercase via CSS.
- `body` has `overflow: hidden` and `.content` is a fixed `100vh` flex column centered vertically, so pages cannot scroll — adding many shows or songs will clip content off-screen unless the layout changes.
- Typical edits are content updates: adding/retiring shows in `tour.html` and reordering the setlist in `music.html`.
