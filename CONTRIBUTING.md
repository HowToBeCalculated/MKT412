# Professor and contributor handoff

## Choose where to work

**Extend this shared course site:** use a branch and pull request in [HowToBeCalculated/MKT412](https://github.com/HowToBeCalculated/MKT412). The owner can grant repository access if you will maintain it directly.

**Make your own course version:** fork the repository to your GitHub account and work there. Enable GitHub Pages for that fork; it has its own publishing settings and URL. Updating a fork does not update the original course site. You can contribute selected changes back through a pull request.

GitHub Pages is the published website. It lets students and professors use activities, but editing requires the GitHub repository (or a clone/fork). An AI agent needs repository access to read and change the HTML.

## Hand the repository to your agent

Claude Code can use this repository directly: the root `CLAUDE.md` imports `AGENTS.md`, which holds the shared project instructions. Start Claude Code in the repository root and use `/context` to confirm the instructions loaded. This follows [Claude Code's documented import syntax](https://code.claude.com/docs/en/memory#import-additional-files). Keep shared guidance in `AGENTS.md` rather than maintaining separate Claude-specific copies.

For a browser chat with Claude, explicitly ask it to read the guides and provide repository access or the files through the tools available in that session. A published Pages URL alone is not a source-editing connection.

Give your agent the repository URL or your fork's URL, and a concrete teaching goal. For example:

> Read README.md, AGENTS.md, and pages/README.md in this repository. Add a standalone activity about [topic] for [audience]. Keep it compatible with GitHub Pages, add a homepage card, update the inventory, and verify its controls and direct link. Open a pull request with a short explanation and your verification results.

For a smaller edit, name the activity and what should change (scenario, defaults, explanatory text, calculation, or interaction). Clarify when a change should apply to both launch simulators; they are separate files, not two views of shared code.

## Preview

Clone your chosen repository and change into its directory:

```sh
git clone https://github.com/HowToBeCalculated/MKT412.git
cd MKT412
python3 -m http.server 8000 --bind 127.0.0.1
```

For a fork, substitute its clone URL. Open [http://localhost:8000/](http://localhost:8000/) and open activities through the homepage or a direct path such as `http://localhost:8000/pages/strategic-pricing-game.html`.

A current browser and internet access cover the existing CDN dependencies. No Node.js, Python application, API service, or database is needed for the published site.

## Common changes

### Edit an activity

Open the relevant `pages/*.html` file. Most pages contain the markup, styles, data, and JavaScript together. Change the lesson text, scenarios, or defaults there and preview the result. See [pages/README.md](pages/README.md) for each activity's main code entry points.

### Add an activity

1. Create `pages/your-activity.html`. Start with a suitable existing activity or a small complete HTML document.
2. Keep calculations and interactions in the browser. Add clearly labeled inputs and describe the classroom assumptions.
3. In `index.html`, copy one visible card inside the activity grid. Set its relative `href`, heading, and short description. Use the existing `card-standard card-hover` classes.
4. Add the activity and any dependencies to `pages/README.md`.
5. Preview the homepage and direct activity URL; check controls, reset/export behavior if provided, browser console, and a narrow screen.

Optional home links inside activities should use `../index.html`. Put downloadable classroom files in an appropriately named directory, link to them with relative paths, and commit only material suitable for public distribution.

### Link the existing Solvix activity

The file `pages/solvix-new-product-simulator.html` already exists. To show it on the homepage, add a visible card pointing to that exact path. It is a separate case-specific simulator; do not replace the generic launch activity unless that is the teaching intent.

## Publish with GitHub Pages

For a new fork of this plain static site, the simple publishing setup is:

1. Open the fork's **Settings → Pages**.
2. Under **Build and deployment**, select **Deploy from a branch**.
3. Choose `main` and `/ (root)`, then save.
4. Check the **Actions** tab for the Pages build/deployment, then use the site URL shown in Pages settings.

The default project URL is `https://<owner>.github.io/<repository>/`. For this repository, the expected address is [https://howtobecalculated.github.io/MKT412/](https://howtobecalculated.github.io/MKT412/). A custom domain or different configuration can change it; Pages settings are authoritative.

For the original repository, the Pages API confirms branch-based publishing from `main`, `/ (root)`, at the address above, with status `built` during this handoff. There is no checked-in deployment workflow or site configuration file. Recheck the settings before changing the publishing source.

Changes publish after they reach the configured source branch and deployment succeeds. A feature branch or pull request alone does not publish a preview. If the original uses `main` as its source, merging a PR into `main` can update the public class site.

See [GitHub's publishing-source guide](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site) for the current settings.

## Troubleshooting

| Symptom | First check |
| --- | --- |
| Activity returns 404 | Exact filename and letter case; file committed; deployment succeeded; correct repository URL prefix. |
| New activity missing from homepage | Cards are manual. Add or update its link in `index.html`. |
| Styling/icons/charts missing | Internet access and CDN requests; check the browser console/network panel. |
| Dashboard reports a canvas already in use | See the documented duplicate Chart.js initialization in `pages/README.md`. |
| Published site still shows old content | Pages deployment status and source branch, then refresh the browser. |
| Progress disappears on reload | Current activities do not persist progress to a backend; use available CSV downloads during the session. |

Keep filenames stable for existing LMS links. For an unwanted published change, revert its commit through GitHub or a new PR and let Pages deploy the corrected version.
