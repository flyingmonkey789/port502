# Port 502 — site guide

Port 502 publishes open research on the security of operational technology (OT).
This repo is the public website at **https://port502.com**, served by GitHub Pages
from `main` / root. Plain static HTML: no framework, no build step.

Owner: Kamden Schewitz. Keep responses condensed. When refining copy, give the
copy options only, without commentary.

## Structure

| Path | Page |
|---|---|
| `index.html` | Home |
| `feed/index.html` | OT security news (nav label: "Live Feed") |
| `research/index.html` | Research index (H1: "OT Security Reports") |
| `research/open-weight-ai/index.html` | Report: Open-Weight AI Models in Critical Infrastructure |
| `assets/` | Images (report covers) |
| `CNAME` | `port502.com` — do not remove |

- Each page is one self-contained HTML file with its own `<style>` and `<script>`.
  Shared styles are duplicated per page; when changing a shared element (nav,
  footer, subscribe, buttons), update every page.
- **Links are relative** (`./`, `../`, `../../`) so the site works on the custom
  domain and on github.io. Never use absolute site URLs for internal links.
- Pages with a cover use `.feat-img` with `background-image:url("<relative>/assets/...")`.

## Design rules

The look is minimal, single-column, editorial. Follow these unless asked otherwise.

- **Layout:** one centered column, `max-width:640px`, side padding 24px (20px on phones).
  Breakpoints: `520px` and `440px`. No horizontal page scroll at 320px+.
- **Corners: square everywhere.** Each page ends its CSS with
  `*,*::before,*::after{border-radius:0 !important}`. Keep it.
- **Color:** black, white and grays only.
  `--text:#000` `--ink:#262626` `--muted:#525252` `--subtle:#737373`
  `--line:#E5E5E5` `--fill:#F2F2F2` `--surface:#FAFAFA`.
  No colored category pills or accent colors. (Report cover art may be in color.)
- **Type:** display font `--display` ("SF Pro Rounded", system fallback) for
  H1s, card titles and section titles; `--sans` (Inter/system) for body;
  `--mono` only for small metadata (chapter numbers, counts, CVSS, sources).
  Weights 400–600 only.
- **H1:** `clamp(30px,5vw,40px)`, weight 500, line-height 1.12,
  letter-spacing −0.01em. All page H1s must match exactly.
- **Section labels (h2):** small, gray, sentence case (e.g. "Latest research").
- **Buttons:** primary = black fill, white text; secondary = light gray fill or
  1px outline. On hover a white/outline button turns **black with white text**;
  never dark text on a dark background. Watch the global `button:hover` rule.
- **Spacing:** sections are ~64px apart; related items inside a block use even
  gaps (e.g. heading → field → note at 16px). Left edges align exactly.
- **Nav (top bar, every page):** "Port 502 Research" left; right: Live Feed,
  Research, and a black **Subscribe** button that opens a centered modal.
  The current page link gets `aria-current="page"`. Under 440px the text links
  hide and a square menu button (`#menuBtn`) opens an accordion (`#mnav`) with
  Home, Live Feed, Research. Update the menu on every page when adding pages.
- **Footer:** "© 2026 Port 502" left; Research, News, LinkedIn, Contact right
  (Contact is a `<button>` styled exactly like the footer links). Contact opens a modal form (`#contactModal`).
- Keep things simple: Kamden prefers fewer elements, plain copy, no busy meta lines.

## Home page (top to bottom)

H1 "Open research on the security of operational technology." → description
"Port 502 helps the people who protect, build, and fund critical infrastructure
stay ahead of what's next." → buttons "Read the research" / "Read the news" →
Latest research card → email signup → About → two cards (Read the research /
Read the news) → footer.

## News feed (`feed/`)

- Data comes from the OT Wire pipeline in **flyingmonkey789/ot-news-wire**
  (hourly GitHub Action → `docs/feed.json`).
- The page embeds a snapshot, then fetches live data from
  `https://otnewswire.com/feed.json`, falling back to
  `https://raw.githubusercontent.com/flyingmonkey789/ot-news-wire/main/docs/feed.json`.
- Item fields: `url, published, category, source, sector, title, summary`.
  Categories come from the data (currently Incidents, Policy, Technology,
  Research, Advisory). Filter chips are built from the data and wrap onto
  multiple lines (no horizontal scrolling).
- Story meta line: category · source (· sector unless "Cross-sector"); CVSS, if
  present, right-aligned. No times.
- "Take it with you" uses the RSS feed `https://otnewswire.com/feed.xml`.
- "How it works" modal: Aggregate Agent, Correlation Agent, Publishing Agent.
  Do not mention "502 Engine" on this page.

## Research

- `research/index.html`: filter chips (All, Risk, Response, Investment),
  "Published" card(s), "In progress" grid (2 columns; compact list on phones).
  Keep in-progress titles ~22–27 characters and descriptions ~89–90 characters
  so each card wraps to the same number of lines.
- **Adding a report:**
  1. Copy `research/open-weight-ai/` to `research/<slug>/`, replace content.
  2. Add the cover to `assets/` (16:9, ~1600px wide, JPG).
  3. Move the topic from "In progress" to "Published" on `research/index.html`.
  4. Update the "Latest research" card on `index.html`.
  5. In the report, set `CANONICAL` in the "Summarize with AI" script to
     `https://port502.com/research/<slug>/`.
- Report layout: breadcrumb, title + subtitle, description, meta line,
  "Summarize with AI" (Claude / ChatGPT / Copilot), cover, collapsible Contents,
  numbered sections, stat boxes, takeaways, controls list, source tags.

## Copy and claims

- About text: "Port 502 provides open research around the security of
  operational technology. Our research is created based on aggregate findings
  across hundreds of public sources such as government advisories, threat
  research, regulatory filings, and funding data."
- Only state numbers that can be backed up. Cite sources for every statistic.
- Don't reuse real company logos or trademarked marks in artwork.

## Open items

- Subscribe forms are not connected yet (planned: Beehiiv).
- Contact form is not connected yet: set `action="https://formspree.io/f/<id>"` on
  `#contactForm` on every page; the script posts it and shows a thank-you.
- Report "Download PDF" button was removed until a PDF exists.
- Readiness assessment page exists outside this repo; not yet added.

## Checks before committing

- Open each changed page at 1280px and 390px; no console errors, no horizontal
  scroll, no broken relative links or images.
- Commit to `main`; Pages redeploys automatically.
