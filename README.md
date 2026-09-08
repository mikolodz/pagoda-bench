# Stillwater Pagoda — Offline Voxel Diorama Benchmark (Three.js variant)

A self-contained front-end graphics benchmark for AI agents (or humans): build a beautiful
five-story **voxel pagoda garden** that runs offline from a double-clicked `index.html`,
rendered with **Three.js bundled from the supplied files**. The recipient needs no network,
server, installation, or build step.

The brief defines the scene, delivery contract, and observable behavior—not how to implement
them. Models choose their technical approach and art direction, from expressive trees and
atmospheric water to rich lighting and a polished interface. The pagoda garden remains the
centerpiece. The 100-point rubric awards 70 points for the core and 30 for interactive bonuses.

## Run the benchmark

1. **Clone** this repo and `cd` into it.
2. **Start your coding agent inside this directory.** The prompt below explicitly loads the
   repository instructions, whether or not the agent discovers `AGENTS.md` automatically.
3. **Prompt it with one line**, e.g.
   `Read AGENTS.md and PAGODA_INSTRUCTION.md, then implement the benchmark.`
4. The agent writes `index.html`, any shareable companion files, and `IMPLEMENTATION.md` (its notes).
5. **Open `index.html` by double-clicking it** — no server, no internet — and review the result
   against the rubric in §7 of the instruction file.

Three.js r180 ships in `vendor/`; no artifact dependency download is needed. Optional dev-only
browser testing tools are governed by §6 of the brief and never belong in the deliverable.
For model comparisons, fix tool access, versions, budget, and review conditions before running.

## What is in the box

| Path | Role |
|---|---|
| `PAGODA_INSTRUCTION.md` | The complete task: output requirements, art direction, implementation freedom, bonuses, verification, and 100-point rubric. |
| `AGENTS.md` | Agent entry instructions, working boundaries, and deliverables. |
| `vendor/three.cjs` | Three.js **r180**, self-contained CommonJS build. Integrating it for offline direct-file use is part of the task. |
| `vendor/OrbitControls.js` | Matching ES-module camera addon. Optional; the only addon supplied. |
| `vendor/LICENSE` | Three.js MIT licence—include it in the distribution. |
