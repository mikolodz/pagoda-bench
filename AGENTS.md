# Offline Voxel Pagoda Benchmark — Three.js variant

## Start here

(`README.md` explains how a human starts a run; you do not need it to do the work.)

For a benchmark implementation run, **read all of [`PAGODA_INSTRUCTION.md`](./PAGODA_INSTRUCTION.md) before planning or coding**. It is the complete task, visual brief, technical reference, and acceptance checklist. Then implement the experience—not another proposal. Make reasonable artistic decisions without asking the owner to design it for you.

This variant mandates **Three.js** as the rendering library. A hand-written raw WebGL pipeline is not an acceptable substitute here; custom GLSL is only allowed as `ShaderMaterial`/`onBeforeCompile` inside a Three.js scene. Three.js is supplied in `vendor/` and must be bundled into the artifact — never fetched from a CDN or installed.

## Working rules

- **Everything you need is inside this directory.** Do not wander the host: no searching the filesystem or other folders for Three.js, a browser, Playwright, or a bundler, and no reading other benchmark variants or solutions. If a required input is genuinely absent, report it as a blocker. The single exception is the explicitly scoped, optional dev-only browser-tooling install in `PAGODA_INSTRUCTION.md` §6, which stays inside `.devtools/` in this folder.
- Work in this directory. Preserve `README.md`, `AGENTS.md`, and `PAGODA_INSTRUCTION.md`; do not weaken the requirements or change the rubric to match your output. Your notes go in `IMPLEMENTATION.md`, never in `README.md`.
- **No online research or downloads for the artifact.** Do not use web search, remote documentation, package registries, CDNs, `npm install`, `npx`, remote browser navigation, or shell commands to obtain code or assets that end up in — or are loaded by — `index.html`. Reference URLs in the instruction are provenance, not tasks to visit. The only permitted install is the optional dev-only test tooling in §6, which must never reach the deliverable.
- **Three.js source:** use the files supplied here — `vendor/three.cjs` (Three.js **r180**, a CommonJS build with no `require()` calls) and, optionally, `vendor/OrbitControls.js` (an ES module whose `from 'three'` import must be rewritten), with `vendor/LICENSE`. Convert them into your deliverable using the shim/rewrite recipes in `PAGODA_INSTRUCTION.md` §4; that conversion is part of the benchmark. No other library, addon, or build tool is supplied. If these files are missing, report the blocker instead of downloading Three.js or reverting to raw WebGL.
- Use this brief, your existing knowledge, and files explicitly supplied in this benchmark directory. Do not assume any other library, asset, build tool, or global JavaScript object is available (no React, no GSAP, no loaders, no external textures, no bundler).
- Local file tools, shell execution, and **whatever browser automation is already available** — a Playwright/Puppeteer MCP or CLI your harness exposes, or a headless Chrome/Chromium binary on this machine — are allowed against your own artifact only. If none is available, that is a verification limit to state; §6 permits an optional `.devtools/` install if you need interaction or request evidence, and otherwise you fall back and disclose. Do not spawn sub-agents or delegate implementation.
- Prefer a single `index.html` containing its own CSS, app JavaScript, the **bundled Three.js source**, generated geometry/colors, and Web Audio sound generation. A folder/ZIP is acceptable only if its `index.html` also opens directly after extraction, without internet, installation, or a server, and includes the Three.js licence. See `PAGODA_INSTRUCTION.md` §4 for bundling routes that survive `file://`.
- Prioritize a beautiful, unmistakable, genuinely 3D voxel pagoda and reliable offline launch. Attempt all bonuses after the core scene works; do not trade the centerpiece for an elaborate settings panel.
- Inspect the rendered result if browser tooling is available — and actually look at the captured image, not just its filename (see `PAGODA_INSTRUCTION.md` §6 for tested headless-Chrome flags). Fix observed defects and retest. A canvas element, a screenshot path, or a passing syntax check alone is not evidence of visual quality.
- Never invent test results. If screenshots cannot be viewed, audio cannot be heard, or direct-file testing is unavailable, state those limits explicitly.

## Deliver

Write the runnable artifact to disk — entry `index.html`, with the Three.js build/licence inside it or alongside it — plus a concise `IMPLEMENTATION.md` (not `README.md`) with opening instructions, controls, implemented bonuses, the exact Three.js revision used, and verification/limitations. The final reply should identify the entry file and summarize what was actually checked. Do not merely print HTML into chat.
