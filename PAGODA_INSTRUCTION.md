# Stillwater Pagoda — Offline Voxel Diorama Benchmark (Three.js variant)

## 1. Your task

You are a creative graphics programmer and voxel environment artist. **Build a beautiful, genuinely three-dimensional Japanese-inspired five-story pagoda garden, rendered with Three.js, that opens offline from a double-clicked `index.html`.** Write the working artifact, not a proposal or a code block in chat.

Imagine a collectible miniature: an elegant pagoda above a pond, expressive stepped roofs, richly shaped trees, a small crossing, and lanterns. The first frame should make someone want to explore it. Give the scene a distinctive artistic identity and an interface worthy of it.

**Deliver the complete core scene and delivery requirements in §§2–3. Aim to implement all four bonuses in §5.** Prioritize a beautiful, unmistakable pagoda and reliable offline delivery; bonuses do not compensate for a missing or unfinished centerpiece.

This brief specifies the result, not the implementation. You choose how to construct, render, optimize, bundle, and animate it within the rules below. There are no secret APIs, voxel-count quotas, or prescribed algorithms. Visual quality and observable behavior matter more than claimed numbers.

## 2. Delivery contract

1. **Entry point: `index.html`.** Prefer a single self-contained file. If you choose that format, sharing that file alone must be sufficient to run the experience and include the required licence.
2. **A folder/ZIP is equally valid** if it contains every runtime dependency and its `index.html` opens directly after extraction. The recipient must not need a server, internet connection, installation, account, build command, or changed browser security settings. Ship only the intended deliverable, not development tooling or a dependency-installation directory.
3. **Offline means a fresh browser session without networking.** No network requests, remote services, or first-run downloads, including for Three.js, fonts, images, models, or audio. The artifact must not depend on a warm cache, absolute machine paths, or files left behind in the development project. Create the scene's visual content yourself; do not use downloaded or prebuilt art assets.
4. **Use the supplied Three.js.** `vendor/three.cjs` is the self-contained CommonJS build of **Three.js r180**. `vendor/OrbitControls.js` is the optional matching ES-module camera addon. `vendor/LICENSE` contains the Three.js MIT licence. These are the only permitted third-party runtime inputs; include the code you actually use and the licence in the deliverable. Integrating them for direct-file use is part of the task. Do not obtain another Three.js build or additional third-party runtime code or art assets from elsewhere. Record the exact Three.js revision used in `IMPLEMENTATION.md`. If the required core build or licence is missing, report the blocker; OrbitControls is optional.
5. **Render actual 3D through Three.js.** The scene must have real spatial depth, occlusion, materials, and lighting and remain convincing from different angles. A flat illustration, prerecorded scene, CSS construction, or 2D image presented as 3D does not qualify. Do not substitute a hand-written rendering engine for Three.js. Custom effects within the Three.js scene are welcome.
6. **Show the scene immediately.** No mandatory splash-screen interaction before viewing the garden. Sound alone requires opt-in. If graphics initialization fails, show a readable explanation instead of a blank page. The scene must remain usable if optional audio is unavailable.
7. **Deliver `IMPLEMENTATION.md` alongside the artifact.** Briefly state opening/sharing instructions, the files to share, controls, implemented bonuses, the exact Three.js revision, tested browser/environment, checks actually performed, and remaining defects or verification limits. Do not overwrite this repository's `README.md`. The runnable artifact must not depend on the notes or benchmark instruction files.

## 3. The core scene

### Hero architecture

Create a **Japanese-inspired five-story pagoda**, interpreted artistically rather than claimed as an exact historical reconstruction:

- Five distinct stacked stories and roof tiers, each roof narrower than the one below. The silhouette must be unmistakable at thumbnail size.
- Elegant proportions with visible structural space between roofs: neither a squat stack of plates nor a skyscraper with tiny ledges.
- Deep overhanging eaves, stepped sloping roofs, and an expressive curved outline with gently lifted corners. Five flat plates or five plain pyramids are not sufficient.
- Readable lacquered posts, timber beams, contrasting wall panels, recessed doors/windows, and bracket-like supports beneath the eaves. Include a legible entrance, stairs, and a stone plinth.
- A slender ornamental **sōrin finial** crowning the top roof, with a recognizable stacked-ring character.
- Finished sides and back, convincing structural connections, and no floating roofs, detached pillars, flickering surfaces, or foliage concealing missing architecture.

The pagoda and garden must visibly belong to a coherent **voxel/block-built world**. Architectural detail, terrain steps, and vegetation should have deliberate block-scale craftsmanship. A smooth building with a pixelation filter does not qualify. Water, sky, lighting, and atmospheric effects need not be made of literal cubes; they should complement the scene rather than erase its voxel identity.

