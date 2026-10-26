# Project Requirements Document contract

Start with project name, version/date, draft/approved status, purpose, context sources, and a concise ledger of Confirmed / Recommendation / Assumption / Open question. Assign owners or mark owner unassigned. Do not label a draft approved without evidence.

## Eight requirement categories (required order)

1. **Business**: problem, users/stakeholders, business outcome and measurable success metrics with baseline/source and target window, scope/non-goals, budget constraints and value tradeoffs.
2. **Functional**: main and exception user journeys; user stories; behavior, permissions and recovery; MoSCoW backlog; MVP boundary and exclusions.
3. **AI**: applicability; task, autonomy and human oversight; grounding/input/output; model/vendor restrictions; hallucination/prompt-injection/data-leakage risks; evaluation dataset/provenance/splits, metrics and release thresholds; fallback, monitoring, latency and per-task/monthly spend. Use N/A with reason for non-AI projects.
4. **Data**: sources, rights/access, entities/relationships, volume/quality, classification, lineage, residency, retention/deletion, migrations and backup/restore needs.
5. **Frontend**: roles/screens, journey states (empty/loading/error/success), accessibility, responsive behavior, interaction and session expectations.
6. **Backend**: API boundaries/contracts, authentication/authorization, validation, workflows/jobs, integrations, idempotency/retries, failures and observability.
7. **Nonfunctional**: measurable performance/load, reliability/recovery, security/privacy threat model and controls, accessibility, maintainability and operating constraints. Tie targets to workloads and test methods.
8. **Delivery**: team/owners, milestones/dependencies, environments, budget and cost model, operational ownership, rollout/rollback and decision gates.

Use requirement records with: ID | requirement | evidence state/source | MoSCoW | acceptance criterion | owner. Criteria should specify preconditions/action/observable result, quantitative target where meaningful, and verification method. Unknown numerical targets stay proposed or unresolved. Avoid vague criteria such as “secure” or “fast.”

## Supporting plans (after the eight categories)

- **Architecture options**: compare at least two plausible approaches when a real tradeoff exists; components/data flow, complexity, security boundary, scalability, cost drivers, fit and recommendation conditions. If only one is viable, explain why. Do not pretend competing stacks are viable when the user mandates a stack.
- **Implementation phases**: dependencies, deliverables, entry/exit gates, owners and estimate ranges with assumptions; deliver a thin end-to-end slice early. Separate discovery/prototype from production readiness.
- **Risks and decisions**: risk, likelihood/impact, mitigation, owner, trigger; decision, options, consequence and deadline. Include budget overrun and external-access risks.
- **Testing/deployment checklist**: unit/component, integration/API, end-to-end journeys, authorization/tenant isolation, privacy/security, load/recovery, accessibility, AI evaluation if applicable; staging, configuration/secrets, migrations/backups, monitoring, budget alerts, rollout, rollback and support. Mark every item planned, verified with evidence, or N/A.
- **Traceability matrix**: requirement ID -> goal -> journey/story -> component -> phase -> test/acceptance evidence -> status. Cover all in-scope IDs; explicitly list deferred items. A planned test is not evidence of a pass.
- **Definition of done**: acceptance evidence for Must requirements, resolved critical assumptions, security/privacy review, AI gates if applicable, budget verification, operational readiness and stakeholder acceptance. Distinguish completion of the PRD from completion of the product.

## Required depth for a full planning package

The eight categories describe requirements; they do not replace the engineering blueprint. After them include the following substantive sections, using engineering-blueprint.md and coding-agent-handoff.md:

1. Project-specific core engineering principles with examples.
2. Architecture decision comparison, recommendation, component responsibilities, data flow and trust/state ownership.
3. Frontend screen/scene states and module/folder design.
4. Backend/API contracts or reason for N/A and future trigger.
5. Storage/database choice, schema/record model, integrity/validation, migrations or save versioning, and recovery.
6. Ordered environment/database/setup plan with expected checks and unverified-command labels.
7. Phased build backlog with a concrete first coding-agent prompt and beginner review instructions.
8. Testing/deployment and operations checklist, risks/decisions, traceability and definition of done.

The first discovery response must still give a provisional eight-category coverage map and a recommended system shape before the small question batch. A full package is not mandatory for every introductory turn, but cannot be withheld when the user requests one. Use N/A with reasons rather than adding artificial infrastructure.
