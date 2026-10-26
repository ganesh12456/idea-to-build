# Verification and limitations

Structural checks passed: required name/description frontmatter, five entrypoint references resolving to real files, no unfinished scaffold markers, UTF-8 encoding and archive integrity.

Manual contract review (not an independent agent execution):
- Problem-only request: first-turn contract now requires suggestions, all eight categories, initial architecture/storage choice and a short question batch.
- Three.js single-player game: example demonstrates scene/state ownership, controller/collision risks, local save schema, corrupt-save behavior and a concrete bounded first prompt. Backend/database/AI are not forced.
- Credit ledger: engineering reference requires money representation, transactional correctness, reversals/history and balance rules when applicable; browser-only persistence cannot silently substitute for shared authoritative records.
- AI investigator: retained example and general instructions require grounding, evaluation and failure handling, with proposed gates separate from measured results.
- Full-plan request: explicitly requires architecture, core principles, storage schema/setup, contracts, phases and handoff beyond the eight-category PRD.

These are document and scenario reviews, not proof of future model behavior. No independent model benchmark or application tests were performed. Standard quick_validate.py remains unavailable because PyYAML is missing. The prior installed version is discoverable in the host catalog; this updated output copy is NOT installed. Updating the protected installed folder was denied by the filesystem policy. This record describes pre-publication validation; publication does not change the installed workspace copy.
