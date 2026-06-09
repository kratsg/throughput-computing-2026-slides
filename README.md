# LLM-Assisted Analysis at the UC AF

Slides for the talk **"LLM Assisted Analysis at the UC AF"** — the USATLAS Face-to-Face
session at Throughput Computing Week 2026 (HTC26), 2026-06-09, by Giordon Stark on behalf
of the UChicago Analysis Facility team.

**▶ View the deck:** https://kratsg.github.io/throughput-computing-2026-slides/

The deck argues one thing: a generic LLM isn't enough — the value comes from wrapping
**facility context** (storage, scheduler etiquette, data access) and ATLAS tools behind
agentic interfaces, built so the framework is shared and the context ports to the next AF.

## What's here

| Path | What it is |
|------|------------|
| `presentation.html` | The deck (reveal.js 6.0.1, loaded from CDN — no build step) |
| `styles.css` | UChicago-maroon theme (CSS variables, `pt` font sizing) |
| `images/` | Committed figures + the web-friendly demo video (`jupyter-mcp-demo.mp4`) |
| `talk-notes.md` | Front-loaded Decisions / Milestones / Action Items / Notes for the agenda |
| `.agents/skills/` | The `revealjs` build skill + `grill-me`, used to author the deck |
| `.github/workflows/deploy.yml` | Auto-publishes to GitHub Pages on push to `main` |

## View it

- **Online:** the GitHub Pages link above (always reflects `main`).
- **Locally:** open `presentation.html` in a browser. It pulls reveal.js from a CDN, so you
  need a network connection the first time.
- **Speaker notes:** press **`S`** in the browser (allow the popup) for speaker view —
  current + next slide, notes, and a timer. Every slide has notes.

## Edit it

The deck is plain HTML + CSS. Edit `presentation.html` directly (one slide / a few slides
at a time), or use the in-browser editor from the reveal.js skill:

```bash
node .agents/skills/revealjs/scripts/edit-html.js presentation.html
```

After editing, check for content overflow and review screenshots (Node deps live under
`.agents/skills/revealjs/node_modules`, gitignored — run `npm install` there if missing):

```bash
# flag any slide whose content exceeds 1280×720
node .agents/skills/revealjs/scripts/check-overflow.js presentation.html

# screenshot every slide (export mode disables animations)
.agents/skills/revealjs/node_modules/.bin/decktape reveal "presentation.html?export" \
  output.pdf --screenshots --screenshots-directory "screenshots/$(date +%Y%m%d_%H%M%S)"
```

> Heads-up: media-heavy slides (video / large images) can render *scaled-down* in the
> decktape export — that's a capture artifact. They render correctly in a real browser;
> trust `check-overflow.js` (it reports no overflow) over the decktape thumbnail.

## Deploy

Pushing to `main` triggers `.github/workflows/deploy.yml`, which publishes
`presentation.html` (as `index.html`) + `styles.css` + `images/` to GitHub Pages and
attaches a best-effort `slides.pdf`. One-time setup: repo **Settings → Pages → Source:
GitHub Actions**.

## Credits

Slides AI-assisted by Claude (Anthropic). Title illustration and the sports-team analogy
image are AI-generated (the latter via Google Gemini); the Gordon Watts "Analysis
Ecosystem" boat is from his CHEP 2026 slides (© Watts + AI). OpenWebUI and Slack
screenshots are real captures. Built in the spirit of Gordon Watts' CHEP 2026 ecosystem
framing.
