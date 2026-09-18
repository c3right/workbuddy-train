# WorkBuddy Train — Project Domain Entry

## Project Purpose

- Project goal：维护面向非技术同事的 WorkBuddy 实操培训教程及其配套教学材料。
- Profile：`skill-heavy`
- Public entry：`README.md`
- Documentation entry：`docs/README.md`
- Training product source：`training/`

## Domain Vocabulary

- **Training product source**：`training/` 下的学员、讲师与 Lab 产品源。
- **Learner-facing fixture**：`training/lab/新岚汽车渠道研究项目/`；保持真实咨询项目口吻，不注入治理术语。
- **Development control plane**：repository root 的 Workflow Kit 资产，只治理教程研发仓库，不属于最终培训产品。

## Authoritative Project Sources

| Topic | Authority source | Read when |
|---|---|---|
| Project purpose and current training status | `README.md` | 判断项目目标、受众与当前培训状态时 |
| Current onboarding Work | `docs/changes/WBT-AWK-001-workflow-kit-onboarding.md` | 执行 WBT-AWK-001 时 |
| Accepted project-specific decisions | `docs/DESIGN-DECISIONS.md` | 判断已接受设计边界时 |
| First-training design/history | `docs/FIRST-TRAINING-DESIGN-IMPLEMENTATION-HISTORY.md` | 修改第一次培训结构或材料时 |
| Training product source | `training/` | 修改或打包学员/讲师/Lab 内容时 |
| Second-training Skill tutorial proposal | `docs/SECOND-TRAINING-SKILL-TUTORIAL-DESIGN.md` | 讨论第二次培训候选方案时 |

## Repository Areas

| Path | Domain responsibility |
|---|---|
| `training/` | Project Owned training-product source |
| `docs/` | Project Owned design, history, operations and change contracts |
| `agents/` | Workflow Kit control-plane state and fixed Kit Base snapshots |
| `production/manifests/` | Profile-provided run manifest template; used only when a real production-run seam is activated |

## Domain Constraints

- `training/**` is product source. Do not place `AGENTS.md`, `.workflow-kit.yml`, `agents/`, Planning ledgers or other Kit control-plane assets inside it.
- Learner-facing and instructor-facing packages copied/exported from `training/` must be clean standalone artifacts and must not depend on repository-root Workflow Kit context.
- `training/lab/新岚汽车渠道研究项目/` keeps its immersive project semantics; repository governance language belongs outside the learner-facing fixture.
- Existing training content, design decisions and project facts are Project Owned and are not replaced by Kit templates.
- The selected `skill-heavy` Profile reflects a documentation/content-production repository. It does not automatically activate formal Skill Change, Specialist Execution Plane, Software TDD, Trellis or Production work.

## Profile Overlay

- 正式 Skill 目录：当前无正式 Skill 资产；未来只有在获授权 Work 明确创建或修改正式 Skill 时才建立。
- Skill、Reference、Script、Asset 和输入输出合同变更仅在真实 formal Skill seam 命中时进入 Skill Change Control。
- 正式或可复用生产批次只有在真实 production seam 激活时才建立 `production/manifests/RUN-ID.yml`。
- Trellis 默认不启用；辅助代码遵守适用的软件规则和 Git 门禁。
- 生产设施变化只有在实际生产设施存在并被当前 Work 命中时才判断旧成果影响和重跑责任。

## Override Anchors

当前没有 Registered Override；`agents/overrides/registry.json` 保持空 registry。未来如确需偏离 Kit Base，先建立稳定 Project Owned rule anchor，再按 Base 的 Override 生命周期审查与登记。
