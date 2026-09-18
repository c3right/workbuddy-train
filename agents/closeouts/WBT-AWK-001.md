# WBT-AWK-001 Closeout

## Metadata

- Work ID：`WBT-AWK-001`
- Title：`Workflow Kit First Onboarding + Training Product Boundary Refactor`
- Type：`REPOSITORY_GOVERNANCE_ONBOARDING / TRAINING_PRODUCT_BOUNDARY`
- Final Status：`ACCEPTED / CLOSED / INTEGRATED`
- Closed：`2026-09-18`
- Work Branch：`work/wbt-awk-001-workflow-kit-onboarding`
- Branch Baseline：`6dabf4aefd70ceb50a68b29f0b9aa06ba1b55379`
- Primary Contract：`docs/changes/WBT-AWK-001-workflow-kit-onboarding.md`
- Workflow Kit Source：`c3right/agent-workflow-kit@9abc9b97d305432a589cf55923192378854ef283`
- Profile：`skill-heavy`
- T01 Accepted HEAD：`8540d9febc9817c6a7af64df0192a06b3012d37a`
- T02 Implementation HEAD：`7932827ae506e1ab92819dc8a265d317c7c5d1c0`
- T03 Validated Target：`77c9f751922f346e1719628de2cc72848f9e5309`
- Pre-integration Accepted Work HEAD：`f8873edf6ec3f820ad2542e97ebaa8470cea5a59`
- Formal Review：`NOT_REQUIRED`
- Blocking Findings Remaining：`0`
- User Integration Authorization：`YES — 2026-09-18`
- Default-branch Integration：`PERFORMED / NON-FORCE FAST-FORWARD`
- Tag / Release / Publication：`NOT_REQUESTED`

## Original Goal

把 `workbuddy-train` 从混合培训内容仓库重构为：

```text
repository root
= Workflow-Kit-governed training development workspace

training/
= Project Owned training-product source

learner-facing package
= clean standalone artifact without Workflow Kit
```

并以固定 Kit source 的 `skill-heavy` Profile 完成首次正式接入。

## Final Result

1. 将原 root `learner/`、`instructor/`、`lab/` 统一迁移到 `training/` 产品树。
2. learner-facing `training/lab/新岚汽车渠道研究项目/` 保持沉浸式项目语义，不部署 Kit、不注入治理术语。
3. repository root 完成 `common + skill-heavy` first onboarding。
4. 建立 `AGENTS.md`、`.workflow-kit.yml`、Project Domain Entry、Planning / Handoff、Override registry、Operations 与 Profile-required assets。
5. 11 个 `agents/kit/*` snapshots 与固定 source commit 对应 blob SHA 全部一致。
6. `training/` 在 T02 前后 tree SHA 完全一致，培训产品内容未因 Kit 接入发生变更。
7. Profile capability 保持按真实 seam 激活；Trellis / Specialist / TDD / Production 未因 `skill-heavy` 自动启用。

## Validation Evidence

### T01 — Training Product Boundary Refactor

CTRL verdict：`PASS / COMPLETE`

- old root product directories：removed / migrated；
- learner files：content-identical rename；
- Lab：content-identical rename；
- XLSX / PNG / DOCX blob identity：PASS；
- Kit installation leakage：NONE；
- scope deviation：NONE。

### T02 — Workflow Kit First Onboarding

CTRL verdict：`IMPLEMENTATION ACCEPTED`

- selected layers：`common + skill-heavy`；
- required Kit Managed targets：`11/11`；
- required Project Owned targets：`18/18`；
- Kit Managed source identity：`PASS 11/11`；
- training product identity：`PASS / tree unchanged`；
- Override registry：empty / valid；
- local-only boundary：configured and ignored；
- scope deviation：NONE。

### T03 — Canonical Installation Validator

Computer-side/local canonical validator：

```text
status: PASS_WITH_WARNINGS
exit_code: 0
errors: 0
warnings: 1
```

Warning：

`MERGE_HISTORY_NOT_FULLY_VERIFIABLE` — no merge baseline; arbitrary historical prose preservation cannot be mechanically proven.

CTRL disposition：non-blocking evidence limitation；不是 installation-integrity error。

原 environment blocker `F-T02-ENV-001` 已 CLOSED。

## Git / Integration Evidence

- pre-integration `main`：`6dabf4aefd70ceb50a68b29f0b9aa06ba1b55379`
- integrated Work object：`f8873edf6ec3f820ad2542e97ebaa8470cea5a59`
- compare before integration：Work branch ahead 7 / behind 0
- mechanics：non-force fast-forward
- merge commit：NONE
- conflicts：NONE
- post-transition verification：`main == f8873edf6ec3f820ad2542e97ebaa8470cea5a59`
- force push / rebase / reset-clean：NONE

## README / Navigation Freshness

- README / Navigation Freshness：`PASS`
- Updated Entry Surfaces：`README.md`, `docs/README.md`, `AGENTS.md`, `docs/project/domain-entry.md`, `.workflow-kit.yml`
- Source Map Updated：`YES`
- Closeout itself introduces no new product-facing navigation requirement.

## Production Impact

`NOT_APPLICABLE`

本 Work 未激活正式 production seam，没有 existing production run 需要重跑或重建。

## Known Limitation

唯一已知限制是 validator 的 merge-history warning：由于没有 merge baseline，无法机械证明任意历史 prose 的全量保留。T01/T02 的真实 diff、blob identity、README merge 与人工/CTRL 检查提供了本 Work 的实际保留证据。

## Planning Archive

- `agents/planning-archive/WBT-AWK-001/task_plan.md`
- `agents/planning-archive/WBT-AWK-001/findings.md`
- `agents/planning-archive/WBT-AWK-001/progress.md`

根 Planning 三件套在 Closeout 后恢复为空闲状态。

## Kit Feedback

```text
Kit Feedback: NONE
```

本 Work 没有形成新的、可复用且尚未被 Kit 当前规则覆盖的稳定缺陷。remote shell 无法运行 validator 属 execution-surface limitation，已由现有“按能力切换 execution surface + evidence honesty”规则正确处理。

## Final Boundary

`WBT-AWK-001` 已完成并集成到 `main`。Repository control plane 返回无活动 Formal Work。

后续新的教程开发、第二次培训 Skill 设计、Kit upgrade、tag、Release 或 publication 均属于新的 scope，需要按当时事实重新进入 Work / 授权判断。