### Garden and composition

- Create a bounded garden/island diorama with an intentional outline and visible soil/stone depth, not an endless empty plane.
- Lead the eye toward the entrance with a path.
- Include a pond with a shaped shoreline and a small bridge or stepping-stone crossing.
- Frame the pagoda with thoughtfully composed trees, including blossom trees and contrasting foliage. Give them varied silhouettes, branching character, and convincing canopies rather than identical decorative balls. Choose the arrangement, density, season, and colors yourself.
- Include convincing garden details such as stone lanterns, rocks, moss, bamboo, or reeds. Make the environment feel inhabited and intentional, not randomly filled.
- Start with an elevated three-quarter view that shows two pagoda faces, the pond, all five roof tiers, and the full finial. The pagoda should be the focal point without clipping or being hidden by scenery or controls.
- Compose for both a desktop viewport and a narrow portrait viewport. Preserve useful framing and a readable interface after resizing.
- The garden must remain convincing from the opposite side and a different elevation, not just from the opening camera angle.

### Color, light, and atmosphere

Choose a coherent, expressive art direction. Vermilion timber, jade roofs, warm ivory walls, and pink blossoms are one possibility, **not a required palette**. Seasonal colors, richly varied trees, stylized skies, and other thoughtful interpretations are welcome.

Give materials distinct identities and use light, shade, and contact with the ground to make the miniature feel dimensional. The default should be an attractive golden-hour scene. Roof profiles, timber, and voxel faces must remain readable, including in shaded areas. Repeated launches should reproduce the same garden composition and material color choices.

**There is no preference for simple effects over sophisticated ones.** Beautiful cast shadows, reflections, moving water, visible sun or moon, clouds, mist, particles, and richer vegetation are welcome when they strengthen the image and run reliably. Choose their implementation and complexity yourself. Judge them by their visual contribution: avoid accidental flicker, distracting clutter, lost silhouettes, or effects that hide the craftsmanship. Extra effects are not separate requirements or substitutes for the core scene.

### Interface and usability

Design a polished interface that belongs to the artwork. Typography, layout, color, transitions, and control styling are part of the experience; they do not need to follow a prescribed template.

Keep the garden as the primary, full-viewport experience. Include a title and discoverable control guidance. Controls may be compact, grouped, or thoughtfully collapsible, but must be readable and usable without covering the centerpiece. Do not turn the entry view into an unrelated marketing page or settings dashboard.

Use clearly labeled, keyboard-operable controls, visible focus states, and adequate contrast. Avoid overlap or inaccessible controls at narrow widths. Interacting with the interface must not accidentally manipulate the scene, and decorative overlays must not block intended scene input. Only expose controls that actually work. Use fonts available offline.

## 4. Implementation freedom and working scope

The required outcomes, Three.js dependency, and offline delivery contract are fixed. **The technical approach is yours.** You may write your own camera controls, geometry generators, shaders, lighting or water effects, procedural textures, and supporting code. No particular camera projection, geometry organization, material model, shadow technique, file-bundling method, or rendering optimization is prescribed.

Make the experience responsive and stable on a normal modern laptop. A desktop viewport around 1440×900 and a narrow viewport around 390×844 are the review targets. Interaction should feel smooth; prolonged use, animation, resizing, and repeated control use must not cause accumulating slowdowns or resource growth. If you report performance figures, measure them and identify the environment.

Work within this repository. Do not read other benchmark variants or solutions, search other projects for dependencies, or use online research. Everything needed for the artifact is supplied here or must be authored by you. Local scripts and development tools may be used to produce it, but do not install or download artifact dependencies or build tools. The only permitted installation is optional dev-only browser testing tooling under §6.

During an implementation run, preserve `AGENTS.md`, `README.md`, and this brief. Put your implementation notes in `IMPLEMENTATION.md`. Do not delegate implementation to sub-agents. Make reasonable artistic and engineering decisions without asking the owner to design the submission for you.

## 5. Interactive bonuses

Aim to deliver all four. They are scored separately from the 70-point core; a bonus is earned by working behavior, not the presence of a control or a claim in the notes.

### A. Camera: orbit, zoom, pan, reset

- Left drag orbits around the scene. Wheel/trackpad scroll zooms in and out.
- Shift+left drag pans in camera-relative screen directions; right-drag panning is also welcome.
- A visible **Reset view** control restores the composed default.
- Keep movement within useful limits: no upside-down view, ground-crossing camera, unusable zoom, or irretrievably lost subject.
- Drags must end reliably, including when released outside the scene. Controls must not interfere with sliders, buttons, or unrelated page input.
- Any automatic camera motion must be disableable and stop when the user takes control. Manual interaction must never fight the camera.
- Touch gestures and keyboard camera navigation are welcome additions; the interface itself must remain keyboard-operable whether or not camera shortcuts are provided.

