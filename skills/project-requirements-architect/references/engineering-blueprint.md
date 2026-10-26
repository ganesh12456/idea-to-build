# Engineering blueprint

Use this reference for the full plan. Translate every section into the actual project; do not output an unfilled checklist. Label proposed specifics and unresolved decisions.

## 1. Architecture decision record

Describe the primary journey as a data/control flow. Identify client, server, storage, external systems and background work only where needed. Include a small diagram when helpful. Mark trust boundaries, source of truth, ownership and failure paths.

Compare a simple baseline with a meaningful alternative using complexity, cost drivers, latency, security, offline support and operational burden. Explain the choice and when to revisit. Respect mandated technologies. Specify why authentication, APIs, queues, caching, real-time sync or object storage are needed or N/A. Avoid microservices by default without an isolation or scale requirement.

## 2. Project-specific engineering principles

Select principles that change implementation decisions, with a concrete example for each. Consider separation of domain rules from UI, explicit state transitions, one owner for mutable state, validation at boundaries, safe retries/idempotency, least privilege, dependency restraint, recoverable failures and measurable performance budgets.

For games: frame-rate-independent movement, pause/scene lifecycle, deterministic transition rules, separation of simulation/render/input, collision ownership, asset disposal and bounded effects. For ledgers: immutable transaction history or explicit reversals, money representation, transactional writes and derived balances. For AI: evidence provenance, prompt/data separation, permission limits and evaluation before release. Do not present every principle as mandatory for every project.

## 3. Frontend and interaction blueprint

Provide screens/scenes, navigation or state-machine transitions, happy/error/empty/loading/offline states, input methods, accessibility and responsive expectations. Explain where local state lives and how it synchronizes. Propose a compact folder/module structure with responsibilities, not empty scaffolding.

For Three.js: rendering/camera, simulation/update loop, input, character controller, world/collisions, game state, UI overlay, assets/audio, effects and persistence. Identify integration boundaries and a playable vertical slice. Native browser APIs versus additional libraries is a decision, not an automatic dependency list.

## 4. Backend and integration contracts

If needed, list important endpoints or commands with method/name, input/output shape, authorization, validation, error codes and retry behavior. Define background job lifecycle and integration failure handling. Explain session/token ownership and secret locations. If no backend is needed, say why and what feature would introduce one. Browser clients cannot securely hold provider secrets or serve as trusted authorities for competitive scores.

## 5. Data and database design

First decide whether persistence is needed and whether browser storage, files, a relational database or another store fits. Explain what data must survive restart, synchronize across devices, remain private, or be authoritative. Avoid a hosted database for a static single-player prototype unless its requirements justify one.

When a database applies, include:

- Entity/relationship model with concrete key fields, primary/foreign keys, cardinality and ownership/tenant boundaries.
- Required/nullable/default values, uniqueness and integrity constraints; representation of money, timestamps and deletion states as relevant.
- Query/access patterns and justified indexes, transaction/concurrency rules and data growth assumptions.
- Migration ordering and tool choice, synthetic seed data, rollback/forward-repair approach, retention/deletion and backup/restore verification.
- Access permissions, connection pooling if needed, server-only connection secrets, environment isolation and residency/open approvals.
- A minimal proposed schema or illustrative DDL when useful; label it unexecuted. Never give destructive migration instructions as routine setup.

For browser storage, provide a versioned record example, validation/default behavior for missing or corrupt saves, compatibility/migration policy, reset/export handling and limitations such as device-local persistence and possible storage loss. Distinguish preferences from trusted game/business records.

## 6. Reproducible setup plan

Provide ordered steps, each with purpose, inputs, expected observable result and failure check:

1. Runtime/tooling versions and package-manager lockfile policy.
2. Project initialization and module/folder layout.
3. Configuration contract: variable names, purpose, required/optional, public versus secret, development/staging/production separation. Use placeholders only; never real credentials.
4. Local dependencies or managed resources, only if justified. Database creation, restricted role, migrations, seed and connectivity check when applicable.
5. Run/build entrypoints and smoke checks; verify exact commands from current official sources or mark them proposed/unverified.
6. CI checks, preview/staging, deployment settings, migrations if applicable, logs/alerts, rollback and restore.

Differentiate writing a setup plan from actually provisioning resources. When tooling/network is unavailable, provide a decision/setup sequence without fabricating executed commands.

## 7. Quality and operations

Tie performance targets to workload/device. Define failure behavior, telemetry with redaction, security checks, functional verification, accessibility checks, load/frame profiling, dependency/license review and support ownership. Give rollback triggers and a recovery procedure. Track service and asset costs separately where applicable. All proposed targets require confirmation or measurement.
