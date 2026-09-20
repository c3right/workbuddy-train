# 任务计划

## 工作信息

- 工作编号（Work ID）：`WBT-AWK-002`
- 主合同（Primary Task Contract）：`docs/changes/WBT-AWK-002-kit-upgrade-latest.md`
- 当前 Assignment：`WBT-AWK-002-T01`
- 当前角色：`BOUNDED IMPL ONLY — KIT UPGRADE MIGRATION`
- 当前状态：`ACTIVE / T01`
- 更新日期：`2026-09-20`
- Old Kit source：`9abc9b97d305432a589cf55923192378854ef283`
- New Kit source：`ad641919f612880f493f2dc73fd3a8eb4df91253`
- Profile：`skill-heavy`
- Scoped Standing Git Authorization：见 Primary Contract。

## 目标

只执行 WBT-AWK-002-T01：把当前 Manifest 0.2 安装升级到固定新 source 的 Manifest 0.3，包括 Planning Layout v2 migration、Kit snapshots refresh 和 Project Owned entry merge，同时保持 `training/**` 不变。

## 当前阶段

T01 upgrade migration implementation。

## 下一准确动作

由 bounded IMPL 读取 Primary Contract 与固定新 Kit source，实施 T01；完成后 RETURN CTRL，不进入 validator 或 main integration。

## 依赖与阻塞

- 当前无已知 blocker。
- `.planning/**` 是 External Managed，禁止纳入迁移。
- default-branch integration 未授权。

## 退出条件

T01 完成 scoped commit + non-force push + evidence RETURN。
