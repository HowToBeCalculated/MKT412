# Activity inventory

Each HTML file in this directory is an independent activity. The homepage is `../index.html`; it does not automatically discover new files.

## Existing activities

| File | What it does | Homepage |
| --- | --- | --- |
| [new-product-simulator.html](new-product-simulator.html) | Generic launch model with market sizing, acquisition, pricing, uncertainty, revenue/cashflow/customer charts, and CSV exports. | Visible |
| [tam-sam-som-simulator.html](tam-sam-som-simulator.html) | EcoCharge EV-charging case with market sizing, strategy scenarios, and five-year revenue projections. | Visible |
| [sentiment-analysis.html](sentiment-analysis.html) | Examples and advice for writing sentiment-analysis prompts. This is reading material, not a live sentiment analyzer. | Visible |
| [market-research-insights.html](market-research-insights.html) | Sample digital-marketing dashboard: revenue/spend, traffic/conversion, channel revenue, and ROAS charts using mock data. | Visible |
| [strategic-pricing-game.html](strategic-pricing-game.html) | Five-round pricing/promotion game against two scripted rivals, with three market segments, demand exploration, charts, and CSV export. | Visible |
| [seo_serp_teardown_simulator.html](seo_serp_teardown_simulator.html) | Synthetic SERP scenarios and heuristic SEO scoring, predicted rank, and advice. No live search-engine data. | Visible |
| [solvix-new-product-simulator.html](solvix-new-product-simulator.html) | Solvix case version of the launch simulator with its own defaults and implementation. | Direct link only |

## New Draft Studio activities

These are playable, intentionally simplified bases for another professor and agent to extend. All four have homepage cards, reset controls, inline instructor notes, and no external dependencies. See the [extension guide](../docs/draft-activities.html).

| File | What it teaches | Main editable blocks |
| --- | --- | --- |
| [ab-test-detective.html](ab-test-detective.html) | Sampling variation and observed vs underlying conversion rates; four reveal checkpoints and Wilson intervals. | `SCENARIOS`, `CHECKPOINTS`, `wilson()`, `advance()` |
| [positioning-map-studio.html](positioning-map-studio.html) | Customer preference, competition, and why an empty position may have little demand. Drag brands or use sliders. | `INITIAL_BRANDS`, `SEGMENTS`, `TASTE_WIDTH`, `NO_PURCHASE`, `choiceShares()` |
| [budget-allocation-challenge.html](budget-allocation-challenge.html) | Diminishing returns, a fixed budget, channel interactions, and market events. | `CHANNELS`, `EVENTS`, `BUDGET`, `MARGIN`, `evaluate()` |
| [ai-marketing-critique-arena.html](ai-marketing-critique-arena.html) | Critiquing fictional AI-style campaign copy against a supplied brief and evidence constraints. | `CASES`, `ISSUE_TYPES`, `review()` |

No page calls an AI model or stores student data. State remains in memory and resets on reload. Budget history is per session; critique scoring is a teaching rubric. A/B intervals use the formula linked from [NIST](https://www.itl.nist.gov/div898/handbook/prc/section2/prc241.htm); the positioning and budget models are explicitly invented for classroom exploration. The default A/B experiment is seeded; budget events follow a fixed cycle rather than a random draw.

## Where to make changes

- **Both launch simulators:** look for `defaults`, `state`, `applyPreset()`, and `currentParams()` for inputs; `computeDeterministic()` and `simulate()` for calculations; `render()`, chart helpers, and export handlers for outputs. They use seeded randomness. Review both files when applying a shared model correction; changing one does not update the other. In the Solvix file, CSV handlers use optional element lookup, so check which export buttons are actually present before promising an export UI.
- **EcoCharge TAM/SAM/SOM:** `state`, `competitorScenarios`, and `calculateProjections()` hold the case inputs and model; `updateAll()` refreshes the page. A `runSelfCheck()` helper exists, but its developer button is hidden; this is not a repository-wide test suite.
- **Sentiment prompts:** edit the HTML sections directly. Students take the prompts to their chosen AI tool; no model integration is configured here.
- **Marketing dashboard:** chart creation and mock data are inline. See the existing initialization issue below before extending it.
- **Pricing game:** `MAX_ROUNDS`, `SEGMENTS`, firm setup, and `simulateRound()` control the game; `predictAtPrice()` and the explorer helpers control previews. Rivals use rules in JavaScript. Although a random “Seed” is displayed, randomness also uses `Math.random()`; do not treat that label as a reproducible run control.
- **SEO simulator:** edit `WEIGHTS` and `SCENARIOS` for the instructional model; `userMetrics()`, `scoreFromMetrics()`, `predictRank()`, and `update()` connect controls to results. The displayed scenario JSON is read-only, not an import/editor feature.

## External dependencies

| Location | Loaded in browser |
| --- | --- |
| Root homepage | Tailwind CSS CDN; Google Fonts (Inter) |
| EcoCharge TAM/SAM/SOM | Tailwind CSS CDN; Lucide icons from unpkg (`@latest`); Google Fonts (Inter) |
| Marketing dashboard | Chart.js 4.4.3 from jsDelivr |
| Other nine activities (including all four drafts) | No external script or stylesheet URLs in the current source |

These dependencies load at runtime, without an install/build step. CDN changes or blocked network access can affect the dependent pages. The other activities use inline styles/scripts and native browser features, including canvas charts where applicable.

## Existing quirks to understand

- The homepage includes **hidden** cards for `customer-segmentation.html`, `ad-campaign-optimizer.html`, and `chatbot-personalization.html`. None of those three files exists. They are placeholders, not implemented activities. Keep the cards hidden unless their target pages are added; a link checker scanning every anchor will report them.
- Solvix exists but has no homepage card. Use its direct path or add a card deliberately.
- The marketing dashboard contains **two script blocks initializing charts on the same four canvases**: an initial random sample and a later seeded mock-data implementation. Chart.js can reject the second initialization because the canvas is already in use. This is a source-level finding, not a browser-verified diagnosis. A focused fix should choose one initialization path or properly destroy/reuse existing charts.
- The generic and Solvix launch simulators duplicate substantial code and can diverge. Keep the case differences deliberate.
- Lesson dates, company examples, and simulation assumptions are embedded in the HTML. Review them for your own course rather than assuming they represent current market data.

This documentation describes the existing source. Adding it does not change the activities or repair the listed quirks.
