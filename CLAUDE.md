# compaan-scripts

Custom JS for the Compaan Webflow site (`compaan-hoogstraten.be`), served by GitHub Pages from `main`.

| File | Loaded on | URL |
|---|---|---|
| `staging.js` | `compaan-space.webflow.io` | `https://matteofabbiani.github.io/compaan-scripts/staging.js` |
| `index.js` | production domains | `https://matteofabbiani.github.io/compaan-scripts/index.js` |

## ⛔ Strict rule

- Editing and pushing `staging.js` → **staging only**. Safe default.
- Changing `index.js` in any way (`npm run promote`, a direct edit, a revert) and pushing it → **PRODUCTION**, live for all visitors within ~10 minutes. **Never without the user's explicit permission, given per release in the current conversation.** "Deploy", "push", "save", "update the code" all mean STAGING ONLY. One approval covers one release.
- Never stage `index.js` in a commit by accident: commit with explicit paths, not `git add -A`.

## Working notes

- Every edit goes into `staging.js` first; run `npm run check` before pushing. Pages rebuilds in about a minute; the staging loader adds a timestamp so no cache applies.
- Production is cached for 10 minutes by GitHub Pages (not configurable). A rollback takes the same time to reach returning visitors.
- The code expects these globals, loaded by Webflow before it: `gsap`, `ScrollTrigger`, `CustomEase`, `Lenis`, `Swiper`, `Hls`.
- The file is loaded after `DOMContentLoaded`: code added here must not wait for that event (use a `document.readyState` check).
- CSS stays in Webflow embeds. Class and attribute names the scripts toggle (`modal--closing`, `offset-swapped`, `data-marquee-status`, …) are styled there; do not rename them.
- `webflow-loader.html` is the copy of the snippet in Webflow → Site settings → Custom code → Footer.
