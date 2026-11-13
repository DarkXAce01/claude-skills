---
name: portfolio-dossier
description: Build a portfolio dossier for the current project, so Jewel's portfolio session can turn it into a site entry. Use when the user types /portfolio-dossier or asks to "prepare this project for my portfolio / website", "make a portfolio folder", or "document this project for my site". It researches the codebase and git history, gathers real screenshots and diagrams, and writes everything into one folder.
---

# Portfolio dossier

You are preparing **source material** for Jewel Chowdhury's personal portfolio site. A separate Claude session (the portfolio session) reads the folder you produce and turns it into a project page (a Persona-5 style "calling card"). Your job is to be a thorough, honest researcher and photographer, not a copywriter. The portfolio session writes the final copy.

## Hard rules

1. **Facts only.** Every claim in the dossier must come from the code, the git history, docs in the repo, measured output you ran, or something the user told you in this session. If you can't verify it, leave it out or put it under "Unverified (ask Jewel)". Never invent numbers, users, adoption, awards or performance figures.
2. **No private data.** Never include any email address, phone number, home address, API keys, tokens, passwords, internal hostnames, private IPs, Wi-Fi names or account IDs. That covers text, screenshots and terminal output. Redact before saving: blur or crop images, replace strings with `[REDACTED]`. **Never include an office or work email in any form.**
3. **Company IP.** If the project is work done for an employer or client, mark it `door: work`. Collect **no screenshots, no code and no internal names** (customers, plants, vendors, internal tools). Only a plain description of what it is and does, the stack, and the problem it solves.
4. **Credit honestly.** List everyone who built it, as the user tells you. Don't scrape names or emails from git authors. Ask the user who should be credited and how.
5. **Read-only on the project.** Don't modify the project's code, commit, or push. Write only inside the dossier folder.
6. **Ask, don't guess,** about anything only Jewel knows: why he built it, what was hardest, what he's proudest of, who it's for. Do it in **one** short batch of questions after your research, not one by one.

## Where to write

`~/portfolio-dossiers/<slug>/`, where `<slug>` is lowercase letters, numbers and hyphens (e.g. `tv-android-bridge`). Create it if missing. If it already exists, update it in place and note what changed in `CHANGELOG.md` inside it.

```
~/portfolio-dossiers/<slug>/
  dossier.md          the main document (template below)
  facts.json          machine-readable fields (template below)
  screenshots/        original-resolution PNG/JPG, named 01-<what>.png, 02-<what>.png, ...
  diagrams/           architecture or flow diagrams (SVG preferred, or PNG)
  media/              optional: logo, demo video/GIF, photos of hardware
  terminal/           optional: real command transcripts (*.txt) showing it working
  questions.md        anything still unanswered for Jewel
```

## Process

1. **Research.** Read the README and docs, the package manifests, the entry points and the main modules. Read `git log` for the timeline: first and last commit dates, major milestones, contributors only as counts. Find out what it does, how it works end to end, the stack, how to install or run it, licence, and repo/live/store links.
2. **Measure, don't estimate.** If there are honest numbers you can get by running something (start time, size of the binary, number of supported devices/providers/commands, tests passing), run it and record the exact command and output in `terminal/`. Public stats (GitHub stars, downloads) go in `facts.json` but are optional; Jewel decides whether they're shown.
3. **Capture visuals.**
   - Web or desktop UI: run it locally and screenshot the key screens at 1440×900, plus a phone size if it's responsive. Use Playwright or the platform's screenshot tool. Use realistic but **fake** data; redact anything personal.
   - CLI or tool: save real terminal sessions to `terminal/*.txt` (the portfolio can replay them as an animated terminal), and render one clean screenshot of the best moment.
   - Hardware, TV, phone or physical devices you can't screenshot: list exactly which photos or screen captures Jewel should take (e.g. "the TV home screen after setup", "the remote pairing screen") in `questions.md`, with suggested file names. Never fake them.
   - Diagrams: draw the architecture or data flow as an SVG from what the code actually does (boxes for components, arrows for data). Keep it readable at 680 px wide.
4. **Ask Jewel** the remaining questions in one batch: motivation, the hardest problem, what he's proudest of, who it's for, collaborators to credit, anything that must not be shown. Fold the answers into the dossier.
5. **Write** `dossier.md`, `facts.json` and `questions.md`. Then do a final privacy pass. Grep the whole folder for `@`, `token`, `key`, `password`, `192.168.`, `10.` and hostnames, and check every screenshot. Fix anything found.
6. **Report** to the user: the folder path, what's in it, and what's still missing (e.g. photos he needs to take).

## dossier.md template

```markdown
# <Project name>

**One line:** what it is, in plain words (max ~15 words).
**Tagline idea:** a punchy line in the project's own spirit (the portfolio session may rewrite it).
**Door:** builds (personal) | work (employer/client; text only)
**Kind:** software | app | game | 3d | hardware
**Year / period:** e.g. 2026, or 2025 to 2026
**Status:** working prototype | in daily use | released | archived
**Licence:** MIT / proprietary / none
**Links:** repo, live demo, store page (only public ones)
**Built with:** names to credit, and how they want to be credited

## The problem (THE TARGET)
What was broken or missing, for whom. 2–4 sentences, concrete.

## The approach (THE PLAN)
3–6 bullets, in order, on how it works. Name the key technical decisions and why.

## The result (THE TREASURE)
What it achieves now. Real, verifiable outcomes only (measured numbers with their command in terminal/).

## How it works (architecture)
A short walkthrough of the components and data flow. Reference diagrams/<file>.

## Highlights
The 3–5 most impressive or clever parts (engineering details a technical reader would enjoy).

## Hardest problems and how they were solved
2–4 short stories.

## Stats
Up to 6 honest value + label pairs, e.g. `~28ms` / `snapshot boot`, `5` / `providers`. Each with its source.

## Comparison (optional)
How it differs from the existing alternatives, as a small table, with facts only.

## Install / try it
The exact commands, if public.

## Screenshots
One line per file in screenshots/: `01-home.png`: caption, then alt text (what's visible, for screen readers).

## Must not be shown
Anything Jewel said to keep private.
```

## facts.json template

```json
{
  "slug": "tv-android-bridge",
  "title": "Project Name",
  "door": "builds",
  "kind": "hardware",
  "summary": "One plain sentence.",
  "tagline": "Optional punchy line.",
  "pitch": "2-3 sentence elevator pitch.",
  "year": 2026,
  "date": "2026-09-01",
  "licence": "MIT",
  "tech": ["Kotlin", "ADB", "..."],
  "links": { "repo": "", "live": "", "store": "" },
  "collaborators": [{ "name": "", "url": "" }],
  "stats": [{ "value": "", "label": "", "source": "terminal/xyz.txt" }],
  "story": { "target": "", "plan": ["", ""], "treasure": "" },
  "install": [{ "label": "", "cmd": "" }],
  "gallery": [{ "file": "screenshots/01-home.png", "caption": "", "alt": "" }],
  "architecture": { "file": "diagrams/architecture.svg", "alt": "" },
  "replay": { "file": "terminal/demo.txt", "title": "", "note": "Recorded <date> on <setup>. Output is real." },
  "publicStats": { "githubStars": null, "downloads": null, "asOf": "" },
  "unverified": []
}
```

Leave a field empty or omit it rather than guessing. `stats[].source` and `replay` must point to real files in the folder.
