# Port 502

Open research on the security of operational technology.

A static site served by GitHub Pages. No build step.

## Pages

| Path | Page |
|---|---|
| `/` | Home |
| `/feed/` | OT security news feed |
| `/research/` | Research index |
| `/research/open-weight-ai/` | Report: Open-Weight AI Models in Critical Infrastructure |

Shared images live in `assets/`. All links between pages are relative, so the site
works both at a custom domain and at `https://<user>.github.io/<repo>/`.

## News feed

`/feed/` shows the stories published by the OT Wire pipeline
(`flyingmonkey789/ot-news-wire`). The page ships with a snapshot of the feed and,
on load, fetches the latest `feed.json` from `https://otnewswire.com/feed.json`,
falling back to the raw file on GitHub. It updates whenever the pipeline runs.

## Publishing

Settings → Pages → Build and deployment → Deploy from a branch → `main` / `/ (root)`.

## Adding a report

1. Copy `research/open-weight-ai/` to `research/<slug>/` and replace the content.
2. Add its cover image to `assets/`.
3. On `research/index.html`, move the topic from "In progress" to "Published".
4. Update the "Latest research" card on `index.html`.
