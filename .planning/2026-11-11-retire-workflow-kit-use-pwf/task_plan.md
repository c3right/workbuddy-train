# 移除 Workflow Kit，改用 PWF

## Goal
移除本项目的 Kit 部署，由 PWF 维护可跨端接续的任务记录。授权与验收见 [TASK.md](TASK.md)。

## Next Step
切换已完成。远端接续时同步 `origin/main`，核对包含本记录的切换提交，再按 [任务索引](../README.md) 选定工作。

## Current Phase
已完成

## Phases

### Phase 1: 范围与现状
- [x] 核对 Kit 安装、历史状态与用户提供的参考规则。
- **Status:** complete

### Phase 2: 切换设计
- [x] 确定 PWF 单一任务入口、历史归档和 Git 边界。
- **Status:** complete

### Phase 3: 移除与迁移
- [x] 移除 Kit 部署与旧状态入口，写入规则、索引和历史指针。
- **Status:** complete

### Phase 4: 核验
- [x] 验证 PWF、导航、忽略规则和产品范围。
- **Status:** complete

### Phase 5: 交付
- [x] 记录实际验证和跨端可见条件。
- **Status:** complete

## Decisions Made
| Decision | Rationale |
|----------|-----------|
| 旧部署原文与执行档案分离 | 现行入口无 Kit 依赖，旧记录留作审计。 |

## Errors Encountered
| Error | Resolution |
|-------|------------|
