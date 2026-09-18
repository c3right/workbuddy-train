# WorkBuddy Train Documentation

This file is the first-level navigation for repository documentation. It complements the existing project README and does not replace the training materials under `training/`.

## Start Here

| Need | Read |
|---|---|
| Project overview and training-product entry | [`../README.md`](../README.md) |
| Project rules and Agent entry | [`../AGENTS.md`](../AGENTS.md) |
| Current Work | [`../agents/WORK_INDEX.md`](../agents/WORK_INDEX.md) |
| Project domain boundary | [`project/domain-entry.md`](project/domain-entry.md) |
| Runtime capabilities | [`operations/runtime-capabilities.md`](operations/runtime-capabilities.md) |
| README maintenance | [`operations/readme-navigation.md`](operations/readme-navigation.md) |

## Documentation Map

<!-- AWK:AUTO:DOCS_INDEX:BEGIN -->
| Area | Purpose | Entry |
|---|---|---|
| Training design and history | First-training design, implementation history and dry-run evidence | `FIRST-TRAINING-DESIGN-IMPLEMENTATION-HISTORY.md` |
| Design decisions | Accepted project-specific design decisions | `DESIGN-DECISIONS.md` |
| Operations | Repository operating procedures and runtime capability notes | `operations/` |
| Project domain | Project-specific purpose, ownership and product boundary | `project/domain-entry.md` |
| Current change contract | WBT-AWK-001 onboarding contract | `changes/WBT-AWK-001-workflow-kit-onboarding.md` |
| Second training proposal | Candidate Skill tutorial design | `SECOND-TRAINING-SKILL-TUTORIAL-DESIGN.md` |
<!-- AWK:AUTO:DOCS_INDEX:END -->

## Authority and Ownership

- Project rules and control-plane entry: `../AGENTS.md`.
- Current Work and Primary Task Contract pointers: `../agents/WORK_INDEX.md`.
- Agent Workflow Kit Base snapshots: `../agents/kit/*.md`.
- Project documentation and all content under `../training/` are Project Owned unless explicitly registered otherwise.
- The clean learner-facing/instructor-facing training package must not depend on repository-root Kit files.
- External Managed tools remain under their own lifecycle.

When sources conflict, follow the authority order exposed by `../AGENTS.md` and the current Primary Task Contract.

## Navigation Maintenance

Update this index when a major document is added, removed, renamed or changes responsibility. Only content inside `AWK:AUTO` markers is eligible for automatic refresh.

Maintenance procedure: [`operations/readme-navigation.md`](operations/readme-navigation.md).
