# 任务计划

## 工作信息

- 工作编号（Work ID）：`WBT-AWK-001`
- 主合同（Primary Task Contract）：`docs/changes/WBT-AWK-001-workflow-kit-onboarding.md`
- 当前 Assignment：`WBT-AWK-001-T03`
- 当前角色：`BOUNDED VALIDATION ONLY — INSTALLATION VALIDATOR COMPLETION`
- 当前状态：`ACTIVE / T03 ENVIRONMENT RETRY`
- 更新日期：`2026-09-18`
- Active Modules：`CORE`；Profile 专业 capability 保持 dormant。
- Scoped Standing Git Authorization：见 Primary Task Contract；T03 本身默认只读。

## 目标

只补齐 canonical `scripts/validate_installation.py` 的真实执行证据，验证当前 target branch 与固定 Kit source `9abc9b97d305432a589cf55923192378854ef283` 的安装完整性。

## 当前阶段

`WBT-AWK-001-T03` validation-only；remote shell 尝试已因环境阻断，继续同一 Task，但切换 computer-side/local execution surface。

## 步骤

- [x] T01 product-boundary refactor：CTRL PASS。
- [x] T02 common + skill-heavy first onboarding implementation：CTRL implementation accepted。
- [x] CTRL 独立核对 11/11 Kit Managed blob identity 与 `training/` tree identity。
- [x] T03 remote validation attempt：环境阻断，validator 未启动。
- [ ] 在能同时持有 target + fixed Kit source 完整 Git checkout 的 computer-side/local 环境运行 canonical read-only validator。
- [ ] 记录 command、target HEAD、source commit、exit code、status 与 findings。
- [ ] RETURN continuing WBT-AWK-001 CTRL；停止，不自行修复。

## 下一准确动作

在 computer-side/local 环境 checkout：
- target branch / HEAD = 当前 T03 entry HEAD；
- Kit source = `9abc9b97d305432a589cf55923192378854ef283`；

然后运行 canonical read-only validator。若 `PASS` / `PASS_WITH_WARNINGS`，返回证据；若 `FAIL` / `NOT_VERIFIABLE`，同样只 RETURN，不修改安装。

## 依赖与阻塞

- 当前 open finding：`F-T02-ENV-001`。
- remote shell 已证明不满足执行前提。
- 下一 surface 必须能同时读取两个完整 Git checkout。
- 不授权 main integration、Release、tag、semantic remediation。

## 退出条件

canonical validator 获得真实执行结果并返回 CTRL。
