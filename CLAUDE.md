# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single static landing page (`index.html`) promoting the "Jornada Internacional de Cirurgia Íntima e Terapia Regenerativa na Mulher", an event at Hospital Mãe de Deus (Porto Alegre, Brazil) on 04–05 December 2026. There is no build system, package manager, or framework — it's plain HTML/CSS/JS in one file.

## Running / previewing

There are no build or lint commands. Preview by opening the file directly or serving it locally:

```bash
open index.html
# or
python3 -m http.server 8000   # then visit http://localhost:8000
```

## File structure

- `index.html` — the entire site. Everything (styles, markup, script) lives in this one file:
  - `<style>` block defines a CSS custom-property design system at `:root` (`--ink`, `--paper`, `--wine`, `--rose`, `--gold`, `--serif`/`--sans` fonts, etc.) — reuse these variables rather than hardcoding colors/fonts when editing styles.
  - Page is a sequence of `<section>` elements with ids matching the nav anchors: `#sobre`, `#palestrantes`, `#programacao`, `#local`, `#inscricao`.
  - `<script>` at the bottom (vanilla JS, no dependencies) handles: nav scroll shadow, mobile menu toggle, day-tabs switching (`#day-1`/`#day-2` schedule panels), and a countdown timer targeting `2026-12-04T09:00:00-03:00`.
  - Includes a `schema.org` `MedicalEvent` JSON-LD block in `<head>` — keep this in sync with the visible date/location/speaker info if those change.
- `img/` — speaker photos and venue image referenced by `index.html` (`dr-charles-runels.png`, `dra-alexandra-runnels.png`, `dr-red-alinsod.png`, `hospital-mae-de-deus.jpg`).
- `jornada-info.md` — the source copy/content brief for the event (description, speaker bios, full schedule, contact/payment info). Treat this as the source of truth for event facts; `index.html` is its HTML rendering.

## Key content facts (keep consistent across `index.html`, `jornada-info.md`, and the JSON-LD)

- Event dates: 04–05 December 2026, Porto Alegre, RS.
- Registration/ticketing is external via Sympla: `https://www.sympla.com.br/evento/jornada-de-cirurgia-intima-e-terapia-regenerativa-do-hospital-mae-de-deus/3483090`.
- Contact is via WhatsApp: `https://wa.me/5551998360769`.
- When updating speakers, schedule, or venue details, update all three: the visible sections in `index.html`, the JSON-LD `MedicalEvent` block, and `jornada-info.md`.
