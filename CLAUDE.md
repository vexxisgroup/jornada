# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A static landing page promoting the "Jornada Internacional de Cirurgia Íntima e Terapia Regenerativa na Mulher", an event at Hospital Mãe de Deus (Porto Alegre, Brazil) on 04–05 December 2026. There is no build system, package manager, or framework — it's plain HTML/CSS/JS. The page exists in three parallel, fully self-contained language versions (PT-BR, EN-US, ES) that each duplicate the full markup/styles/script rather than sharing templates.

## Running / previewing

There are no build or lint commands. Preview by opening the file directly or serving it locally:

```bash
open index.html
# or
python3 -m http.server 8000   # then visit http://localhost:8000
```

## File structure

- `index.html` — PT-BR (default/original), at the repo root.
- `en/index.html` — English (en-US) translation.
- `es/index.html` — Spanish (es) translation.
- Each of the three HTML files is a fully self-contained page (styles, markup, script all inline) with identical structure:
  - `<style>` block defines a CSS custom-property design system at `:root` (`--ink`, `--paper`, `--wine`, `--rose`, `--gold`, `--serif`/`--sans` fonts, etc.) — reuse these variables rather than hardcoding colors/fonts when editing styles. The `<style>` block is byte-for-byte identical across all three files except for a couple of comment headers translated per language — copy CSS edits to all three.
  - Page is a sequence of `<section>` elements with ids matching the nav anchors. IDs are translated per language and differ across files: PT `#sobre`/`#palestrantes`/`#programacao`/`#local`/`#inscricao`/`#topo`; EN `#about`/`#speakers`/`#schedule`/`#venue`/`#registration`/`#top`; ES `#acerca`/`#ponentes`/`#programa`/`#sede`/`#inscripcion`/`#inicio`.
  - `<script>` at the bottom (vanilla JS, no dependencies, identical in all three files) handles: nav scroll shadow, mobile menu toggle, day-tabs switching (`#day-1`/`#day-2` schedule panels — these ids are NOT translated), and a countdown timer targeting `2026-12-04T09:00:00-03:00`.
  - Includes a `schema.org` `MedicalEvent` JSON-LD block in `<head>`, translated per language (`name`/`description`/location name), except proper nouns (speaker names, clinic name, street address) which stay as-is — keep in sync with the visible date/location/speaker info if those change.
  - `<head>` has `hreflang` alternate `<link>` tags pointing at the other two language versions plus `x-default`; these currently use relative URLs (`./index.html`, `./en/index.html`, `./es/index.html`) as placeholders since the site has no deployed domain yet — replace with absolute URLs once one exists.
  - A `.nav-lang` language switcher (`PT` / `EN` / `ES`) sits at the end of the nav links in all three files; update its relative hrefs if the directory layout changes.
- `img/` — speaker photos and venue image, referenced as `img/...` from the root `index.html` and as `../img/...` from `en/index.html` and `es/index.html`.
- `jornada-info.md` — the source copy/content brief for the event (description, speaker bios, full schedule, contact/payment info), in Portuguese. Treat this as the source of truth for event facts; the three `index.html` files are its (translated) HTML rendering.

## Key content facts (keep consistent across all three `index.html` files, `jornada-info.md`, and each file's JSON-LD)

- Event dates: 04–05 December 2026, Porto Alegre, RS.
- Registration/ticketing is external via Sympla: `https://www.sympla.com.br/evento/jornada-de-cirurgia-intima-e-terapia-regenerativa-do-hospital-mae-de-deus/3483090`.
- Contact is via WhatsApp: `https://wa.me/5551998360769` (shown as a local-format number on the PT page, and with the `+55` country code on the EN/ES pages for an international audience).
- When updating speakers, schedule, or venue details, update **all five** places: `index.html`, `en/index.html`, `es/index.html` (visible content + JSON-LD in each), and `jornada-info.md`.
