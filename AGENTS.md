# Offline Voxel Pagoda Benchmark — Three.js variant

## Start here

For an implementation run, **read all of [`PAGODA_INSTRUCTION.md`](./PAGODA_INSTRUCTION.md) before planning or coding**. It is the complete task, visual brief, delivery contract, and rubric. `README.md` is the human-facing introduction, not an additional specification.

Then build the experience, not another proposal. Make artistic and engineering decisions yourself. The output requirements are fixed; the implementation is yours to solve.

## Working rules

- **Three.js is required.** Use the supplied `vendor/three.cjs` (r180), optionally `vendor/OrbitControls.js`, and include the MIT licence text from `vendor/LICENSE` in the deliverable. Integrating the library for direct-file use is part of the task. Do not obtain another build, addon, runtime library, or asset from elsewhere. A missing core build or licence is a blocker; the controls addon is optional.
- **Deliver offline.** Prefer one self-contained `index.html`; a complete folder/ZIP is also valid. Opening the artifact directly must work in a fresh browser session without internet, installation, a server, or changed browser security settings. All runtime dependencies and the Three.js licence must travel with it.
- **Work in this repository.** Do not inspect other benchmark variants or solutions, search the host or other projects for dependencies, or delegate implementation to sub-agents.
- **No online research or artifact downloads.** Author the scene and use the supplied runtime code. Do not install build tools or artifact dependencies. Existing local development tools are allowed; §6 of the brief defines the sole installation exception for dev-only browser testing under `.devtools/`.
- **Preserve the benchmark during an implementation run.** Do not modify `README.md`, `AGENTS.md`, or `PAGODA_INSTRUCTION.md`, or change the requirements to fit your output. Put implementation notes in `IMPLEMENTATION.md`.
- **Deliver the full core; aim for every bonus.** Protect the five-story voxel pagoda, garden composition, and reliable operation. Rich lighting, water, skies, vegetation, particles, and a beautiful interface are welcome when they improve the experience. The brief prescribes no rendering technique or UI template.
- **Inspect and refine.** Use harness-exposed browser tools, runner-provided executable paths, or ordinary command-availability checks. Do not scan the filesystem or create containers/services to obtain a browser. Optional local testing setup is governed by §6. Test only your own artifact or its local development URL; final portability evidence must come from direct-file use.
- **Report evidence honestly.** Actually view captured images when possible. A canvas, screenshot path, or syntax check alone does not establish visual quality. Distinguish checks performed, failures observed, and checks unavailable—including direct-file behavior and audible musical quality. Missing testing tools do not excuse a missing artifact.

## Deliver

Write `index.html`, any required shareable companion files, and a concise `IMPLEMENTATION.md` as specified in the brief. Exclude development tools from the distribution. The final reply should name the entry and shareable files, list implemented controls/bonuses, summarize actual verification, and disclose limitations. Do not merely print HTML into chat.
