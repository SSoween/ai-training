# Training IA: interactive support for Claude

Two self-contained training pages for teams adopting Claude (Chat, Projects, Cowork). The content is in French. Each page is one HTML file with no build step and no dependency besides Google Fonts.

| Module | Folder | Focus |
|---|---|---|
| 1 · Premier contact | `module-1-premier-contact/` | How an LLM works, tokens, context, models and thinking, web and artifacts, Cowork, limitations and human in the loop, prompt workshop |
| 2 · Prendre les commandes | `module-2-prendre-les-commandes/` | Structured prompts, meta-prompting, projects, memory, skills, scheduled tasks, connectors, shared artifacts, security, controlled automation, "my first automation" workshop |

## What a page does

- One notion per step: short bullets for the session, plus a collapsed "Détails" block that goes into the export.
- Live demos (violet) and hands-on prompts to try (gold).
- Workflow navigation on desktop, compact navigation bar on mobile, Focus mode (one notion open at a time).
- Per-notion self-assessment (Clair / À consolider / Flou), "need more info" flag and private notes.
- Personal export at the end: printable HTML or Markdown.

## Two ways to run it

**1. Standalone (this repository, GitHub Pages or a local file)**
Open `index.html` in a browser. Everything works for one person: content, demos, levels, notes and export. Levels and notes stay in that browser (`localStorage`). There is no shared team dashboard in this mode, so the related controls are hidden.

**2. Live session with team tracking (Claude artifact)**
Publish the page as a Claude artifact to get the shared crew dashboard (who joined, levels per notion, info requests, result links), reusable sessions and owner-only trainer settings. Declare these capabilities when publishing:

```json
{"db":{"rules":[
  {"path":"sessions","read":"view","write":"admin"},
  {"path":"meta","read":"view","write":"admin"},
  {"path":"crew","read":"view","write":"owner"},
  {"path":"crew/{self}","read":"view","write":"interact"}]},
 "user":{"scopes":["profile"]}, "downloads":true}
```

Then:
- Share with participants as **Contributor**. Viewers cannot write, so their levels would never reach the dashboard. Editors could modify the page.
- Test with one colleague before the session: their name must appear in the dashboard within seconds.
- Reset between sessions: delete the `crew` documents and bump `meta/reset.at`, which also clears local copies in browsers. Ask participants to export their notes first.

## Adding or changing a notion

All content sits in the `MODULES` array at the top of the script. Copy a block, place it where the notion should appear, and give it a unique `id`. Numbering, navigation, dashboard and export adapt automatically.

```js
{ id:"unique", title:"Step title", notion:"Notion covered", short:"Short label",
  track:true,            // false for briefing / conclusion
  lede:"One-line hook",
  points:["<b>Key</b> : bullet", ...],
  visual:`<div class="widget" data-widget="name" data-print="Text for the export"></div>`,
  detail:`<p>Collapsed on screen, included in the export</p>`,
  tryIt:"Prompt to try in Claude" }
```

## Design

The "cockpit rétro" look (crisp or beveled corners, corner brackets, technical grid, beveled commands, cream ink on deep black) is one self-contained CSS block marked `SKIN « COCKPIT RÉTRO »`. Remove it to return to the previous look. Bevelled corners use `corner-shape`, available in recent Chromium browsers; other browsers show crisp square corners.

## Content notes

- Token, cost and model figures are illustrative orders of magnitude. Check current model availability and pricing before each session.
- Features such as memory and connectors depend on how your organization configures Claude.
- Official learning resources are linked in the last step of each module (Anthropic Academy, Claude documentation and help center).

## Usage

Internal training material. Review with your security or communication team before publishing outside your organization.
