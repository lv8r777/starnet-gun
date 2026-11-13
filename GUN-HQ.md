# GUN HeadQuarters

GUN HeadQuarters is Global Underground Network's own station. LV8R first called it GUN HQ, then renamed it GUN HeadQuarters on 2026-11-13 so the app has its own name: "GUN HQ" stays the name of the org pyramid on disk (root AGENTS.md, tech/, media/, office/, network/ in lv8r777/Maria). The org is GUN HQ; GUN HeadQuarters is the building it works in.

GUN HeadQuarters is a fork of StarNet (MIT, androoAGI/starnet), maintained on branch `gun-hq` of `lv8r777/starnet-gun`. LV8R named it on 2026-11-13, the same day the Paperclip trial was retired. GUN HeadQuarters is now the dispatch layer for the crew.

## Rename policy: the skin changes first, the plumbing last

Every user-facing name says GUN HeadQuarters, written exactly that way (capital H, capital Q): window title, boot mark, screen labels. The logo art is the exception: LV8R decided on 2026-11-13 that the logo reads just "GUN HQ" (it replaces the StarNet logo). Logo alt/aria text says GUN HQ to match what the mark shows. Internal identifiers keep their upstream names, so we can keep merging upstream fixes without conflicts across about 3,600 files.

### Renamed (phase 1, 2026-11-13)
- Window/tab title and boot mark (GUN HeadQuarters); splash logo (`frontend/assets/brand/gunhq-logo.png`, reads GUN HQ).
- Top-left chrome wordmark and the setup console titlebar (`frontend/assets/brand/gunhq-wordmark.svg`). This is a CSS mask, and its aspect ratio is pinned in `style.css` and `test/brand-wordmark-mask.test.js`.
- The art is a placeholder set in the house face VT323. Final logo art needs LV8R's sign-off. Regenerate it with `uv run --no-project --with fonttools --with brotli --with pillow python ~/.hermes/cache/scratch/gunhq/brand.py <repo> "GUN HQ"`, then copy the printed viewBox width/height into `style.css` `.logo-img` and `overseer-setup.css` `.cc-titlebar>.ov-wordmark` or replace the two files directly.

### Deliberately NOT renamed
- The provider id `starnet`, "STARNET CREDITS" and the "START WITH StarNet" hero. These name the vendor's managed-inference service, not our station.
- Package name `starnet-harness`, the `bin/starnet` CLI, `SKYNET_*` / `STARNET_*` env vars, and the app identifier `ai.skynet.harness`. Renaming the identifier would orphan every saved station, agent and key under `~/Library/Application Support/ai.skynet.harness`.
- The agent system prompts that say "StarNet harness". This is a phase-2 decision because QA claim tests lock them.

### Phase 2 (Maria, when LV8R wants it)
- Tauri `productName` and `install_manifest.rs::PRODUCT_NAME` change to "GUN HeadQuarters". The desktop bundle and updater feed then need to point at our own releases, not starnetos.com.
- Overseer and system-prompt wording, plus the website.
- Real logo art (reads GUN HQ). Logo input from LV8R (2026-11-13): "the other font type was fire, but whatever it's fine i don't really care." Read as: he liked the original StarNet wordmark lettering over the VT323 placeholder. Not a blocker; use it as the starting brief when the real logo is drawn.

## GUN crew in the Recruitment Bay (2026-11-13)
- `shared/specialties.js` opens BUILTINS with two fork-owned classes: `maria` (Maria, GUN Tech) and `gus` (Gus, GUN Media). Summoning one from the bay creates a seat whose purpose points at the real soul files in lv8r777/Maria and whose standing orders hand work to the real body (`claude -p` in the GUN HQ repo, or a work order). Seats front the agents; they never copy them (office/starnet/CREW.md).
- Seals reuse the engineer and producer emblems (`classicons.js`, codes MRA / GUS). `recruiter.js` keeps both out of the learned-work recommender, so they are only ever picked on purpose.
- `test/class-loadouts.test.js` pins the roster as the 35 upstream classes plus `GUN_CREW`, with the GUN crew first.
- The sidecar reads the class list at boot, so RAVEN's `team.summon` sees the new classes only after a sidecar restart. The bay sees them on a window reload.

## Running
The live station is `node sidecar/index.js` from this checkout on 127.0.0.1:8787. The frontend has no build step, so a window reload picks up frontend changes. Keep `LICENSE` and the upstream copyright notice; MIT requires it.
