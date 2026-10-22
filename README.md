# MKT 412 classroom site

A lightweight collection of classroom activities for **MKT 412: Marketing Policy and Problems at Bryant University**. It began as a place to host low-stakes class materials and interactive marketing examples.

The site is plain HTML, CSS, and browser JavaScript. There is no package install, build command, application server, database, or API key to configure.

## Start here

- **Students / visitors:** open the [GitHub Pages site](https://howtobecalculated.github.io/MKT412/).
- **Professor taking over or extending the site:** read [CONTRIBUTING.md](CONTRIBUTING.md) for editing, preview, publishing, and fork instructions.
- **AI coding agent:** read [AGENTS.md](AGENTS.md) first, then the [activity inventory](pages/README.md). Give the agent this repository URL, not only the published site URL.
- **Claude Code:** [CLAUDE.md](CLAUDE.md) imports the same shared instructions, so both tools follow one maintained guide.

GitHub Pages is configured to publish `main` from `/ (root)` at the address above. Confirm future URL or source changes in [Settings → Pages](https://github.com/HowToBeCalculated/MKT412/settings/pages).

## Repository map

| Path | Purpose |
| --- | --- |
| [index.html](index.html) | Student-facing homepage; activity cards and navigation are maintained by hand. |
| [pages/](pages/) | Eleven individual HTML activities, mostly with their CSS and JavaScript in the same file. |
| [pages/README.md](pages/README.md) | Activity descriptions, dependencies, implementation entry points, and existing quirks. |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Human handoff and contribution guide. |
| [AGENTS.md](AGENTS.md) | Repository-wide instructions for coding agents. |
| [CLAUDE.md](CLAUDE.md) | Claude Code entry point importing the shared agent instructions. |

The homepage currently links to six original activities plus four clearly labeled drafts. The Solvix launch simulator is available by direct URL but has no homepage card. Three hidden cards refer to pages that do not yet exist; see the inventory before enabling them.

## Draft Studio

Four playable starting points are now linked from the homepage: **A/B Test Detective**, **Positioning Map Studio**, **Budget Allocation Challenge**, and **AI Marketing Critique Arena**. They run without external dependencies or API keys. Their data and coefficients are fictional teaching examples. See the [instructor extension guide](docs/draft-activities.html) for model assumptions and ways to adapt each page.

## Preview locally

From a clone of this repository:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Open [http://localhost:8000/](http://localhost:8000/). Stop the server with Ctrl+C. Python is only a convenient local preview tool, not a deployment dependency. A static preview server supplied by your editor also works.

Several pages load styling, fonts, icons, or charts from public CDNs, so a full preview needs internet access. Activity calculations run in the browser. The existing pages contain no backend calls or durable saved progress; download any available CSV results before leaving or reloading an activity.

## Extending it

Add a standalone HTML activity under `pages/`, add a matching card to `index.html`, and update the activity inventory. Use relative links so the site works under the `/MKT412/` project path and under a professor's fork. Keep existing filenames stable because instructors may have linked directly to activities from an LMS.

These are teaching simulations and examples. The pricing game's “AI rivals” are JavaScript rules, the SEO activity uses synthetic scenarios and heuristic scores, and the sentiment page supplies prompts to use elsewhere rather than calling an AI service.
