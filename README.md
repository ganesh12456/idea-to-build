# Idea to Build

Give your coding agent a problem statement. This reusable Agent Skill suggests what to build, asks a few important questions, and turns decisions into a practical plan. You do not need technical context or complete requirements to start.

## What you get

- Suggested users, solution directions and features, with reasons and tradeoffs.
- A scoped MVP, user journeys/stories and MoSCoW priorities.
- Eight core categories: Business, Functional, AI, Data, Frontend, Backend, Nonfunctional, Delivery. AI is N/A when unnecessary.
- Architecture options, budget constraints, phases, dependencies, risks, security/privacy, AI evaluation when applicable, acceptance criteria, testing/deployment checklist, traceability and a definition of done.
- Clear distinctions between confirmed facts, recommendations and assumptions.

## Install

Copy the complete `skills/project-requirements-architect` folder into your Codex project's `.agents/skills/` folder. The resulting entrypoint is `.agents/skills/project-requirements-architect/SKILL.md`.

The repository name is `idea-to-build`; the skill invocation name is `project-requirements-architect`. Other coding agents must support Agent Skills and use their documented discovery locations. This does not install anything in ChatGPT's global catalog.

## Use

```text
Use $project-requirements-architect. Small shops struggle to track customer credit. I only have this problem statement; suggest what to build and guide me through the important decisions.
```

```text
Use $project-requirements-architect for a volunteer shift scheduler. No AI. Suggest an MVP and draft requirements with assumptions clearly labeled.
```

```text
Use $project-requirements-architect for an AI Security Incident Investigator using FastAPI, React and PostgreSQL. Ask the important missing questions first.
```

The [security investigator example](skills/project-requirements-architect/references/ai-security-example.md) is one illustration, not the skill's only use case. Its output is a proposed plan, not implemented software or passing product tests.

## Validation

No runtime dependencies are required to use the skill. It contains instructions, two references and optional Codex UI metadata. Local discovery was confirmed by the host's available-skills catalog after creation. Structural checks and manual AI/non-AI workflow reviews were completed. No independent model benchmark was run. The standard Python validator remained blocked by missing PyYAML. See [VALIDATION.md](VALIDATION.md).
