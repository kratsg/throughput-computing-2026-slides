# CLAUDE.md — working on this repo

This repo is a **reveal.js talk**: "LLM Assisted Analysis at the UC AF" (USATLAS F2F @
HTC26, 2026-06-09, Giordon Stark). It is **public** and auto-deploys to GitHub Pages.
Read `README.md` for the audience-facing overview; this file is for whoever edits it next.

## How to work on it

- The deck was authored with the **project-local skills** in `.agents/skills/`:
  - `revealjs/` — build mechanics (scaffold, overflow check, screenshots, in-browser editor)
    and design conventions. Read `.agents/skills/revealjs/SKILL.md` before structural changes.
  - `grill-me/` — the interview-the-user-to-lock-decisions skill used to scope the talk.
- It's already scaffolded. **Don't re-scaffold.** Edit `presentation.html` incrementally
  (one or a few slides at a time) — never rewrite the whole file at once.

## The edit → verify loop (do this every change)

1. Edit `presentation.html` / `styles.css`.
2. `node .agents/skills/revealjs/scripts/check-overflow.js presentation.html` — must report
   **no overflow** (slides are fixed 1280×720; content must fit).
3. Screenshot with decktape and **look at every changed slide** (see README for the command).
4. **Known gotcha:** slides with video or large images render *scaled-down in decktape's
   export* — a capture artifact, not a real problem. Confirm via `check-overflow.js` (and, if
   unsure, a Puppeteer screenshot navigating with `Reveal.slide()`); the browser render is fine.

## Conventions (match these)

- **Theme:** UChicago Maroon (`#800000`) on warm off-white, teal/slate accents. All in
  `styles.css` CSS variables. **Font sizes in `pt`**, never px/em/rem (fixed-size slides).
- **reveal 6.0.1** from CDN. Plugins: **Notes only** (`dist/plugin/notes.js`). The chart
  plugin was removed (unused, didn't register on v6). `slideNumber: 'c/t'`.
- **Vertical stacks (columns):** the core-insight pair (`slide-13`, `slide-13b`) and the
  architecture run (`slide-14/15/16/16b`) are grouped as vertical stacks — right-arrow moves
  between sections, down-arrow within. Keep that structure if adding architecture slides.
- **Em-dash policy (humanized):** prose uses commas/colons/periods. Keep em-dashes only for
  real quotations, the "— Giordon" attribution, and the "Name — role" team list on slide 18.
  Don't reintroduce prose em-dashes.
- **Boxes:** cards for parallel items, `.callout` for "the point" / open questions. The deck
  is intentionally box-rich but not over-boxed; don't pile more onto `slide-17-2`.
- **Speaker notes:** every slide has an `<aside class="notes">`. Keep them conversational
  (first person, spoken cadence). They use straight apostrophes and commas, not em-dashes.

## Images

- Live in `images/` and are committed (incl. the 16 MB web-friendly `jupyter-mcp-demo.mp4`).
- Fill a placeholder by replacing a `<div class="shot">…</div>` with `<img src="images/…">`
  (or `<video>`). Cap large media height (e.g. `max-height:470px`) so the slide fits.
- **Provenance:** AI-generated images must be credited on-slide (see the title footnote and
  slide 15's "Image: Google Gemini 3.1 Pro"). The Watts boat is "© Watts + AI".

## Commits & deploy

- Commit/push to **`main`** (no feature branches needed here). Conventional Commits.
- End commit messages with `Assisted-by: Claude (Anthropic)` (Giordon's convention — not
  Co-Authored-By).
- Pushing `main` auto-deploys to GitHub Pages via `.github/workflows/deploy.yml`. Verify the
  run is green and the live site updated.

## Source material (LOCAL ONLY — gitignored on purpose)

These inputs live in the working tree but are **not committed**, and should stay that way:

- `af-agentic-ai-research.md` — the Slack/email research that seeded the deck. **Contains
  internal details (usernames, ops internals) beyond what's on the public slides — do NOT
  commit it.** This is why it's gitignored, not an oversight.
- PDFs (`*.pdf`): Gordon Watts' and Vakho Tsulaia's CHEP talks — large/external; link, don't commit.
- Checked-out repos: `marketplace/`, `rucio-mcp/`, `ami-mcp/`, `jupyter-mcp-server/`,
  `af-docs/`, `flux_apps/` — external sources used for accurate tool names/commands. Link, don't commit.
- `TODO.md` — Giordon's personal pre-talk checklist (gitignored).

**This repo is public.** Don't add internal usernames, emails, or ops internals beyond the
level already on the slides.

## Getting Slack/email-sourced facts

For anything that lives only in Giordon's Slack or email (real outputs, adoption numbers,
quotes), don't fabricate — hand Giordon a copy-paste prompt to run in **Claude App** (which
has those connectors) and fold the result back in. `af-agentic-ai-research.md` was produced
that way.
