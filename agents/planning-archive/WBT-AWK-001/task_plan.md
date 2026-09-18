# 任务计划

## 工作信息

- 工作编号（Work ID）：`WBT-AWK-001`
- 主合同（Primary Task Contract）：`docs/changes/WBT-AWK-001-workflow-kit-onboarding.md`
- 当前 Assignment：`NONE — HUMAN DECISION`
- 当前角色：`CTRL`
- 当前状态：`ACTIVE / READY_FOR_INTEGRATION_DECISION`
- 更新日期：`2026-09-18`
- Active Modules：`CORE`；Profile 专业 capability 保持 dormant。
- Scoped Standing Git Authorization：当前 authorization 不覆盖 default-branch integration。

## 目标

Workflow Kit first onboarding 已完成实现与 canonical validation。当前只决定是否将已验证 Work branch 集成到 `main` 并随后 closeout。

## 当前阶段

Human integration decision。

## 已完成

- [x] T01 training product boundary refactor：CTRL PASS。
- [x] T02 common + skill-heavy first onboarding：CTRL implementation accepted。
- [x] 11/11 Kit Managed snapshot identity：PASS。
- [x] `training/` product identity：PASS / unchanged。
- [x] T03 canonical read-only installation validator：`PASS_WITH_WARNINGS` / exit 0 / 0 errors。
- [x] F-T02-ENV-001：CLOSED。
- [x] Integration baseline check：`main` unchanged at baseline；Work branch ahead / behind 0。

## 下一准确动作

等待用户明确决定是否授权 default-branch integration。

若授权，再释放一个 integration/closeout action；未授权则保持 Work branch 为已验证 checkpoint。

## 当前决策边界

Protected action：

- default-branch integration / push to `main`
- closeout after integration
- tag / Release / publication

均不得由现有 standing authorization 推定。

## 退出条件

用户决定 integration；若完成 integration，再执行相称 closeout。
