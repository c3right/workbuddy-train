# 任务计划

## 工作信息

- 工作编号（Work ID）：`WBT-AWK-002`
- 主合同（Primary Task Contract）：`docs/changes/WBT-AWK-002-kit-upgrade-latest.md`
- 当前 Assignment：`NONE — SUSPENDED BEFORE T01`
- 当前角色：`CTRL`
- 当前状态：`SUSPENDED / WAITING_FOR_UPSTREAM_KIT_REVISION`
- 更新日期：`2026-09-20`
- Old Kit source：`9abc9b97d305432a589cf55923192378854ef283`
- Previously targeted Kit source：`ad641919f612880f493f2dc73fd3a8eb4df91253`
- Profile：`skill-heavy`

## 目标

等待 Workflow Kit 上游完成 CTRL planned succession / forced reconstitution 使用流程澄清后，再以新的固定 Kit source 重新刷新升级差异并继续部署。

## 当前阶段

暂停。T01 substantive implementation 尚未开始。

## 已完成

- [x] upgrade delta analysis；
- [x] WBT-AWK-002 Work / branch / Primary Contract initialization；
- [x] old installation drift check：11/11 PASS；
- [x] identified Manifest 0.2 → 0.3 Planning Layout v2 migration；
- [ ] T01 implementation — NOT STARTED；
- [ ] canonical validator — NOT RELEASED；
- [ ] main integration — NOT AUTHORIZED。

## 下一准确动作

等待上游 Kit 修订完成。恢复时：

1. refresh `workbuddy-train/main` 与 Work branch；
2. 获取新的 fixed Kit source commit；
3. 重新比较当前 installed source → new source 的真实 installation delta；
4. 更新 Primary Contract 后再决定是否重新释放 T01。

## 依赖与阻塞

- Blocker：上游 CTRL succession / reconstitution UX semantics 待澄清。
- 不把此前 `ad641919...` 继续视为未来部署目标；恢复时以新的 latest accepted source 为准。
- default-branch integration 未授权。

## 退出条件

上游 Kit revision accepted，并由 CTRL 明确恢复本 Work。
