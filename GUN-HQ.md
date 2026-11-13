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
- Real logo art (reads GUN HQ).

## Running
The live station is `node sidecar/index.js` from this checkout on 127.0.0.1:8787. The frontend has no build step, so a window reload picks up frontend changes. Keep `LICENSE` and the upstream copyright notice; MIT requires it.
