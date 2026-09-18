# Session Routing

**版本：v0.2-draft**
**依赖：`core-protocol.md`、`planning-and-handoff.md`**

## 1. 目的与范围

本标准规定 CTRL、IMPL、REVIEW 的责任边界，以及 Session action、Context strategy 与 `RETURN` 的路由选择。

本标准不规定 Planning 三件套的具体内容、Git 操作方法或跨电脑 Transfer Snapshot。状态写入与普通 Handoff 由 `planning-and-handoff.md` 主责。

## 2. 角色边界

### CTRL

CTRL MUST 负责：

- 建立、确认和重大修改 Primary Task Contract；
- 定义范围、约束、风险和验收；
- 判断是否授权进入实施；
- 处理重大偏离和接受风险；
- 决定 Work Item 关闭。

### IMPL

IMPL MUST：

- 只在已批准范围内修改和验证；
- 把重大偏离、未授权依赖或新增风险返回 CTRL；
- 记录实施结果和修复证据；
- 不得自行扩大范围或宣布正式 Review 通过。

### REVIEW

REVIEW MUST：

- 检查合同、diff、测试和产物；
- 在 Formal Review 激活时维护 Finding、证据和结论；
- 复查修复或建议接受风险；
- 不得替代用户业务验收，也不得在未授权范围内实施功能修改。

同一执行主体 MAY 在不同阶段承担不同角色，但每次输出 MUST 明确当前责任角色。

## 3. Role topology 与 Session topology 分离

Role topology 描述“谁承担什么责任”，Session topology 描述“是否继续当前会话、是否创建新会话”。

两者 MUST 独立判断：

- role change 不自动要求 `CREATE`；
- Formal Review 不自动要求 `CREATE`；
- 多个角色不自动意味着多个会话；
- 同一角色 MAY 因连续性丢失、污染隔离、执行面能力或独立判断证据而 `CREATE`；
- bounded consecutive IMPL 在上下文仍可靠时 SHOULD 优先 `STAY`；
- 任务复杂、耗时、文件多或需要更强能力，单独均不构成 `CREATE` 理由。

## 4. Session action 与 Context strategy

### 4.1 Session action

Session action 只描述会话动作：

- `STAY`：继续当前会话；
- `CREATE`：创建新的顶层会话；
- `RETURN`：把结果或阻塞返回既定 Return Target。

### 4.2 Context strategy

Context strategy 只描述上下文处理：

- `CONTINUE`：现有上下文仍可靠，直接继续；
- `REFRESH`：保留当前会话与经验，只刷新已经改变或对下一动作必要的 repository facts；
- `BOUNDED`：新会话只恢复完成当前 assignment 所需的最小可靠上下文；
- `INDEPENDENT`：为独立判断、污染隔离或 evidence value 建立不继承原判断负担的上下文。

### 4.3 常用 2×2

```text
STAY + CONTINUE
STAY + REFRESH
CREATE + BOUNDED
CREATE + INDEPENDENT
```

这四种组合是常用路由，不是新的 lifecycle state，也不要求持久化 Session registry。

`Fresh Session`、`Cold Start`、`Full Historical Reload`、Formal Review、Protected Independent Review 是不同概念：

```text
Fresh Session
≠ Cold Start
≠ Full Historical Reload
≠ Formal Review
≠ Protected Independent Review
```

Cold Start 只要求新会话取得当前任务的最小可靠 authority/context；不得定义成重新学习整个 repository 历史。

## 5. `CREATE` 的真实触发

只有存在实际收益或 correctness requirement 时 SHOULD `CREATE`，典型理由包括：

- continuity loss：当前会话已无法可靠恢复下一步；
- context contamination：既有假设或历史判断会污染下一判断；
- responsibility isolation：某责任需要独立顶层上下文才能安全承担；
- execution-surface capability：下一动作需要当前会话不具备的执行能力；
- fresh judgement / independence 具有明确 evidence value；
- acceptance contract 明确要求 Protected Independent Review。

选择 `CREATE` 时 MUST 同时指定 `BOUNDED` 或 `INDEPENDENT`，并说明原因。Formal Review 本身、风险等级、规范性资产标签或 stronger capability need 不自动触发 `CREATE`。

## 6. `STAY` 的默认使用

当 assignment、授权和上下文仍可靠时 SHOULD 使用 `STAY`。

- 连续 bounded IMPL 默认优先 `STAY + CONTINUE`；
- repository facts 已变化但会话经验仍有效时使用 `STAY + REFRESH`；
- `STAY` 不免除读取当前动作所需事实，也不免除真实 fact delta 的 canonical-owner 更新。

## 7. 能力建议

Agent MAY 推荐：

```text
FAST
GENERAL
STRONG
```

或明确的能力类型，例如“需要可执行代码环境”“需要视觉判断”“需要独立审阅”。

Kit routing MUST NOT 绑定具体 vendor、model、provider 或商业产品名称。能力建议也不得替代用户授权或 execution-surface safety。

## 8. `RETURN`

完成受托工作、遇到合同级偏离、需要上级决定或命中停止条件时 MUST `RETURN`。

`RETURN` MUST 指向唯一 Return Target。`RETURN` 不自动要求新会话，也不自动要求修改 CURRENT；是否写入状态由 `planning-and-handoff.md` 的 Delta State Sync 与 durable recovery need 决定。

## 9. 正式 Routing 输出

正式 Routing SHOULD 包含：

```markdown
## Routing

- Decision: STAY / CREATE / RETURN
- Session Action: STAY / CREATE / RETURN
- Context Strategy: CONTINUE / REFRESH / BOUNDED / INDEPENDENT / N/A
- Current Role:
- Next Role:
- Work ID:
- Return Target:
- Handoff: <pointer / NOT_REQUIRED>
- Reason:
```

字段使用责任、上下文和状态语言，不绑定具体 vendor/model。

## 10. Cross-References

- 权威、Work Item 和所有权：`core-protocol.md`
- Delta State Sync、Minimum Sufficient Context、CURRENT 与 Task Capsule：`planning-and-handoff.md`
- Git 状态检查和用户门禁：`git-safety.md`
- 跨电脑接续：`portability-and-distribution.md`
- 轻量探索参考：`docs/reference/lightweight-exploration-reference.md`
- 计划性 CTRL 接续参考：`docs/reference/control-continuity-succession-reference.md`

## 11. Source Map

- KC-021 Frozen Full Design：Work C — Session Routing + Delta State + Lightweight / Succession References。
- KC-024 Primary Task Contract：RO-01、RO-03、RO-04。
