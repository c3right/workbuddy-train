# Findings & Decisions

## Requirements
- 移除 Workflow Kit；PWF 任务档案放在 `.planning/`；规则统一由 `AGENTS.md` 维护。

## Research Findings
- `main` 基线为 `b920d808`，旧 manifest 为 `0.2` / `skill-heavy`，安装了 11 份固定 Kit 快照。Override 为空；未发现本机 Kit 配置或 `local/`。
- WBT-AWK-001 已结项并集成。WBT-AWK-002 的最终暂停证据在 `7ac37ee8`，只提交了治理记录，未实施升级。
- 参考 Automotive Social Radar 的单一规则入口、TASK 授权与 PWF 状态分离、同一计划单一维护者、跨端以可核对的 Git 提交接续；不引入其业务约束或默认提交推送权限。

## Technical Decisions
| Decision | Rationale |
|----------|-----------|
| 退役 Kit，不再恢复 WBT-AWK-002 | 新决定取代升级意图，不改写旧授权、验收和分支。 |
| 历史证据与可执行计划分离 | 旧档放在 `.planning/history/`，不被识别为活动计划；项目入口仅指向新规则和索引。 |

## Issues Encountered
| Issue | Resolution |
|-------|------------|
| 首次检查命令使用了 PowerShell 不支持的路径花括号 | 改用明确路径；原生计划格式检查通过。 |

## Resources
- [历史入口](../history/README.md)
