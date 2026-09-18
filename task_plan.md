# 任务计划

## 工作信息

- 工作编号（Work ID）：`WBT-AWK-001`
- 主合同（Primary Task Contract）：`docs/changes/WBT-AWK-001-workflow-kit-onboarding.md`
- 当前 Assignment：`WBT-AWK-001-T02`
- 当前角色：`BOUNDED IMPL ONLY — WORKFLOW KIT FIRST ONBOARDING`
- 当前状态：`ACTIVE / T02 IMPLEMENTATION`
- 更新日期：`2026-09-18`
- Active Modules：`CORE`；Profile 专业 capability 保持 dormant，除非当前事实命中真实 seam。
- Scoped Standing Git Authorization：见 Primary Task Contract。

## 目标

只完成固定 source commit `9abc9b97d305432a589cf55923192378854ef283` 的 `common + skill-heavy` first onboarding，建立 repository-root control plane 与 Project Domain Entry，并保持 `training/**` 产品内容不变。

## 当前阶段

`WBT-AWK-001-T02` first onboarding implementation。

## 步骤

- [x] 核验 CTRL release commit 与 T01 accepted lineage。
- [x] 读取 selected Profile、Layer Manifests、first-onboarding / installation validation canonical guidance。
- [ ] 安装 Manifest required Project Owned / Kit Managed assets。
- [ ] 验证 Manifest union、snapshot content、entry / local-only boundary、training tree identity 与完整 diff。
- [ ] 在可运行环境执行 canonical read-only installation validator；当前 host 的 shell 无法解析 `github.com`，不能在本 session materialize 两个 repositories。
- [ ] exact commit + non-force push + remote HEAD verification。
- [ ] RETURN continuing WBT-AWK-001 CTRL；停止，不进入后续 Task。

## 下一准确动作

完成 T02 安装与远端机械验证后 RETURN CTRL；canonical validator execution evidence 若仍因 host 限制缺失，明确作为 blocker/warning 返回，不虚报 PASS。

## 依赖与阻塞

- Git 动作遵守 Primary Task Contract 的 Scoped Standing Git Authorization。
- canonical validator 需要同时可读取 target project root 与固定 Kit source root；当前 shell 网络条件不满足该执行前提。
- Trellis / Specialist / TDD / Production 不因 `skill-heavy` 自动激活。

## 退出条件

满足 T02 合同的安装、diff、Git 与远端验证要求，并诚实报告 validator execution 状态。
