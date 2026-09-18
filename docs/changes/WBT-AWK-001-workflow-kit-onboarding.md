# WBT-AWK-001 — Workflow Kit First Onboarding + Training Product Boundary Refactor

## Status

- Role owner: CTRL
- Lifecycle: ACTIVE
- Method: Lightweight Exploration Reference Pattern
- Repository: `c3right/workbuddy-train`
- Work branch: `work/wbt-awk-001-workflow-kit-onboarding`
- Target baseline: `6dabf4aefd70ceb50a68b29f0b9aa06ba1b55379`
- Workflow Kit source: `c3right/agent-workflow-kit@9abc9b97d305432a589cf55923192378854ef283`
- Deployment mode: FIRST_ONBOARDING
- Intended profile: `skill-heavy`
- Return target: continuing WBT-AWK-001 CTRL

## Goal

把 `workbuddy-train` 重构为由 Workflow Kit 治理的“培训教程研发仓库”，同时保持培训教程及学员运行包本身不携带 Workflow Kit。

目标模型：

```text
repository root
= development workspace + Workflow Kit control plane

training/
= training product source

exported / copied learner-facing package
= clean standalone artifact, no Workflow Kit control surface
```

## Accepted Decisions

1. Workflow Kit 部署在 repository root，不部署到单独 development 子目录。
2. 培训教程作为产品成果本身不部署 Kit。
3. 现有 `learner/`、`instructor/`、`lab/` 可重组到统一 `training/` 产品树。
4. 学员实际打开的沉浸式项目继续保持无 `AGENTS.md`、无项目级 Skill、无 Git/Trellis/治理术语。
5. 研发仓库与 learner-facing runtime/package 必须形成清晰边界。
6. Workflow Kit profile 使用 `skill-heavy`；专业 capability 按真实 seam 惰性激活，不因 profile 自动启用 Skill/TDD/Specialist/Trellis/Production。
7. 项目现有 README、设计决定、教程和验证材料均视为 Project Owned；不得用 Kit 模板覆盖正文。

## Product Boundary

### Development / governance surface

允许包含 Workflow Kit 控制面、研发设计、验证、历史和发布准备。

### Training product surface

目标产品源根：`training/`。

至少承载：

- `training/learner/`
- `training/instructor/`
- `training/lab/`

其中 `training/lab/新岚汽车渠道研究项目/` 是 learner-facing fixture，必须保持沉浸式真实项目口吻。

### Clean-package invariant

面向学员/讲师的独立交付包不得依赖 repository-root Workflow Kit context。Learner-facing runtime 不得因父级控制文件继承而获得隐藏能力。

## Execution Model

按 Lightweight Exploration Reference 单步推进：

```text
CTRL release one IMPL Task
→ IMPL execute bounded scope
→ IMPL RETURN and stop
→ CTRL independently review diff/evidence
→ continue / targeted remediation / pivot / stop / human decision
```

不预建 child Work；不因流程完整性自动增加 Formal Review 或 Fresh Session。

## Task Sequence

### WBT-AWK-001-T01 — Training Product Boundary Refactor

只做目录/产品边界重构，不安装 Workflow Kit。

Expected semantic changes:

- `learner/` → `training/learner/`
- `instructor/` → `training/instructor/`
- `lab/` → `training/lab/`
- 研发文档按需要整理到更清晰的 `docs/` 子域，但不得为了形式机械搬迁。
- 更新所有受影响的 Markdown 路径、导航、reset 说明和教程引用。
- 保持二进制资产内容不变。
- 不新增 `AGENTS.md`、`.workflow-kit.yml`、`agents/` 或 Kit snapshots。

Exit criteria:

1. training product root 清晰；
2. 所有已知内部链接和路径引用与新位置一致；
3. learner-facing fixture 内容语义未被治理术语污染；
4. 无 Kit 安装文件；
5. diff 仅服务于产品边界重构；
6. exact commit + non-force push to Work branch；
7. RETURN 后停止。

### WBT-AWK-001-T02 — Workflow Kit First Onboarding

只有 T01 经 CTRL Review 通过后释放。

目标：按 `skill-heavy`、source `9abc9b97...` 将 Kit 部署到 repository root，建立 Project Domain Entry，并保持 `training/` 为 Project Owned product source。

### Later Tasks

只在前一 Task Review 后按真实需要释放；不在本合同中预授权 main integration、Release 或 publication。

## Scoped Standing Git Authorization

- Repository: `c3right/workbuddy-train`
- Work / Goal: `WBT-AWK-001`
- Allowed branch: `work/wbt-awk-001-workflow-kit-onboarding`
- Allowed actions: branch create, exact scoped writes, exact stage/commit equivalent, non-force push, postcondition verification
- Target baseline: `6dabf4aefd70ceb50a68b29f0b9aa06ba1b55379`
- Rollback anchor: same baseline
- Preconditions: write scope equals current released Task; no default-branch mutation; no force/history rewrite; no unexplained scope drift
- Forbidden: default-branch push/merge, force push, reset/clean/discard, shared-history rewrite, tag, Release/publication
- Authorization source: user approved deployment plan and assigned current session as CTRL on 2026-09-18
- Expiry: Work closeout, scope/branch/baseline drift, user revocation, or protected action request

## Current CTRL Decision

Release exactly one implementation task: `WBT-AWK-001-T01`.

No independent Formal Review is required at entry. CTRL will review the real T01 diff and evidence before any Kit installation task is released.
