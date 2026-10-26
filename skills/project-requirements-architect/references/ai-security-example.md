# Example usage

“Use $project-requirements-architect for an AI Security Incident Investigator using FastAPI, React and PostgreSQL. Help analysts investigate uploaded logs and draft evidence-backed reports. Start with the important missing questions.”

Example first response: “I have the purpose and stack. Who will use the first release, and which investigation outcome matters most? Which log sources and sensitive-data restrictions apply? What are the delivery deadline and build/operating budget, including currency?”

If answered, ask only remaining consequential questions. If asked to draft now, show assumptions as below.

# Example output — abbreviated but complete PRD

Version 0.1; draft. This is a proposed design. No application, integration, security control, deployment or evaluation has been implemented or verified by this example.

Confirmed from the example request: investigation assistant; FastAPI/React/PostgreSQL; uploaded logs; evidence-backed draft reports.

Recommendations: analyst review before report finalization; read-only investigation; modular monolith initially. Assumptions A1–A3: one internal security team, synthetic JSON logs for the prototype, and a pilot workload of 10 concurrent analysts. Owners unassigned. Open decisions: supported log schemas, identity provider, external model permission, residency/retention policy, deadline, team capacity, currency and build/monthly spending caps. These block production commitment, not this draft.

## 1. Business

BUS-01 [Recommendation; Must]: reduce analyst triage effort. Proposed success target: median time to an approved draft report at least 25% below a manual baseline on 20 matched synthetic cases during the pilot. Baseline and target need stakeholder confirmation; no measurement exists.

Budget: unknown. Estimate build cost as approved hours × local rate; recurring cost as hosting + database/storage/backups + model calls × average input/output usage and provider rates + support. Verify current quotes after workload and residency decisions. Do not call this plan affordable yet.

## 2. Functional

Journey J1: analyst signs in → creates case → uploads logs → reviews ingestion errors → requests analysis → inspects cited evidence → edits/approves draft → exports report. J2: unauthorized case access is denied; invalid upload can be corrected; AI failure leaves evidence available for manual investigation.

Story S1: As an analyst, I want evidence-linked findings so I can verify each conclusion. S2: As an analyst, I want failures explained without losing my case so I can continue manually.

FUN-01 [Recommendation; Must]: create case, upload validated logs, review findings and export approved report. Acceptance: a synthetic case completes J1; malformed logs produce actionable errors without creating partial findings; an unapproved draft cannot be exported as approved. Test T1: end-to-end workflow.

MVP: single-team case workflow, one agreed JSON schema, evidence citations, manual review/export. Should: saved filters. Could: timeline visualization. Won't this release: live SIEM ingestion, automated containment, multi-tenant SaaS, guaranteed incident detection. Deferred backlog D1–D3, not implementation commitments.

## 3. AI

AI-01 [Recommendation; Must]: generate hypotheses and summaries grounded in uploaded evidence; no containment actions. Each factual finding links to an immutable event ID. Missing evidence produces an explicit uncertainty statement; analyst approval is required.

Proposed gate T2: a security reviewer labels 50 synthetic/de-identified cases, freezes a 20-case holdout, and checks factual findings for at least 95% citation support and at most 5% unsupported factual claims; report denominators and per-case failures. Require all 10 designated insufficient-evidence cases to abstain and all 10 prompt-injection cases to avoid external action or disclosure. Small samples limit confidence; expand before wider rollout. Evaluate prompt/model versions separately; never train/tune on holdout cases. These are targets, not results.

Model/vendor decision remains open pending data-processing approval. Log text is untrusted data. Keep tool permissions read-only and exclude secrets from prompts. On timeout or cap exhaustion, show a retry/manual-review state without inventing findings. Proposed p95 analysis latency ≤30 seconds at the pilot workload; per-case and monthly caps unresolved and must be set before a paid pilot.

## 4. Data

DAT-01 [Recommendation; Must]: store cases, normalized events, event provenance/hash, findings with evidence IDs, report versions and audit entries in PostgreSQL. Proposed entities: Case 1:N Event; Case 1:N Finding; Finding N:M Event; Case 1:N ReportVersion.

Acceptance T3: every citation resolves to its original imported event; duplicate import retries do not duplicate events. Confirm access rights and classification before importing real logs. Proposed deletion behavior: configured retention removes case content and derived summaries; backup expiry and legal-hold exceptions require policy approval. Do not promise immediate backup erasure. Synthetic data only until those decisions are resolved.

## 5. Frontend

FE-01 [Recommendation; Must]: React case list, upload status, findings/evidence view and review/export screen support loading, empty, error and success states. Acceptance T4: J1 is keyboard-operable, errors are announced to assistive technology, and findings/citations remain distinguishable without color. Target WCAG 2.2 AA, subject to a scoped audit; no conformance claimed.

## 6. Backend

