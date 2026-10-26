# Coding-agent handoff

Prepare a sequence that a beginner can follow without handing an agent an entire product in one ambiguous request.

## Phases

Use project-specific phases with entry/exit gates. A typical order is foundation and reproducible setup; one complete core journey; persistence and failure handling; secondary features; hardening and deployment. Adapt order to risk: validate a difficult camera/controller or an external-access dependency before producing extensive content.

Each phase states requirement IDs, user-visible outcome, modules affected, dependencies, owner or unassigned, estimate assumptions, acceptance checks and failure/stop conditions. Identify placeholders/mocks explicitly and plan their replacement. A phase is complete only with evidence, not because files exist.

## Copyable prompt contract

For each implementation slice, provide:

- Context: project goal, confirmed stack, constraints and relevant requirement IDs.
- Task: one bounded user-visible change and the decisions already made.
- Boundaries: exclusions, allowed resources and secrets/data constraints.
- Contracts: state/schema/API or component boundaries that must hold.
- Checks: actions and observable expected results, including an important failure path.
- Report: changes, verification actually performed, remaining gaps and next step.
- Stop: conditions requiring a decision, such as destructive migration, unavailable credentials, unexplained test regression or budget-impacting service addition. Follow existing user authorization; do not invent repetitive approval gates.

Do not tell the implementation agent to claim success, skip errors or continue unlimited retries. Avoid prompts that build unrelated features. Include a concrete first prompt for the current project, not just this template.

## Beginner review guide

After each slice tell the user: how to launch or inspect the result; what happy-path action to try; what failure to simulate; what observable result constitutes success; what evidence to retain; what to send back if it fails. Explain that screenshots alone do not verify data integrity or authorization.

End with a definition of done that distinguishes planning ready, prototype playable/useful and production ready. Include remaining decisions and a traceability matrix. Review scope and dependencies when requirements change; do not silently rebuild the whole system.