### B. A living garden

Include at least two complementary layers of visible environmental motion, such as swaying foliage and drifting petals, or pond ripples and swimming koi. Other coherent combinations are welcome.

Motion should feel varied, gentle, and connected to the environment. Trees remain rooted; foliage and petals move naturally rather than vibrating; water does not move as a rigid slab; fish stay within the pond. Keep the pagoda and terrain rigid.

Provide an **Animate/Pause** control that freezes environmental motion. Respect the user's reduced-motion preference by starting environmental and automatic camera motion paused or substantially reduced. Manual camera and time controls must remain usable. Motion must remain stable over extended use.

### C. Time of day

Provide a clearly labeled **Time of day** slider covering the full 24-hour cycle, a readable `HH:MM` value, and useful dawn/noon/dusk/night markers. Start at an attractive golden hour, approximately **17:30**. Scrubbing must update the scene immediately.

Time changes must affect the actual scene: the direction, color, and strength of illumination; sky or atmospheric color; and warm lantern/window light. Shadows and any visible sun, moon, clouds, or reflections must remain coherent with the chosen time and artistic lighting scheme. A background-only color change does not qualify.

Make transitions smooth, including across midnight. Night must remain legible with cool illumination and warm accents; do not light the underside of the world with a below-horizon sun.

Automatic progression is optional. If present, give it a separate toggle and an unhurried multi-minute cycle. Manual scrubbing must take precedence. Pausing the garden must pause automatic day progression without disabling the slider.

### D. Original generated ambient music

Compose a quiet, pleasant, recognizable musical motif using **Web Audio synthesis only**. The composition and generated sound must live in the artifact. No recordings, downloaded music, or existing audio assets, even if embedded.

Choose the instrumentation, pitch language, tempo, and arrangement yourself. Aim for an intentional, listenable miniature soundtrack with phrasing, space, and a returning motif—not endless random beeps. It may evoke the garden without claiming historical musical authenticity.

- Sound starts **off**. Provide an explicit **Enable sound / Mute** control and a volume slider.
- Sound must begin only after user opt-in, and the UI must reflect whether it actually started. Audio failure must not break the garden.
- Keep playback comfortable and clean: no clicks, clipping, unintended bursts, or accumulating layers.
- Mute must silence everything, including lingering effects. Repeated enable/mute cycles must not duplicate the music.
- Handle leaving the tab and returning without a burst of missed notes or unexpected loud playback.
- Keep sound independent from the garden's animation toggle and document its pause/background behavior.

Functional audio checks cannot establish musical quality. If you cannot listen, disclose that separately.

## 6. Inspection and verification

Inspect the artifact during development and after the final changes. When browser tooling is available, **look at the rendered images**, evaluate the most visible weaknesses, refine the result, and inspect again. A screenshot filename, DOM snapshot, canvas element, or syntax check is not visual evidence.

### Testing tools and boundaries

Use browser tooling exposed by the harness or a runner-provided browser executable. Ordinary command-availability checks are allowed; do not scan the filesystem, inspect other projects, or create new containers/services to obtain tooling. Test only your own artifact or its local development URL. A local server is allowed for development, but the final delivery check must use a real direct-file (`file://`) load with normal browser security settings.

For a standalone run, if browser testing would otherwise be unavailable or insufficient, you may install a browser automation package and, if necessary, its browser under **`.devtools/` in this repository**. For local tooling you set up, keep its files, download caches, browser profiles, and test outputs scoped to the repository. Do not install globally or into another project. None of this tooling may become an artifact dependency or be included in the deliverable. If setup is unavailable or fails, stop tooling work and disclose the missing checks rather than abandoning the artifact.

For controlled comparisons, the runner must fix permitted tool access and browser/tool versions before the runs; an optional installation is not permission to give one submission a different testing environment. Record the tooling actually used in `IMPLEMENTATION.md`.

### Review checklist

Record **pass / fail / not tested** with evidence or a brief reason. Fix observed failures where possible; do not relabel them as passes. Apply bonus checks to features actually implemented and identify omitted bonuses separately.

