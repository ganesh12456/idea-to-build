# Three.js game: depth example

Use this as a compact illustration of engineering depth, not a claim of completed implementation or fixed defaults. A full output also includes the eight-category PRD and traceability required by the document contract.

## Input and state of knowledge

Confirmed: game featuring Hanuman reaching Seetha Matha in Lanka, fighting, fire sequence and escape; Three.js requested. Proposed assumptions: single-player desktop browser prototype, stylized non-graphic action, keyboard/mouse, one compact level. Open: target devices, artistic/source interpretation, assets and rights, language, scope, budget/currency and deadline. No implementation exists in this example.

## Provisional eight-category coverage

| Category | Project-specific proposal |
|---|---|
| Business | One complete playable story experience; proposed success is a new player finishing it without developer assistance. Audience and release purpose unresolved. |
| Functional | Enter Lanka, reach peaceful meeting encounter, activate scripted fire sequence, escape; checkpoints, retry and completion. |
| AI | N/A for generative AI; guards use ordinary patrol/chase/attack states. |
| Data | Versioned local checkpoint/settings save; no account or cloud database for proposed prototype. |
| Frontend | Three.js world/camera, controls, objective/health HUD, pause, subtitles and loading/failure states. |
| Backend | N/A initially; static asset hosting. Cloud saves or trusted scores would change this decision. |
| Nonfunctional | Propose a reference-device frame target after device selection; bound particles, test collisions and dispose resources on scene changes. |
| Delivery | Greybox movement prototype first, then complete story slice, then licensed art/audio and release checks; budget unresolved. |

## Architecture and core principles

Option A, recommended for this scope: TypeScript browser application with Three.js, DOM-based menus/HUD, a game-state controller, asset loader and local persistence. Option B: same stack with server API, accounts and database for cross-device saves. B adds identity, data/security and operating work; choose it only if cross-device progress is a confirmed need.

Flow: input -> player controller -> simulation/collisions -> scene state -> renderer/HUD; checkpoint events -> validated save adapter. Rendering is not the source of truth for mission completion. An explicit mission state prevents skipping the meeting by entering an escape trigger early. Movement uses elapsed time, with an agreed strategy for large frame gaps and collision stability. A paused state stops simulation while menus remain usable. Scene teardown releases listeners, models, textures and effects it owns.

Proposed folders: src/game/ for state and lifecycle; src/player/ for controller/input; src/world/ for level/collisions; src/enemies/ for guard states; src/ui/ for HUD/menus; src/effects/ for bounded fire effects; src/storage/ for versioned saves; public/assets/ for optimized models/audio with a rights inventory. Keep the first greybox small before adopting a physics or animation dependency.

## Storage design and setup

No PostgreSQL is proposed for this prototype. Browser-local storage persists only on that browser/device and may be unavailable or erased. It is not suitable for trusted leaderboards.

Illustrative save record, not executed:

```json
{"schemaVersion":1,"checkpoint":"ashoka-vatika-entry","settings":{"music":0.5,"subtitles":true}}
```

Checkpoint is an allowlisted identifier, not arbitrary coordinates or executable content. On load, validate record version, checkpoint and setting ranges. Missing/corrupt/unsupported saves offer a safe new game and an understandable message; storage failure must not prevent playing. Store no personal details. Persist at milestone checkpoints; do not write every animation frame. Define reset confirmation and future version migration before changing the format.

Setup sequence: confirm browser/device baseline; verify supported runtime/build-tool versions in official docs; initialize a TypeScript client and lock dependencies; create renderer/camera/input loop; load a placeholder level with an asset-error fallback; add state/collision/controller; connect checkpoint save/load; add DOM HUD; run a production build and host under the intended path. Each step needs an observable smoke result. Exact commands and versions require current verification. No database credentials or API secrets are required for the proposed static prototype.

## First implementation slice

Proposed prompt:

“Build only a greybox Three.js/TypeScript prototype of the entry-to-checkpoint journey. Add a controllable placeholder character, third-person camera, floor/wall collision, pause/restart and one checkpoint trigger. Separate simulation, rendering, input and mission state. Use placeholder geometry and label it; no final character art, combat, fire, external services or paid assets. Validate movement at different frame rates, wall blocking, pause/resume and checkpoint retry; report checks actually performed and known gaps. Stop and explain if the camera/collision approach requires a major dependency or a scope change.”

Beginner review: walk and jump across the area, attempt to pass through a wall, pause mid-movement, restart, reach the checkpoint and retry. Success means the controller remains responsive, walls block movement, pause freezes gameplay and retry returns to the checkpoint. These are proposed checks, not passed tests.

Later slices: meeting and mission transitions; one guard/combat loop; bounded fire and escape; persistence/failure recovery; asset/art/audio pass and device profiling. Test story order, camera obstruction, health/retry, corrupt saves, missing assets and scene transitions. Confirm respectful narrative interpretation, asset licenses, performance baseline and scope before release. Prototype completion does not imply production readiness.
