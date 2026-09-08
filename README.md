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
| `AGENTS.md` | Agent working rules: no web/downloads, library comes from `vendor/`, no host filesystem wandering, deliverables. |
| `vendor/three.cjs` | Three.js **r180**, CommonJS build (self-contained, no `require()`). Must be converted into the artifact — see §4 of the instruction. |
| `vendor/OrbitControls.js` | Matching `examples/jsm` addon (ES module, imports from bare `'three'`). Optional; rewrite per §4. The only addon supplied. |
| `vendor/LICENSE` | Three.js MIT licence — carry it into the distribution. |

## Scoring

Core 70 points (pagoda architecture 30, composition/atmosphere 20, runtime & delivery 20) plus
30 bonus points (camera 8, living world 8, time-of-day 7, procedural music 7). A blank page, a
non-3D substitute, CDN-loaded Three.js, hand-written WebGL standing in for Three.js, or a
network/server-dependent deliverable does not meet the brief regardless of bonuses.

Score the visible artifact and demonstrated interactions, **not** the agent's self-report.

## Comparing models fairly

Hold everything constant across runs: the same clone of this repo, the same agent tool access,
the same execution budget, the same browser and viewport (1440×900 plus a narrow pass), and the
same default camera and time-of-day. Then compare first frames, reverse angles, and night views.

## Notes

- **Implementation output is gitignored by design** (`index.html`, `IMPLEMENTATION.md`, `src/`,
  `tools/`, `shots/`, `deliverable/`), so `git status` stays clean and different variants or
  models are easy to diff. Commit on your own branch if you want to keep a result.
- `README.md` is the benchmark's front page; agent submissions belong in `IMPLEMENTATION.md`.
- `PAGODA_INSTRUCTION.md` §8 lists the public sources that informed the brief. They are
  provenance only — the benchmark is offline by contract, and no browsing is required or wanted.
- Brief and original code: MIT. Bundled Three.js: its own MIT licence, see `vendor/LICENSE`.
