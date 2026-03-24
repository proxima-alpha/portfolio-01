# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static portfolio website deployed to GitHub Pages via Jekyll. No build step required — open `index.html` directly in a browser for local development. Changes pushed to `master` automatically deploy via GitHub Actions.

**Live URL:** https://proxima2182.github.io/portfolio-01/

## Development

No package manager or build tools. To preview locally, open `index.html` in a browser. Deployment is automatic on push to `master`.

## Architecture

**Data-driven UI:** All portfolio content (projects, skills, bio) lives in XML files under `meta/`. JavaScript reads these at runtime to render the UI — editing content means editing XML, not HTML.

- `meta/project_list.xml` — project portfolio entries
- `meta/skill_list.xml` — skills with proficiency levels (1–3)
- `meta/popup_about.xml` — bio, work history, education

**JS responsibilities:**
- `js/map.js` — parses XML and creates DOM elements (core rendering engine)
- `js/include.js` — initializes the page, loads XML data, wires up skills/projects
- `js/fullpage.js` — custom fullpage scroll with 5 named sections
- `js/slider.js` — custom slider (4 items/page) used for skills and projects
- `js/popup.js` — detail overlay for projects, supports images and video
- `js/common.js` — device/OS detection, utility helpers
- `js/form-submission-handler.js` — contact form posts to Google Sheets via Google Apps Script

**CSS layers:** `default.css` (reset) → `include.css` (components) → `style.css` (main layout) → `media.css` (responsive breakpoints at 1000px desktop / mobile)

**Responsive:** Detects iOS/Android via user agent in `common.js`; CSS media queries handle layout. Portrait/landscape orientation is also handled.
