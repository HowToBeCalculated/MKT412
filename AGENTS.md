# Instructions for coding agents

These instructions apply to the whole repository.

## Purpose and architecture

Maintain a small, easy-to-share classroom site for MKT 412. Read [README.md](README.md), [CONTRIBUTING.md](CONTRIBUTING.md), and [pages/README.md](pages/README.md) before editing.

- `index.html` is the manually maintained directory of activities.
- Each activity lives in `pages/*.html`; CSS and JavaScript are generally inline.
- There is no package manifest, build pipeline in the repository, backend, database, or automated test suite.
- GitHub Pages publishes `main` from `/ (root)` using GitHub's branch-based build. Recheck Settings → Pages before changing deployment assumptions.
- Preserve this static architecture for ordinary content and activity changes. Do not add a framework, bundler, package manager, or server unless the requested feature needs it and the maintainer agrees.

## Working rules

1. Read the whole activity before editing it. Preserve the existing IDs, event bindings, input units, defaults, and calculation/render flow unless the task calls for changes.
2. Keep changes scoped to the request. Explain unrelated issues you find rather than silently repairing them.
3. Preserve existing filenames and direct URLs. Use `pages/example.html` from the root homepage and `../index.html` for a home link within an activity. Avoid links beginning with `/` and hardcoded owner/repository URLs in internal navigation.
4. For a new activity, add a complete HTML document with language, character encoding, viewport, descriptive title, labeled controls, and usable keyboard focus. Add its homepage card and inventory entry unless it is intentionally direct-link-only.
5. Reuse the selected page's visual conventions. The homepage uses dark styling with gold accents and Tailwind's CDN; individual activities have their own styles.
6. Prefer existing browser APIs and dependencies. If adding or changing a CDN dependency, document it and verify the page with it loaded.
7. Keep instructional assumptions visible. Do not describe synthetic values, heuristic rankings, random outcomes, or scripted opponents as live data or an external AI model.
8. Preserve input bounds and output units. For model changes, document what assumption or formula changed and check a small known example or invariant; use a fixed seed where the activity actually supports reproducible randomness.
9. This repository and its published files are public. Use synthetic classroom examples; keep credentials, grades, student submissions, and identifiable student data out of source, fixtures, exports committed to Git, and browser code.
10. Update relevant documentation when adding/removing an activity, changing dependencies, or changing publishing requirements.

Use the standard filename `AGENTS.md` for these instructions; avoid creating a second, divergent `Agent.md`.

## Verification

There is no `npm test`, install step, or build step to run. Preview from the repository root:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

For an HTML or JavaScript change:

- Open the homepage and changed activity over HTTP. Check a direct activity URL too.
- Confirm visible homepage links resolve. The three existing hidden placeholders are documented in `pages/README.md`; do not make them visible without implementing their targets.
- Exercise the relevant controls, recalculation, reset, scenarios, charts, and CSV downloads that actually exist on the changed page.
- Check browser console errors. Compare against the baseline; the market dashboard has duplicate chart initialization, as documented in the inventory.
- Check a narrow/mobile viewport, readable labels, and keyboard interaction for changed controls.
- For the launch simulators, compare repeat runs with unchanged parameters and seed. Do not assume the pricing game's displayed seed provides reproducibility.
- Review the diff for accidental changes to other activities and links.

For documentation-only changes, check relative links and factual claims against the source; no application test suite needs to be introduced. Report what was verified and any checks you could not perform. Do not claim a browser or live deployment check succeeded unless you performed it.

## Delivery

Prefer a focused branch and pull request for changes to the shared course site. Describe the student-visible behavior, files changed, and checks performed. A PR branch is not automatically a published preview. Merging into the configured Pages source branch can publish changes; follow the maintainer's requested delivery scope and leave Pages settings alone unless asked to change them.
