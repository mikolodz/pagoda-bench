# Stillwater Pagoda — Offline Voxel Diorama Benchmark (Three.js variant)

A self-contained front-end graphics benchmark for AI agents (or humans): build a beautiful
five-story **voxel pagoda garden** that runs offline from a double-clicked `index.html`,
rendered with **Three.js bundled from local disk**. No network access, no build step, no CDN,
no installation for the recipient.

The scene — not the interface — is the product. The brief is deliberately long because the
interesting failures here are subtle: a canvas is not a scene, a localhost load is not
portability, and a slider that changes a CSS background is not a lighting model.

## Run the benchmark

1. **Clone** this repo and `cd` into it.
2. **Start your agent inside this directory**, so it picks up `AGENTS.md` automatically — e.g.
   [`pi`](https://github.com/earendil-works/pi), Claude Code, Codex, or any coding agent that
   reads repo-local instruction files.
3. **Prompt it with one line**, e.g.
   `Read AGENTS.md and PAGODA_INSTRUCTION.md, then implement the benchmark.`
4. The agent writes `index.html` (the artifact) and `IMPLEMENTATION.md` (its notes).
5. **Open `index.html` by double-clicking it** — no server, no internet — and review the result
   against the rubric in §7 of the instruction file.

That is the whole setup. Nothing needs to be downloaded or installed: Three.js r180 ships in
`vendor/`.

## What is in the box

| Path | Role |
|---|---|
| `PAGODA_INSTRUCTION.md` | The complete task: brief, art direction, offline recipes, bonuses, build stages, verification checklist, 100-point rubric. Read it in full. |
| `AGENTS.md` | Agent working rules: no web or downloads for the artifact, library comes from `vendor/`, no host filesystem wandering, deliverables. |
| `vendor/three.cjs` | Three.js **r180**, CommonJS build (self-contained, no `require()`). Must be converted into the artifact — see §4 of the instruction. |
| `vendor/OrbitControls.js` | Matching `examples/jsm` addon (ES module, imports from bare `'three'`). Optional; rewrite per §4. The only addon supplied. |
| `vendor/LICENSE` | Three.js MIT licence — carry it into the distribution. |
