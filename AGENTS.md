# Offline Voxel Pagoda Benchmark — Three.js variant

## Start here

For a benchmark implementation run, **read all of [`PAGODA_INSTRUCTION.md`](./PAGODA_INSTRUCTION.md) before planning or coding**. It is the complete task, visual brief, technical reference, and acceptance checklist. Then implement the experience—not another proposal. Make reasonable artistic decisions without asking the owner to design it for you.

This variant mandates **Three.js** as the rendering library. A hand-written raw WebGL pipeline is not an acceptable substitute here; custom GLSL is only allowed as `ShaderMaterial`/`onBeforeCompile` inside a Three.js scene. Three.js must come from **local disk** and be bundled into the artifact — never fetched from a CDN or installed.

## Working rules

- Work in this directory. Preserve these two instruction files; do not weaken the requirements or change the rubric to match your output.
- **No online research or downloads.** Do not use web search, remote documentation, package registries, CDNs, `npm install`, `npx`, remote browser navigation, or shell commands to obtain online code/assets. Reference URLs in the instruction are provenance, not tasks to visit.
- **Three.js source:** use the copy supplied in this directory (`vendor/three.module.min.js`, `vendor/three.module.js`, or `vendor/three.min.js`). If none is supplied, copy a `three` build already installed on this machine's local disk into your deliverable. That library copy is the one permitted read outside this directory; do not inspect sibling benchmark folders or their solutions. If no local copy exists, report that blocker explicitly instead of downloading Three.js or reverting to raw WebGL.
- Use this brief, your existing knowledge, and files explicitly supplied in this benchmark directory. Do not assume any other library, asset, build tool, or global JavaScript object is available (no React, no GSAP, no loaders, no external textures, no bundler unless one is already installed locally).
- Local file tools, shell execution, and **Playwright against your own local artifact** are allowed. Do not spawn sub-agents or delegate implementation.
- Prefer a single `index.html` containing its own CSS, app JavaScript, the **bundled Three.js source**, generated geometry/colors, and Web Audio sound generation. A folder/ZIP is acceptable only if its `index.html` also opens directly after extraction, without internet, installation, or a server, and includes the Three.js licence. See `PAGODA_INSTRUCTION.md` §4 for bundling routes that survive `file://`.
- Prioritize a beautiful, unmistakable, genuinely 3D voxel pagoda and reliable offline launch. Attempt all bonuses after the core scene works; do not trade the centerpiece for an elaborate settings panel.
- Inspect the rendered result if browser tooling is available, fix observed defects, and retest. A canvas element, screenshot path, or passing syntax check alone is not evidence of visual quality.
- Never invent test results. If screenshots cannot be viewed, audio cannot be heard, or direct-file testing is unavailable, state those limits explicitly.

## Deliver

Write the runnable artifact to disk — entry `index.html`, with the Three.js build/licence inside it or alongside it — plus a concise `README.md` with opening instructions, controls, implemented bonuses, the exact Three.js revision used, and verification/limitations. The final reply should identify the entry file and summarize what was actually checked. Do not merely print HTML into chat.
