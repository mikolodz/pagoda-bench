# Stillwater Pagoda — Offline Voxel Diorama Benchmark (Three.js variant)

> **Library variant:** this run uses **Three.js**, not a hand-written WebGL pipeline. Three.js must be bundled from local disk into the artifact (§2.4, §4). Everything else in this brief is the same benchmark.

## 1. Your task

You are a creative graphics programmer and voxel environment artist. **Build a beautiful, interactive, genuinely three-dimensional pagoda garden that opens in a web browser, rendered with Three.js.** Write the working files, not a design proposal or a code block in chat.

Imagine a collectible miniature: a five-story lacquered pagoda above a jade pond, deep stepped roofs catching warm evening light, clustered blossom trees, a small bridge, and tiny lanterns. The first frame should make someone want to explore it. The scene—not the interface—is the product.

**Priority order:** unmistakable pagoda silhouette → excellent composition and voxel craftsmanship → reliable rendering and offline delivery (which includes bundling Three.js into the artifact itself) → camera interaction → environmental animation → time-of-day control → original ambient music. Aim to implement every bonus, but preserve a polished core if resources become tight.

This is a custom benchmark, not a claim to reproduce any public benchmark's hidden tests. There are no secret APIs or voxel-count quotas. Visual quality and observable behavior matter more than claimed numbers.

## 2. Non-negotiable delivery contract

