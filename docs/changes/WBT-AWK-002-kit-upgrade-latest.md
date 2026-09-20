# WBT-AWK-002 — Workflow Kit Upgrade to Latest

## Status

- Role owner: CTRL
- Lifecycle: ACTIVE
- Method: Lightweight Exploration Reference Pattern
- Repository: `c3right/workbuddy-train`
- Work branch: `work/wbt-awk-002-kit-upgrade-latest`
- Target baseline: `b920d80823303d3f69dbb04e346b8ef2df55b477`
- Old Kit source: `c3right/agent-workflow-kit@9abc9b97d305432a589cf55923192378854ef283`
- New Kit source: `c3right/agent-workflow-kit@ad641919f612880f493f2dc73fd3a8eb4df91253`
- Profile: `skill-heavy`
- Upgrade contract: Manifest / workflow `0.2 -> 0.3`
- Return target: continuing WBT-AWK-002 CTRL

## Goal

把当前已安装 Workflow Kit 从旧 source `9abc9b97...` 升级到最新固定 source `ad641919...`，保持项目领域语义与 `training/**` 产品内容不变。

## Confirmed Upgrade Facts

1. Current installation is clean against old Base: 11/11 Kit Managed snapshots match old source.
2. Registered Override registry is empty.
3. New Manifest schema is `0.3`.
4. Planning Layout v2 is a required-path migration:
   - `/task_plan.md` -> `agents/planning/current/task_plan.md`
   - `/findings.md` -> `agents/planning/current/findings.md`
   - `/progress.md` -> `agents/planning/current/progress.md`
   - `agents/planning-archive/**` -> `agents/planning/archive/**`
5. `.planning/**` is External Managed and is outside migration scope.
6. The following Kit Managed source assets changed between old and new Base and must be refreshed from the fixed new source:
   - `agents/kit/core-protocol.md`
   - `agents/kit/planning-and-handoff.md`
   - `agents/kit/lightweight-exploration-reference.md`
   - `agents/kit/control-continuity-succession-reference.md`
7. Unchanged Kit Managed snapshots must still remain content-matched to the new fixed source.
8. Project Owned templates with material upgrade delta include:
   - `AGENTS.md`
   - `.workflow-kit.yml`
   - `agents/WORK_INDEX.md`
   - `agents/handoffs/CURRENT.md`
   - Planning current triplet at the new paths.
9. `AGENTS.md` latest template changes Reference invocation to explicit canonical Adoption Rules copy-and-send routing; merge must preserve WorkBuddy Train project identity while adopting the new protocol.
10. `training/**` is outside semantic upgrade scope and must remain content-identical.

## Execution Model

```text
CTRL releases one bounded Task
→ IMPL performs only that Task
→ IMPL RETURN and stop
→ CTRL independently reviews actual diff/evidence
→ next Task only after review
```

No default-branch integration is authorized by this Work initialization.

## Task Sequence

### WBT-AWK-002-T01 — Upgrade Migration Implementation

**Status: RELEASED BY CTRL**

Apply the fixed new Kit source to the current `skill-heavy` installation.

Required scope:

1. perform the explicit Planning Layout v2 migration, preserving current and archived content/semantics and favoring Git rename/move identity;
2. remove legacy root planning triplet and legacy `agents/planning-archive/**` runtime/archive paths after successful migration;
3. update `.workflow-kit.yml` to source `ad641919...`, Manifest version `0.3`, and exact `common + skill-heavy` required target lists;
4. refresh all Kit Managed snapshots from the fixed new source, changing bytes only where the new source changed;
5. merge required Project Owned entry changes without overwriting project-specific facts;
6. update path-only navigation/recovery references required by the Planning Layout migration;
7. preserve `training/**` byte-identically;
8. run all available remote/mechanical checks and full diff review;
9. exact commit + non-force push current Work branch;
10. RETURN and stop.

### WBT-AWK-002-T02 — Canonical Installation Validation

Only released after CTRL accepts T01 implementation.

Run canonical read-only validator against the exact post-T01 target and fixed Kit source. If remote execution cannot materialize both repositories, switch execution surface rather than weakening the evidence requirement.

## Hard Boundaries

Do not:

- edit `training/**` product content;
- read, migrate, delete or synchronize `.planning/**`;
- create Overrides;
- activate Trellis / Specialist / TDD / Production merely because of the upgrade;
- modify Kit Managed snapshots by hand;
- perform default-branch integration, tag, Release or publication;
- silently preserve legacy root planning files or `agents/planning-archive/**` as runtime fallback.

## Validation / Acceptance

T01 acceptance requires:

- Planning Layout v2 migration correctness;
- exact Manifest `0.3` required lists;
- all 11 Kit Managed snapshots content-match the fixed new source;
- Project Owned semantics preserved;
- no forbidden legacy planning runtime paths;
- `training/**` unchanged;
- no Override/local-only boundary regression;
- scope-clean diff and remote checkpoint.

Final Work acceptance additionally requires canonical validator `PASS` or `PASS_WITH_WARNINGS` with zero errors.

## Scoped Standing Git Authorization

- Repository: `c3right/workbuddy-train`
- Work / Goal: `WBT-AWK-002`
- Allowed branch: `work/wbt-awk-002-kit-upgrade-latest`
- Allowed actions: exact scoped writes for released Task, semantic commit, non-force push, postcondition verification
- Rollback anchor: `b920d80823303d3f69dbb04e346b8ef2df55b477`
- Preconditions: branch/baseline/scope remain consistent; no unexplained dirty ownership; no default-branch mutation
- Forbidden: default-branch integration, force push, rebase/amend/shared-history rewrite, reset/clean/discard, tag, Release/publication
- Authorization source: user requested deployment of latest Workflow Kit on 2026-09-20
- Expiry: Work closeout, scope/branch/baseline drift, user revocation, or protected action request

## Current CTRL Decision

Release exactly one Task: `WBT-AWK-002-T01 — Upgrade Migration Implementation`.

No independent Formal Review is required at entry. CTRL will judge the actual migration diff and evidence before releasing canonical validation.
