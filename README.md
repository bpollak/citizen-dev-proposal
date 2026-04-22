# Agentic Development at UC San Diego — ITS Proposal

Internal socialization deck for UCSD ITS leadership covering the proposed **citizen agentic development** framework.

**Live deck:** https://bpollak.github.io/citizen-dev-proposal/

## What's in here

- `index.html` — Reveal.js bootstrap that loads the slide markdown
- `slides/slides.md` — all slide content, editable as plain markdown
- `assets/theme.css` — UCSD-inspired color theme on top of the Reveal white theme
- `.github/workflows/pages.yml` — auto-deploy to GitHub Pages on push to `main`

## Structure

Four-act flow, ~22 slides, designed for a 20-45 min discussion with heavy Q&A time:

1. **Why** — the problem we're trying to solve
2. **What** — the tier-based framework
3. **How** — intake, harness, deploy, data, review
4. **Open questions** — where the audience helps shape the next iteration

## Local preview

```bash
# any static server will do
python3 -m http.server 8000
open http://localhost:8000
```

Press `S` for speaker notes (notes are inline in `slides/slides.md` after each `Note:` marker).

## PDF export

Append `?print-pdf` to the URL and print from Chrome/Chromium:

```
http://localhost:8000/?print-pdf
```

## Editing

- All content lives in `slides/slides.md` — no build step, edit and refresh
- Diagrams are [Mermaid](https://mermaid.js.org/) blocks embedded in the markdown
- Theme tweaks go in `assets/theme.css`

## Context sources

- Apr 22, 2026 agentic coding meeting transcript (participants: Brett Pollak, Matthew Holland, Shawn Munro, Adam Tilghman, Sandra Chalmers)
- OpenClaw wiki pages: TritonAI Developer API, TritonAI Embedded App Builder, TritonAI AI Initiative Readiness Copilot, TritonGPT, Mission Control
- Three source diagrams (simple picture, tier model, full pipeline) redrawn in Mermaid