1. **Entry point: `index.html`.** Prefer one file with inline CSS, JavaScript, the bundled Three.js source, and all generated content. Sharing that file must be sufficient.
2. A folder/ZIP alternative is acceptable only if all dependencies are included using relative paths, and double-clicking its `index.html` after extraction works. A server, installation, build command, account, or network connection must not be required by the recipient. Do not include `node_modules` as your distribution — ship only the Three.js build (and any addon) you actually use, plus its licence.
3. **Offline from a fresh browser session.** No externally loaded scripts, fonts, images, textures, models, audio, analytics, API calls, or first-run downloads — **including the Three.js library itself**. Procedurally generated in-memory textures/buffers are fine. A warm browser cache is not portability. No downloaded music hidden as base64; compose and synthesize the sound yourself.
4. **Three.js is required and comes from `vendor/` in this folder.** Use `vendor/three.cjs` (Three.js r180, CommonJS build) and, if you want ready-made camera controls, `vendor/OrbitControls.js`; carry `vendor/LICENSE` into the distribution. Converting those files into your artifact is part of the task — see §4. Searching the machine for another Three.js build, `npm install`, `npx`, package registries, CDNs, remote `<script src="https://…">`, remote `import`, and importmaps are all out. Include the Three.js MIT licence text in the final distribution and state the exact revision used (`three@0.180` / r180 — read `REVISION` from the vendored file) in `IMPLEMENTATION.md`. If the vendored files are missing from your clone, report that blocker rather than downloading Three.js or switching to raw WebGL. No other library is supplied or permitted.
5. Use actual 3D geometry rendered **through Three.js**: real projection, depth occlusion, materials, and lighting. **Not** a flat illustration, prerecorded scene, CSS stack of roof shapes, or a 2D canvas picture disguised with a rotating DOM element. Do not hand-write a raw WebGL pipeline as a substitute for Three.js; custom GLSL is fine only as `ShaderMaterial` or `onBeforeCompile` patches inside the Three.js scene.
6. The pagoda and environment must visibly use a coherent voxel/block construction. Cubes, grid-aligned cuboids, and merged coplanar voxel faces are fine. A smooth building with a pixelation filter is not voxel architecture.
7. Show the scene immediately without a mandatory splash-screen click. Audio alone requires opt-in. Provide a useful visible error if graphics initialization fails, rather than an empty page — detect it explicitly (for example `canvas.getContext('webgl2')` returning `null` or the `WebGLRenderer` constructor throwing) and render a readable message plus the failure reason.
8. Include a concise **`IMPLEMENTATION.md`** (do not overwrite this repository's own `README.md`): how to open/share, controls, implemented bonuses, supported/tested browser information, and honest verification limits. If you deliver a folder or ZIP rather than one file, put a copy of it in that folder as its `README.md`. The HTML must work without the notes file or these prompt files.

**Important browser trap:** “one HTML file” does not mean “offline,” and Three.js is the usual way this breaks. Remote imports, importmaps, `three/addons/...` URLs, and CDN `<script src>` tags still download code at runtime. Relative or bare ES-module imports (`import * as THREE from './three.module.js'`, `from 'three'`) and `fetch()` of neighboring files can also fail under `file://` origin rules even though they work over `http://localhost`. The safe default here is Three.js bundled **into the artifact itself** (§4): a classic `<script>` IIFE bundle exposing `window.THREE` — the recommended route for the supplied CommonJS build — or one inline `<script type="module">` with no remaining `import`/`export` statements, plus inline app code, generated geometry/colors, and Web Audio. Do not solve portability by telling the recipient to disable browser security, run localhost, or install an app. A local server is allowed for development/testing only.

## 3. Art direction: make the miniature worth looking at

### Hero architecture

Create a **Japanese-inspired five-story pagoda**, interpreted artistically rather than presented as an exact historical reconstruction:

- Five distinct, stacked roof tiers, each narrower than the tier below. A useful starting ratio is `roofWidth(i) = baseRoofWidth * 0.86 ** i`, for `i = 0..4`.
- Tall enough to feel elegant, not a squat stack of pancakes. Leave visible timber/wall space between roofs. Avoid a skyscraper with tiny roof ledges.
- Deep overhanging eaves; stepped roof slopes with a shallow concave profile and gently lifted corners. The outline must read at thumbnail size. Neither five flat plates nor five plain pyramids is sufficient.
- Vermilion structural posts, dark timber beams, warm ivory wall panels, recessed doors/windows, and small bracket-like blocks supporting the eaves. Include a legible entrance and stairs on a stone plinth.
- A slender, stacked-ring **sōrin finial** above the top roof. The finial is the crown, not the name of the roof curve. Keep it upright and visually delicate.
- Detail on the sides and back as well as the front. No floating roofs, detached pillars, coplanar flicker, or foliage hiding a missing floor.

Think in three scales: **large** silhouette and tier proportions; **medium** beams, eaves, windows, stairs; **small** roof edging, brackets, stone variation, lantern apertures. Small details cannot rescue a weak silhouette.

### Composition

Use a bounded garden/island diorama, not an endless empty plane. Give its base visible soil/stone depth and an intentional outline.

- A path should lead the eye from the foreground toward the entrance.
- Add a pond with a shaped shoreline and a small bridge or stepping-stone crossing.
- Frame the pagoda asymmetrically with a few deliberately placed trees. Combine blossom clusters with darker foliage for contrast; do not scatter identical lollipop trees uniformly.
- Include a few convincing small props: stone lanterns, rocks, moss, bamboo, or reeds. Choose details that reinforce the composition rather than filling every gap.
- The default camera is an elevated three-quarter view, showing two pagoda faces, the pond, and the full finial. The tower should dominate the image without clipping. Leave some quiet negative space around its outline.
- The scene should remain convincing from the opposite side. Avoid a single-angle stage set.

### Palette and light

Suggested palette; tune it into a coherent image rather than using every color equally:

| Material | Starting colors |
|---|---|
| Lacquer / timber | vermilion `#B94735`, teak `#4A2C23` |
| Roofs | deep jade `#244B45`, patina `#477B68` |
| Walls / accents | warm ivory `#E8D9B8`, muted gold `#D8AF62` |
| Blossoms | dusty pink `#EFA7B5`, pale blush `#F7D2D5` |
| Ground | moss `#667348`, stone `#8E9390` |
| Water | deep teal `#326D73`, restrained glints `#A5D7CE` |

Use a small family of neighboring shades per material, distributed with seeded randomness. Use a fixed default seed for procedural layout and colors so repeated launches give a reproducible composition. No per-frame random color flicker, rainbow confetti, or thick black outlines around every cube. Voxel faces should remain crisp and readable; do not blur away the craft.

Use directional warm light, cooler ambient fill, darker undersides/recesses, and convincing contact/cast shadows. A simple, reliable shadow/contact approximation is preferable to broken advanced effects. Subtle fog or distance desaturation can separate layers. Avoid blown-out bloom, washed-out walls, and black silhouettes at night.

### Interface

Keep the garden full-viewport. Use a small title, discreet control hints, and one compact, readable control strip. No marketing page, dashboard cards, giant side panel, fake loading sequence, or statistics pasted over the pagoda. Local serif/system font stacks are fine; do not fetch fonts.

Use real labeled buttons and range inputs, visible focus states, and adequate contrast. Controls must not overlap at narrow widths. An overlay must not invisibly swallow all canvas input. Only show controls that actually work.

## 4. Offline technical field guide

These are implementation recipes for a Three.js scene. Choose the simplest architecture that delivers the image reliably; do not rebuild an engine Three.js already gives you.

### Getting and bundling Three.js offline

- **The library is already in this folder.** `vendor/three.cjs` is Three.js **r180** (`REVISION === '180'`) as a self-contained **CommonJS** build (unminified, ~2 MB, zero `require()` calls, zero top-level `import`). `vendor/OrbitControls.js` is the matching `examples/jsm/controls/OrbitControls.js` **ES module**. `vendor/LICENSE` is the MIT text. These three files are the entire permitted dependency set; confirm the revision from the file itself rather than trusting this sentence.
- **Do not look anywhere else on the machine.** There is no `three.module.js`, `three.min.js`, `three.core.min.js`, or `node_modules` tree here, and you are not to search for one. If you believe something you need is missing, report it as a blocker instead of downloading, installing, or substituting raw WebGL.
- **Never** fetch the library at runtime or build time: no CDN, jsdelivr/unpkg/skypack, importmap, `three/addons/...` remote path, `npm install`, `npx`, or package registry. `npx` counts as a download attempt even if it appears to resolve locally.
- Ship the licence (MIT text) and state the exact revision in `IMPLEMENTATION.md`.
- **Bundling routes** — the supplied build is CommonJS, so an ESM-only recipe does not fit it. Pick one route and verify it by double-click:
  1. **Classic-script global bundle (recommended for `vendor/three.cjs`):** a browser has no `require`, so give the CJS body a module shim inside an IIFE and expose it as `THREE`:

     ```html
     <script>
     globalThis.THREE = (function () {
       var module = { exports: {} }, exports = module.exports;
       /* entire contents of vendor/three.cjs pasted here, 'use strict' line kept inside */
       return module.exports;
     })();
     </script>
     ```

     The build only ever *writes* `exports.X = X`, so the shim is sufficient. Load your own app as a plain `<script>` afterwards and use `THREE.Scene`, `THREE.REVISION`, and so on. The IIFE plus `var` also keeps the build's ~400 top-level names out of global scope, which is what makes it safe to concatenate with your own code.
  2. **Single inline module:** only if you are working from a module-style build. Such a file ends in one `export { a as X, … }` list with no sibling imports — delete that list, or turn it into `const THREE = { X: a, … }`, and leave **no `import` or `export` statement anywhere in `index.html`**. Do **not** paste `vendor/three.cjs` into a `<script type="module">` and expect `exports.X = …` to resolve.
  3. **OrbitControls:** rewrite `vendor/OrbitControls.js` mechanically before use — replace its `import { Controls, MOUSE, … } from 'three'` block with `const { Controls, MOUSE, … } = THREE;` (keep every name; `OrbitControls extends Controls`) and replace the trailing `export { OrbitControls };` with a plain declaration, then load it as a classic `<script>` after THREE. A bare `'three'` specifier would need an importmap, which is not allowed.
  4. **Folder deliverable:** allowed only when every runtime load is a **classic** `<script>` (no module scripts, no bare or relative ES-module imports, no importmap) and the whole folder opens by double-click offline.
- **No bundler is needed or expected.** The conversions above are mechanical text edits; do not install esbuild, rollup, or any other tool to avoid them.
- **Name-collision caution:** builds can collide on top-level names when concatenated into one scope. The IIFE shim in route 1 avoids this; if an inline-module route throws a redeclaration error, switch to route 1 rather than debugging Three.js internals.
- **`vendor/OrbitControls.js` is the only addon supplied.** There is no `BufferGeometryUtils`/`mergeGeometries`, no `EffectComposer`, no loader, no texture — implement equivalent behaviour yourself. Never load an addon from a `three/addons` URL.

### Voxel geometry and rendering in Three.js

- Use Three.js for the renderer, scene graph, camera, materials, lights, and geometry. Establish one world-up convention (Three.js default: **Y up**) and one base grid size. Build reusable `Group`s for the pagoda, terrain, trees, props, and animated elements.
- Prove one lit `BoxGeometry` cube with a `DirectionalLight` plus ambient/hemisphere fill renders correctly — depth ordering, resize, shadow if used — before generating the entire world. Use `renderer.info.render.calls` / `.triangles` for honest reporting instead of inventing numbers.
- Build cuboid faces with consistent winding and outward normals. Keep lighting normals and the light direction in the same coordinate space. Use flat face normals and `flatShading: true` on `MeshLambertMaterial`/`MeshStandardMaterial` so voxel faces stay crisp; smooth normals and heavy roughness/metalness blur away the craft.
- Batch. Merge same-material blocks into a few `BufferGeometry` batches (write the merge yourself — `mergeGeometries` is **not** supplied) or use `InstancedMesh` with per-instance color via `setColorAt`. **Do not create one mesh per voxel.** Remove faces between neighboring opaque voxels when practical. Merge terrain surfaces without erasing visible block steps and color variation.
- Mind index capacity: unsigned 16-bit indices address only vertices `0..65535`. Three.js uses 32-bit indices when the context supports them (`renderer.capabilities.isWebGL2` or `OES_element_index_uint`), but split batches deliberately rather than pushing one huge buffer into index wrap and exploding triangles.
- Keep dynamic foliage/petals/water in separate meshes, `InstancedMesh`, or `Points` groups from static architecture. Animate instance matrices, small group transforms, or shader parameters (`material.onBeforeCompile` or a compact `ShaderMaterial`) rather than rebuilding the pagoda each frame. No general-purpose game engine, physics system, editable voxel world, or huge 3D occupancy grid is needed.
- Custom GLSL must match the context Three.js gives you (`renderer.capabilities.isWebGL2`): GLSL ES 3.00 on WebGL2 versus GLSL ES 1.00 on the WebGL1 fallback. Do not mix attribute/varying/output syntax, and remember `onBeforeCompile` patches Three.js's own shader chunks rather than replacing them.
- Color management: Three.js converts sRGB hex values into the working color space automatically (`THREE.ColorManagement.enabled` default `true`, `renderer.outputColorSpace = THREE.SRGBColorSpace`). The palette hexes in §3 are sRGB design values; do not double-convert them.
- Water need not be physically simulated. A mostly opaque tinted surface (`MeshStandardMaterial` with animated normals/roughness or a gentle vertex ripple) with restrained glints is robust. If using transparency, render opaque geometry first and handle transparent ordering/depth writes intentionally (`renderOrder`, `depthWrite: false`). Avoid overlapping translucent cubes that obscure the fish and shoreline.

### Lights, shadows, and fog

- Use a `DirectionalLight` for the warm key light, `HemisphereLight` (or `AmbientLight`) for cooler fill, and darker undersides/recesses via geometry, vertex color, or an occlusion term rather than heavy post-processing. Add depth cues before expensive effects.
- If using shadow maps: `renderer.shadowMap.enabled = true`, `directionalLight.castShadow = true`, a tight orthographic shadow camera fitted to the diorama bounds, a bounded map size (for example 1024–2048), and `castShadow`/`receiveShadow` only where they help. Re-fit the shadow camera and mark `shadow.camera.updateProjectionMatrix()` / `shadow.map.needsUpdate` when the sun direction changes materially. A simple contact-shadow blob or baked vertex darkening is preferable to broken shadow maps.
- Use `scene.fog = new THREE.Fog(...)` (or `FogExp2`) for subtle distance desaturation, and update its color with the time-of-day keyframes while keeping night legible.
- Avoid bloom/`EffectComposer` dependencies. Prefer emissive materials (`emissive`, `emissiveIntensity`) on lantern and window blocks for glints. Do not trade reliable launch for post-processing.

**Roof construction recipe:** define each floor in local coordinates. Build thin square stepped bands that become narrower and higher toward the center. Near the outer edge, introduce a shallow dip followed by a small raised lip; lift corner cells a little more than edge midpoints. Quantize heights to the voxel grid. Add a darker underside band and supports, then place the next floor above the roof's actual highest point. Verify the side profile and inter-floor clearance visually. Do not fill the entire roof bounding box solid or cover all walls with huge eaves.

### Frame loop and performance

Use one `requestAnimationFrame` loop, elapsed time in seconds, and a capped delta after tab resume (for example `min(delta, 0.05)`). `THREE.Clock` is fine as long as you keep a separate accumulated simulation clock so pausing actually freezes environmental motion. Camera input may remain active while the environment is paused.

When the canvas/container changes, update **both** the renderer and the camera: `renderer.setSize(width, height, false)` (or `true` when Three.js should manage canvas CSS), `renderer.setPixelRatio(Math.min(devicePixelRatio || 1, 1.5))`, and `camera.aspect = width / height; camera.updateProjectionMatrix()`. Do not hard-code the initial window size.

Avoid allocating `Vector3`/`Color`/`Matrix4` objects, creating geometries/materials/textures, adding event listeners, or growing particle pools every frame; reuse module-level temporaries and update instance matrices in place. Keep `renderer.info` counts stable across frames rather than climbing.

Target smooth interaction on a normal modern laptop; approximately 30+ FPS at 1440×900 is a useful target, not a universal guarantee. Measure on the actual available browser and report its context. Prefer reducing pixel ratio/particles before removing the architectural detail. Do not display fabricated FPS, voxel counts, or draw-call numbers.

## 5. Bonuses — implement real behavior, not decorative controls

### A. Mouse camera: orbit, zoom, pan, reset

- Left drag: orbit around the scene target. Wheel/trackpad scroll: zoom in/out.
- Right drag **or** Shift+left drag: pan in camera-relative screen directions. Provide the Shift alternative for users without a convenient right button.
- A visible **Reset view** button restores the carefully composed default. Optional idle rotation must stop on interaction and be disableable; never fight the user's camera.
- Clamp zoom and elevation so users cannot turn the scene upside down, pass through the ground, or lose the subject irretrievably. Use sensible pan bounds.
- Scope pointer/wheel handling to the canvas. Capture the active pointer while dragging; clean up on `pointerup`, `pointercancel`, and lost capture. Suppress the context menu on the canvas only. A wheel handler that calls `preventDefault()` must be registered with `{ passive: false }`.
- Dragging a time or volume slider must not rotate the scene. Keyboard-operable controls are required; optional keyboard camera controls and one-finger orbit/two-finger pan-pinch are welcome.

**Three.js route:** `OrbitControls` (`vendor/OrbitControls.js`, converted per §4 — never from a remote `three/addons` URL) covers most of this: attach it to the canvas element so input stays scoped, `enableDamping = true`, `minDistance`/`maxDistance` for zoom clamps, `minPolarAngle`/`maxPolarAngle` for elevation clamps, `enablePan`/`screenSpacePanning`/`panSpeed`, `enableZoom`, `mouseButtons`/`touches` mapping, and `saveState()` + `reset()` for the **Reset view** button. Its default right-drag already pans; still provide the Shift+left alternative (map `mouseButtons.ROTATE`/a small handler). Clamp `controls.target` inside garden bounds yourself, stop idle rotation on interaction, and never let an animation fight the user's camera.

**Custom route** (if OrbitControls is not supplied locally and cannot be bundled): implement the same behaviour yourself with pointer capture and Three.js maths. Retain a target `T`, distance `r`, yaw `a`, and polar angle `b` measured from +Y; camera position is `T + r * [sin(b)*sin(a), cos(b), sin(b)*cos(a)]` — equivalently `camera.position.setFromSphericalCoords(r, b, a).add(T)` plus `camera.lookAt(T)`. Clamp `b` away from the poles and below a ground-crossing angle, clamp `r`, and pan `T` along the camera's right/up vectors scaled to distance and viewport size. Use `PerspectiveCamera` with a moderate field of view (about 45–60°) or `OrthographicCamera` with zoom; both can be real 3D. Do not use any control you cannot bundle offline.

### B. Wind and a living garden

Implement at least two complementary layers of environmental motion: for example gently swaying canopy branches plus drifting petals, and/or pond ripples plus swimming koi. Subtle lantern or hanging-bell movement is another option.

Motion should have differing phases and amplitudes. Anchor trees at their trunks, sway foliage around branch pivots, and keep the pagoda/terrain rigid. Use a bounded/recycled particle pool and elapsed-time-based motion. In Three.js this means rotating trunk-anchored `Group`s, updating `InstancedMesh` matrices in place (`instanceMatrix.needsUpdate = true`), or animating a bounded `Points`/`InstancedMesh` petal pool — not rebuilding geometry every frame. Leaves should drift rather than vibrate, water should ripple rather than bob as a solid slab, and fish should stay inside the pond.

Include an **Animate/Pause** toggle. Respect `prefers-reduced-motion` by starting environmental/automatic camera animation paused or substantially reduced. Manual camera and time controls must still work.

### C. Time-of-day bar

Add a clearly labeled **Time of day** slider spanning the full 24-hour cycle with a readable `HH:MM` value and useful dawn/noon/dusk/night markers. Start at an attractive golden-hour setting, approximately 17:30. Scrubbing should update the scene immediately.

The slider must change actual scene lighting: sun direction and intensity, ambient/sky/fog colors, and lantern/window emission. In Three.js that means `directionalLight.position`/`.intensity`/`.color`, `hemisphereLight`/`ambientLight` colors, `scene.fog.color`, `scene.background`, and material `emissive`/`emissiveIntensity` — plus a coherent shadow-camera re-fit if shadows are used. A changing CSS background with an unchanged building is not enough. Night should remain legible in cool moon/ambient light with warm lantern accents. Interpolate smoothly, including across midnight; do not illuminate the underside with a below-horizon sun.

A simple cycle uses `sunElevation = sin(2π * (hour - 6) / 24)` (sunrise near 06:00, noon maximum, sunset near 18:00). Use a smoothly clamped daylight amount to drive light/sky transitions. If shadows are implemented, update them coherently. Artistic keyframes for 00:00, 06:00, 12:00, 18:00, and 24:00 can supply colors, with matching endpoints.

Optional auto-advance needs a separate toggle, an unhurried multi-minute cycle, and no conflict with manual scrubbing. Pausing the garden should also pause automatic day progression, not the slider.

### D. Original generated ambient motif

Compose a quiet, pleasant, recognizable musical phrase using **Web Audio synthesis only**. “Baked in” means the composition, synthesis, and any generated buffers live in the artifact—not that an external sound file is embedded.

- Default sound **off**. Provide an explicit **Enable sound / Mute** control and volume slider. Create or resume one `AudioContext` from a user click, await successful resume, and reflect its real state in the UI. The scene must still work if audio is unavailable.
- A useful starting point is a sparse 8- or 16-note phrase at 60–76 BPM using D, E, G, A, B across one or two octaves. Include rests and a returning motif; not endless random beeps. This is an artistic pitch set, not a claim of historical musical authenticity.
- Convert MIDI pitch to Hz using `440 * 2 ** ((midi - 69) / 12)`. Build a soft bell/pluck from sine/triangle oscillators and a few quieter harmonics with gentle attack and decay envelopes. A restrained drone, filtered generated noise, or a low-feedback delay can add atmosphere.
- Schedule notes against `audioContext.currentTime`. A scheduler waking roughly every 25 ms and scheduling about 0.1 seconds ahead is a practical pattern; do not use rendering frames as the musical clock. When resuming after a hidden tab/suspension, rebase the next-note time instead of rapidly playing every missed note.
- Avoid clicks and clipping: low master gain, short gain ramps, bounded polyphony, and no exponential ramp to exactly zero (use a small positive floor, then stop). Stop/disconnect finished voices. Repeated sound toggles must not create duplicate contexts, schedulers, or overlapping copies of the composition.
- Mute must silence the whole graph, including effect tails. Handle page visibility deliberately (for example suspend audio when hidden); never burst into loud playback on return. Keep sound independent from the visual animation toggle and document the behavior.

Bonus audio is earned by a functioning, musically intentional result—not merely by constructing an `AudioContext`. If you cannot listen in your environment, distinguish functional checks from unverified sound quality.

## 6. Build and inspect in useful stages

1. Establish the Three.js source and bundling route (§4), then the offline entry point. Prove one lit cube renders through `file://` — geometry, depth, lighting, resize — before adding thousands of blocks.
2. Build the complete five-tier pagoda. Inspect the silhouette, roof profile, clearance, and finial before decorating.
3. Compose the garden, materials, light, and default camera. Refine the still image until it is attractive.
4. Add camera controls and bonuses incrementally, keeping the existing scene working.
5. Inspect actual browser output, fix the most visible problems, and repeat. Reserve time for the final offline check and `IMPLEMENTATION.md`.

### How to actually see your result

Use browser automation that is **already in front of you**: a Playwright or Puppeteer MCP/CLI that your agent harness already exposes, or a headless Chrome/Chromium binary already installed on the machine. Point it only at your own artifact or its local development URL.

**Do not go hunting for a tool.** No filesystem searches for a stray Playwright install, no reading other projects or sibling folders for one, no new container or service just to obtain a browser. Use what is already in front of you. If nothing is available, either record the missing checks as verification limits and keep building — or use the explicitly scoped optional install in “Optional: local Playwright” below. A missing screenshot is not permission to skip the working artifact, and not permission to claim a review you did not do.

A bare headless-Chrome capture loop that needs no installation and stays offline:

```bash
CHROME=/path/to/an/already-installed/chrome   # a local Google Chrome or Chromium binary
"$CHROME" --headless=new \
  --window-size=1440,900 --virtual-time-budget=6000 \
  --screenshot="$PWD/shot-default.png" \
  "file://$PWD/index.html"
```

- **Never add `--disable-gpu`.** It can leave WebGL unavailable, so a *correct* scene renders nothing but your failure panel and you will chase a phantom bug. Observed on Chrome 152: `--headless=new` alone, and `--use-gl=angle --use-angle=swiftshader`, both produce a lit WebGL frame, while `--disable-gpu` and `--use-gl=egl` produce a blank canvas plus the error panel. If you need software rasterisation, use `--enable-unsafe-swiftshader` or `--use-angle=swiftshader`.
- `--virtual-time-budget` lets the animation loop and deferred initialisation run before capture; without it you may screenshot frame zero.
- Capture the states you must judge: the default view, a narrow viewport such as `--window-size=390,844`, a reverse angle and a night view (drive these with a temporary dev camera/time value, or a script that dispatches real input), and two frames several seconds apart to compare motion.
- **Then look at the pixels.** If your harness can attach an image file to your context — a file-reading tool that supports images (Pi's `read`, Claude Code's `Read`, and similar do), or an MCP browser tool that returns the image itself — open the screenshot and review it. A file path, a byte count, a DOM snapshot, or "the canvas exists" is not visual review. If you truly cannot view images, state that limit and fall back to the checks below.
- `--dump-dom` is a **weak** probe: it prints hidden markup too, so grepping for your error-panel text false-positives on a working page (confirmed here — the failure string appears in the DOM of a correctly rendering build). Use it only alongside a screenshot or a computed-style visibility check.
- Playwright/Puppeteer, when already available, is better for interaction and console capture: subscribe to `console`/`pageerror`, drive `page.mouse` drags and wheel for orbit/zoom/pan, then `page.screenshot({ path })` and view that file. If none is available, see the optional local install below.
- A local server (`python3 -m http.server`) is convenient for iteration but **does not prove double-click portability**; always finish on a real `file://` load. Never use `--allow-file-access-from-files` or similar flags to paper over `file://` rules — a real double-click has no such flags, so anything needing them fails the brief.

### Optional: local Playwright for interaction and request evidence

The checks above need input simulation and request counts that a screenshot CLI cannot give you. Prefer the zero-install route when a browser already exists. Install only if you genuinely need orbit/pan/zoom simulation, console errors, or outgoing-request evidence — and keep every byte of it inside this directory:

```bash
mkdir -p .devtools
export npm_config_cache="$PWD/.devtools/npm-cache"          # never ~/.npm
export PLAYWRIGHT_BROWSERS_PATH="$PWD/.devtools/browsers"   # never ~/Library/Caches
npm install --prefix .devtools playwright-core              # no browser download
```

Then drive the **already-installed** Chrome/Chromium binary with `chromium.launch({ executablePath })`, so nothing is downloaded at all. Only if no local browser exists should you let `npx playwright install chromium` fetch one — and with the export above it lands in `.devtools/browsers`, not your home directory.

Hard rails:

- **Nothing installed may be referenced by, bundled into, or loaded at runtime by `index.html`.** The library still comes only from `vendor/`; the offline contract applies to the artifact, not to your test harness.
- Never `npm install -g`, never install into your home directory, another project, or anywhere outside this folder. `.devtools/` is gitignored and must not appear in a folder or ZIP deliverable.
- If there is no network, or the install fights you, **stop**. Fall back to the headless-Chrome loop and record the missing checks as verification limits. Do not spend implementation budget on tooling; the scene is the product.
- Note in `IMPLEMENTATION.md` which browser tooling you had. §7 requires holding tool access constant between runs, and this is the one place where it can legitimately differ.

### Verification checklist

Record **pass / fail / not tested**, with evidence or a brief reason, for applicable checks. Fix failures rather than relabeling them as passes.

- **Cold offline launch:** open `index.html` with `file://` in a fresh browser context with networking blocked/offline. Verify a visible scene and working implemented controls. Inspect outgoing requests; zero external resource dependencies — including Three.js. HTTP localhost alone or a cache-backed load is insufficient.
- **Library provenance:** the deliverable contains the bundled Three.js source it actually runs, its licence text, and the exact revision stated in `IMPLEMENTATION.md`. No CDN/importmap/`npm`/`npx` step **for anything the artifact loads**, no remote `three/addons` load, and no hand-written WebGL scene substituting Three.js. (Dev-only test tooling under `.devtools/` per §6 is not part of the deliverable and does not count against this check.)
- **Visual review:** inspect the actual image at about 1440×900, then a narrow viewport such as 390×844. All five roofs and finial visible; readable tier spacing; deliberate palette; grounded objects; no clipping, flicker, empty scene, or control overlap. Take default, reverse-angle, and night views if supported. Prefer at least one render–inspect–refine cycle.
- **Real 3D:** orbit to the back and a different elevation. Perspective/occlusion must change correctly; the back is finished. If the camera bonus is absent, use a temporary development camera to inspect these angles.
- **Camera:** orbit, zoom to both limits, pan, release a drag outside the canvas, and reset. No stuck dragging, upside-down view, lost target, or slider/input conflict.
- **Day cycle:** test dawn, noon, dusk, midnight, and the 23:59→00:00 boundary. Lighting changes on the geometry; night remains readable. Paused animation still permits manual time changes.
- **Motion:** compare frames several seconds apart and while paused. Observe independent, plausible motion. Leave running for roughly a minute; no runaway particle/buffer counts or accumulating slowdowns. Check reduced-motion behavior.
- **Audio:** initial silence; enable by click; audible motif if listening is possible; volume and mute; repeated on/off; background and return. No stacking, clicks, clipping, or stuck playback. Audio-node state alone cannot verify musical quality.
- **Runtime:** inspect console errors, uncaught exceptions, and failed resource requests. Measure performance over multiple seconds after warm-up if reporting FPS; state browser, viewport, and environment. Check resize in both directions.
- **Shareability:** copy only the intended deliverable to a different local folder (with a space in its name), or extract the ZIP there; open it offline again. No absolute paths or dependency on project/prompt files.

Do not replace runtime checks with tests that merely look for words like “pagoda,” “wind,” or “offline” in the source. Do not claim tests you could not execute. Unavailable tooling is a verification limit, not permission to omit the working artifact.

## 7. Review rubric

This rubric guides honest human review; it is not a self-awarded certification. For comparisons between models, keep these instructions, supplied files, tool access, execution budget, browser/viewport, default camera, and time-of-day settings the same. Score the visible artifact and demonstrated interactions, not the model's self-report.

| Area | Points | What earns credit |
|---|---:|---|
| Pagoda architecture and voxel craft | 30 | Five readable tapering tiers, convincing eaves, coherent block scale, detailed structure and finial |
| Composition and visual atmosphere | 20 | Memorable first frame, intentional garden, material separation, depth and excellent lighting |
| Runtime and delivery | 20 | Correct Three.js 3D/depth, batched/instanced rendering, stable responsive resize, usable interface, genuinely portable offline artifact |
| Camera bonus | 8 | Reliable orbit, scroll zoom, pan, reset and input handling |
| Living-world bonus | 8 | Multiple convincing motion layers, bounded animation, pause/reduced-motion behavior |
| Time-of-day bonus | 7 | Smooth full-cycle control that changes real lighting and preserves night readability |
| Procedural music bonus | 7 | Original pleasant motif, user-gated synthesis, reliable volume/mute/lifecycle |
| **Total** | **100** | **Core 70 + bonuses 30** |

A blank page, non-3D substitute, CDN-loaded Three.js, a hand-written WebGL scene in place of Three.js, or a network/server-dependent deliverable does **not** meet the brief regardless of bonus points. Do not add meaningless geometry to inflate a count, invent performance figures, or sacrifice the hero scene to chase every bonus.

Final handoff: name the entry file and shareable files, list controls and bonuses actually implemented, summarize checks actually run, and disclose remaining defects or untested cases. Do not declare success solely because the code was written.

## 8. Research provenance — already distilled above; do not browse

These sources informed this prompt. They are not runtime dependencies or additional reading required of the implementation agent. All necessary requirements and recipes are in this document. Ratios, palette, musical suggestions, performance targets, and scoring are this benchmark's artistic/engineering choices, not historical facts or guarantees.

- [Artificial Analysis, public Pagoda Bench](https://artificialanalysis.ai/microevals/pagoda-bench-1788018029907): precedent for a procedural five-tier voxel garden with animation. Its prescribed CDN imports are **not offline**; its strict counts, version locks, model-specific directions, and hidden-test claims are deliberately not adopted.
- [OpenAI, Prompt engineering](https://developers.openai.com/api/docs/guides/prompt-engineering): clear roles, explicit constraints, structured sections, supplied context, and observable validation. Useful general guidance, not evidence that one wording is optimal for an unspecified local model.
- [Tōji, Five-Storied Pagoda](https://tojimap.jp/en/contents/content02/) and [Architecture of the Pagoda](https://tojimap.jp/en/contents/content02-2/): timber/tiled construction, stacked sections, central column, and ornamental finial. The brief is inspired by these architectural cues, not an exact replica.
- [MDN, JavaScript modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules): local-file module loading has CORS/security constraints; avoid runtime imports for this delivery contract.
- [MDN, WebGL best practices](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/WebGL_best_practices): batch draw calls, budget resources, and control drawing-buffer resolution — still applicable through Three.js batching, instancing, and pixel-ratio caps.
- [Three.js manual, Voxel geometry](https://threejs.org/manual/en/voxel-geometry.html): internal voxel faces waste geometry; generate visible surfaces. This applies directly to merged Three.js voxel batches. The URL is provenance only; the library here must come from local disk.
- Three.js package contents (`vendor/three.cjs` = `build/three.cjs` r180, `vendor/OrbitControls.js` = `examples/jsm/controls/OrbitControls.js`): the only library files supplied. Nothing else from the Three.js package is present or permitted — `BufferGeometryUtils` in particular is not here — and nothing may be fetched remotely.
- [MDN, Pointer capture](https://developer.mozilla.org/en-US/docs/Web/API/Element/setPointerCapture): preserve drag events when the pointer leaves the element.
- [MDN, Web Audio best practices](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API/Best_practices) and [sequencing audio](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API/Advanced_techniques): user-gesture audio activation, explicit sound controls, and scheduling ahead against the audio clock.