BE-01 [Recommendation; Must]: FastAPI exposes case/upload/analysis/report endpoints; server-side authorization scopes every request to permitted cases. Use idempotency keys for uploads and analysis requests, bounded retries and structured error responses. Acceptance T5: an unauthorized user cannot read or modify any case resource; replaying a successful upload key returns the same import; provider failure records a failed job with no fabricated findings. Identity provider remains undecided.

## 7. Nonfunctional

NFR-01 [Recommendation; Must]: protect incident data through scoped access, encrypted transport/storage, secret management, redacted telemetry and an audit trail. Acceptance T6: negative authorization tests cover every resource endpoint; secret-canary fixtures do not appear in logs; staging verifies configured transport/storage protections. A threat review covers malicious uploads, prompt injection, unauthorized access and report leakage.

NFR-02 [Assumption A3-derived recommendation; Must]: at 10 concurrent pilot users, ordinary case reads meet p95 ≤500 ms excluding uploads/AI. Proposed recovery targets: RPO ≤24 hours, RTO ≤4 hours. T7: agreed load test and timed restore exercise with recorded results. Targets await stakeholder confirmation.

## 8. Delivery

DEL-01 [Recommendation; Must]: stage with synthetic data before a limited production pilot. Acceptance T8: named owner demonstrates rollback, restore, alert routing and enforced spend limits; security/data approvals and Must acceptance evidence are recorded. No release date or budget commitment until team capacity and caps are confirmed.

## Architecture options

Option A, recommended for the assumed pilot: React → FastAPI modular monolith → PostgreSQL, with a bounded worker process and provider adapter. Lower operational complexity; job retry/durability and resource contention need explicit design. PostgreSQL job records provide persistent status; their implementation is still planned.

Option B: same confirmed stack plus dedicated queue/worker service. Better isolation for large imports and long analyses; adds deployment, queue security, monitoring and recurring costs. Choose B if measured backlog or isolation needs exceed A's limits. Neither option authorizes external model processing; that remains a gate.

## Phases

P0: resolve data/model permissions, owners, caps and schema; baseline study. Exit: agreed constraints.
P1: thin J1 slice with synthetic data and a stubbed analysis response; stub is visibly labeled. Exit: T1/T3/T5 smoke evidence.
P2: approved provider integration, grounding/review and failure recovery. Exit: T2/T4/T6 evidence.
P3: load/restore tests and limited pilot. Exit: T7/T8 and business pilot plan.

Sequence is proposed; duration and cost ranges cannot be responsibly committed without team capacity and vendor choices. Estimate each phase after P0 and retain contingency for access and data-quality delays.

## Risks and dependencies

High impact: sensitive logs sent to an unapproved provider → block real-data AI until approval; owner unassigned. Medium/high: misleading findings → citations, holdout evaluation and analyst review. Medium/high: budget overrun → per-job limits, concurrency caps and monthly cutoff before paid use. Medium: missing log access/schema → synthetic fixtures and schema agreement in P0. Identity access and operational ownership are production dependencies. Risk likelihoods are preliminary.

## Testing/deployment checklist

All planned, none passed: unit parser/validation tests; API/database integration and idempotency; J1/J2 end-to-end; authorization and malicious-upload tests; privacy/retention review; AI holdout/adversarial evaluation; keyboard/accessibility audit; load and restore exercises. Before deployment: approved secrets/configuration, staging migrations and backup, redacted monitoring, cost cutoff, named support contact, limited rollout and rehearsed rollback. Live SIEM integration tests: N/A for this MVP.

## Requirements traceability

All rows proposed, verification pending. BUS-01 is the common business goal.

| ID | Goal / journey or story | Component | Phase | Verification |
|---|---|---|---|---|
| BUS-01 | Faster triage / J1 | Pilot measurement | P0/P3 | Matched baseline study |
| FUN-01 | BUS-01 / J1,J2,S2 | Full workflow | P1 | T1 |
| AI-01 | BUS-01 / S1,J2 | Analysis adapter/review | P2 | T2 |
| DAT-01 | BUS-01 / S1 | PostgreSQL/import | P1 | T3 |
| FE-01 | BUS-01 / J1,S2 | React | P2 | T4 |
| BE-01 | BUS-01 / J1,J2 | FastAPI/auth/jobs | P1 | T5 |
| NFR-01 | BUS-01 / J2 | Access/storage/telemetry | P2 | T6 |
| NFR-02 | BUS-01 / J1,J2 | API/operations | P3 | T7 |
| DEL-01 | BUS-01 / J1 pilot | Deployment/operations | P3 | T8 |

Deferred: D1 saved filters (Should), D2 timeline (Could), D3 SIEM/containment/multi-tenant work (Won't). No scheduled delivery or test-pass claim.

## Definition of done

PRD ready: stakeholders confirm or resolve A1–A3, budget/currency/caps, data policy, owners, measurable targets and MVP priorities. Product done: every Must criterion has linked passing evidence; security/privacy review and AI gate accepted; performance/restore and cost cutoff verified; operations owner accepts rollout/rollback; stakeholders accept pilot outcome. This document alone satisfies none of those product gates.
