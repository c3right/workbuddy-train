# 当前会话交接

- Work ID：`WBT-AWK-002`
- 来源角色：`CTRL`
- 目标角色：`future CTRL resume`
- Session Action：`STAY`
- Context Strategy：`REFRESH`
- Fresh Independence：`NO`
- Execution Surface：`REMOTE`
- Return Target：`USER`
- 准备日期：`2026-09-20`

## 当前状态

WBT-AWK-002 已在 T01 substantive implementation 前暂停。

暂停原因：上游 Workflow Kit 的 planned CTRL succession / forced reconstitution UX 与 successor prompt packaging 需要先澄清并修订。

## Authority Pointers

- Lifecycle：`agents/WORK_INDEX.md`
- Primary Task Contract：`docs/changes/WBT-AWK-002-kit-upgrade-latest.md`
- Current Planning：root `task_plan.md / findings.md / progress.md`（项目仍处 Manifest 0.2）
- Install record：`.workflow-kit.yml`

## 恢复原则

恢复本 Work 时不得直接沿用旧 T01 dispatch 或旧 new-source SHA。先 refresh target facts 与新的 accepted Kit source，再更新 upgrade delta / contract。

## Do Not Do

暂停期间：

- 不执行 T01；
- 不执行 validator；
- 不更新 `main`；
- 不修改 `training/**`；
- 不触碰 `.planning/**`；
- 不 tag / Release / publication。