- **Cold offline launch:** open the intended deliverable through `file://` in a fresh browser context with networking blocked/offline. Confirm a visible scene and usable implemented controls. Check for external resource dependencies, including Three.js. A localhost-only test or cache-backed launch is insufficient.
- **Dependency and licence compliance:** confirm that the deliverable runs the supplied Three.js, carries its MIT licence, states the exact revision, and does not depend on other runtime libraries, development tooling, remote resources, or project instruction files.
- **Visual quality:** inspect the default view at about 1440×900 and 390×844. Check all five roofs and the finial, readable tier spacing, finished structure, coherent materials, convincing garden composition, and usable UI. Look for clipping, flicker, hidden geometry, and control overlap. Inspect a reverse view and, when implemented, a night view.
- **Real 3D:** inspect the back and a different elevation. Spatial relationships and occlusion must behave correctly, and those views must be finished. This requirement applies even without a user-facing camera bonus.
- **Camera:** exercise orbit, both zoom limits, pan, release outside the scene, reset, and interaction with UI controls. Confirm no stuck drag, lost subject, or input conflicts.
- **Day cycle:** inspect dawn, noon, dusk, midnight, and the midnight boundary. Confirm meaningful changes to scene lighting, coherent effects, and readable night views. Manual time changes must work while animation is paused.
- **Motion:** observe different motion layers, pause/resume, and reduced-motion behavior. Leave the scene running for roughly a minute and check that behavior and responsiveness remain stable.
- **Audio:** check initial silence, user-enabled playback, volume, full mute, repeated toggles, and leaving/returning to the tab. Listen to the motif if possible; distinguish audible quality from functional checks.
- **Runtime:** check errors, failed resource requests, resizing in both directions, and responsiveness after warm-up and repeated interaction. State the browser, viewport, and environment for any measurements.
- **Shareability:** copy only the intended deliverable into a new test folder inside this repository, with a space in its name, or extract the ZIP there. Open that copy offline. Confirm that it does not rely on files outside the shareable artifact.

Do not substitute source-text checks for behavior or invent results. If image viewing, direct-file testing, network inspection, or listening is unavailable, state the specific limitation. Missing tooling does not remove the implementation requirements, and an untested feature is not automatically a working feature.

## 7. Review rubric

This is a human-review rubric, not a self-awarded certification. Score the visible artifact and demonstrated behavior, not the model's self-report. Sophisticated effects and interfaces earn credit through the quality they contribute, not their complexity or quantity.

For model comparisons, keep the brief revision, supplied files, tool access, execution budget, browser/environment, viewport sizes, and review procedure fixed. Review each submission's authored default composition and the same kinds of additional views and time-of-day states; do not impose identical camera coordinates on differently scaled scenes. Judge unverified behavior through reviewer testing, not assumption.

| Area | Points | What earns credit |
|---|---:|---|
| Pagoda architecture and voxel craft | 30 | Five readable tapering tiers, expressive eaves, coherent block scale, finished structure and finial |
| Composition and visual atmosphere | 20 | Memorable first frame, beautiful garden, distinctive art direction, material separation, depth and excellent lighting |
| Runtime and delivery | 20 | Genuine Three.js 3D, smooth and stable operation, responsive framing, polished usable interface, portable offline artifact |
| Camera bonus | 8 | Reliable orbit, scroll zoom, pan, reset, useful limits and input behavior |
| Living-world bonus | 8 | Multiple convincing motion layers, stable animation, pause and reduced-motion behavior |
| Time-of-day bonus | 7 | Smooth full-cycle control, meaningful lighting changes, coherent effects and readable night |
| Procedural music bonus | 7 | Original pleasant motif, user-gated synthesis, reliable volume/mute and playback behavior |
| **Total** | **100** | **Core 70 + bonuses 30** |

Report delivery-contract compliance separately from the score. A blank page, non-3D substitute, replacement rendering engine, missing required Three.js/licence, or network/server-dependent artifact is **not a valid submission**, regardless of bonus points. Diagnostic feedback may still be given, but invalid submissions must not be ranked as successful ones. Visual weaknesses and incomplete bonuses should be reflected honestly in their respective scoring areas.

Final handoff: name the entry file and shareable files, list controls and bonuses actually implemented, summarize checks actually run, and disclose remaining defects or untested cases. Writing the code alone is not evidence that the result works.

## 8. Provenance

This is a custom benchmark inspired by the public [Pagoda Bench](https://artificialanalysis.ai/microevals/pagoda-bench-1788018029907) and Japanese pagoda architecture, including [Tōji's five-storied pagoda](https://tojimap.jp/en/contents/content02/). It does not reproduce another benchmark's hidden tests or claim historical precision.

These links are attribution, not required reading or permission to browse during a run. This document contains the complete task. The supplied Three.js r180 files and MIT licence are the only third-party runtime inputs; all artistic and engineering decisions beyond the stated requirements are yours.
