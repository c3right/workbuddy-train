# 轻量探索 Reference Pattern

**定位：Reference Pattern / non-owner**  
**适用：边界清晰、可分段推进、需要快速试探但仍受现有 Authority / Git / Review / production 保护边界约束的探索或 bounded IMPL**

本参考把现有 canonical standards 已允许的行为组合成一套可直接执行的轻量运行方式。它不是 Mode、Profile、lifecycle、state machine 或新的 authority；不得新增 `LIGHTWEIGHT_MODE`。与 canonical standard 冲突时，canonical owner wins。

> **Core Principle：长期控制、单步执行、文件承载状态、执行后停手、Review 后再继续；人的视角只保留 Task ID、进度、结果和必要决策。**

## 1. Agent 运行层总则

1. **单一 Work 持续推进。** 默认在同一 Formal Work 内连续探索，不为每个小试探拆 child Work，也不预建大量 Phase。每轮只释放并推进一个最小且有价值的 Task / material bounded advance。
2. **长期 CTRL + REVIEW 掌舵，IMPL 执行。** 同一长期 CTRL 默认持续承担控制与判卷责任：定义当前 Task、接收 IMPL RETURN、独立判断完成条件，再决定下一步。这里的 “Review” 是 CTRL 的判卷动作；Formal / Independent REVIEW 仍按现有 Review 规则单独触发。
3. **IMPL 完成本轮即 RETURN 并停止。** IMPL 不自行进入下一 Task，不扩大 scope，不把“还有明显下一步”解释为继续执行授权。
4. **状态 file-first。** 可 durable 化的长期状态、正式结论、evidence 和 authority facts 由既有 repository owner 承载；prompt 不重复搬运已经可靠落盘的背景。
5. **默认最小治理。** 不为流程完整性自动增加 Work、Review、Fresh Session、文档、gate 或检查。只有真实 failure mode、独立性、authority、risk、execution surface 或 evidence need 要求时才升级，并由适用 owner / 人工授权决定。

## 2. CTRL + REVIEW 的单步控制循环

每轮按以下方式运行：

```text
CTRL 释放唯一 IMPL Task
→ IMPL 在授权范围内执行
→ IMPL RETURN 并停止
→ CTRL 独立 Review 本轮结果
→ continue / targeted remediation / pivot / stop / human decision
→ 若继续，再释放下一唯一 Task
```

CTRL + REVIEW SHOULD：

1. 每轮只释放一个 IMPL Task，避免把多个可独立判断的决策压成不可审查批次。
2. **Review 不只复述 IMPL RETURN。** 必须对照本轮 completion / exit criteria、真实 diff、验证与 evidence，自行判断是否完成、是否存在偏离，以及下一控制动作是什么。
3. 默认复用已有 IMPL 会话；上下文可靠时优先 `STAY + CONTINUE`，repository facts 变化但经验仍有效时使用 `STAY + REFRESH`。只有独立性、authority 变化、continuity loss / context contamination、跨 execution surface 或其他真实理由存在时，才要求 `CREATE + BOUNDED / INDEPENDENT`。Fresh Session、Cold Start、Full Historical Reload 不是同义词。
4. 若下一步涉及显著方向、scope、authority、production / release 边界变化，或存在真正 human-owned trade-off，先请求人工决定，不机械释放下一 Task。
5. 若无需人工决定，下一轮只给出一个唯一 Task，并保持 Return Target 清楚。

Session / Context 语义由 `standards/session-routing.md` 主责；本参考只组合其已允许的路由。

## 3. IMPL 运行规则

IMPL MUST：

1. 只执行当前 Task 与明确授权范围；命中合同级偏离、未授权依赖、新风险或停止条件时 RETURN。
2. Required reads 只采用 Minimum Sufficient Context：只强制“不读就不能安全或正确完成当前 Task”的最小文件集；historical evidence、retrospective、archive、old Review 默认 pointer-first / on-demand，不机械 Full Historical Reload。
3. 本轮完成后立即 RETURN；不得自行设计或执行下一 Task。
4. RETURN 只提供 CTRL 真正需要判卷的结果、验证、证据、阻塞、pointer 与必要 open issue，不用聊天重复 repository 已拥有的完整背景。

Planning / CURRENT / Task Capsule 的 owner 边界由 `standards/planning-and-handoff.md` 主责。

## 4. Git 与执行授权

轻量运行不等于无 Git 保护。

在当前 Work branch 与当前 Task scope 内，CTRL MAY 在 Task envelope 中一并授予精确 stage / commit / non-force push；但实际 mutation 只有在当前有效 action-specific approval 或 Scoped Standing Git Authorization **确实覆盖** repository、branch、文件范围、动作与前提时才可执行。

本参考本身不得授予或推定以下权限：

- merge / default-branch integration；
- force push；
- amend / rebase / shared-history rewrite；
- reset / clean / discard；
- tag / Release / publication；
- authorization scope 外的 repository / branch / file mutation。

具体授权和 mutation mechanics 由 `standards/git-safety.md` 主责。

## 5. 独立 REVIEW

独立 REVIEW **不是轻量探索默认步骤**。

只有存在明确的独立判卷、污染隔离、evidence value 或 acceptance contract 要求时才单独建立。Independent / Formal REVIEW：

- 只承担其已授权审查范围；
- 不因为 “Review” 标签自动要求 Fresh Session，session/context route 仍需单独判断；
- 不承担 remediation implementation，除非另有独立、明确授权。

## 6. Human 操作层

### 6.1 Task 与 prompt

1. 每个 IMPL Task 使用**唯一、连续的 Task ID**，用于关联 dispatch、执行结果和 CTRL Review；Task ID 不因此成为新的 lifecycle 或 assignment owner。
2. prompt 只传当前 Task、Return Target、必要 authority / scope / read pointers 与执行限制。已经 durable 的背景不重复整段粘贴。
3. 人的前台视角优先保持简洁：当前 Task ID、结果、进度、是否需要决策、下一步。

### 6.2 CTRL + REVIEW 对人输出

每轮 CTRL Review 至少让人能快速确认：

1. Review verdict；
2. 本轮实际解决了什么；
3. 当前大致进度 / 所处位置；
4. 是否需要人工决策，以及需要决定什么；
5. 若无需人工决策，下一唯一 Task 是什么。

这里的“进度”是 human-facing projection，不得复制或取代 lifecycle / Planning / Review canonical owner。

### 6.3 执行环境

1. 默认按 remote execution 理解，不因轻量探索自动要求本机环境。
2. 只有确需本机能力时才显式标记 `LOCAL / COMPUTER-SIDE`。
3. 本地产出在进入正式 authority / portable checkpoint 前，必须按项目 authority contract 与 Git safety 回到可追溯、可核验的 durable state；不得把仅本地结果宣称为已远端完成。

## 7. Progressive Formalization / De-escalation

只有真实 failure mode 出现时才增加治理承载，例如：

- material contract / scope change；
- protected action；
- continuity breakdown；
- distinct review failure mode；
- substantial executable seam；
- production / release / security boundary；
- evidence-required independence；
- human-owned criterion。

升级控制 MUST 与 failure mode 成比例，不得因为“看起来正式”而自动建立新 lifecycle、ledger 或 gate。

当触发升级的 failure mode 消失后，MAY 移除临时机制并回到更轻的运行方式。De-escalation 不得削弱 Authority、Evidence Honesty、explicit authorization、Production Trace、applicable required Review 或真实存在的 human acceptance requirement。

## 8. Non-owner / canonical boundary

本参考不：

- 创建 `LIGHTWEIGHT_MODE`、Profile 或新 lifecycle；
- 建立第二套 Planning、Task state、Review 类型或 gate；
- 成为 authorization、Git facts、production / release state 的 owner；
- 以“少读、少写”为由跳过 correctness-critical evidence；
- 覆盖 canonical standard。

任何时候：

- lifecycle 仍由 `agents/WORK_INDEX.md` 主责；
- Review verdict / Open Findings 仍由 Review ledger 主责；
- execution next action 仍由现有 Planning owner 主责；
- authorization 仍来自用户 / Primary Contract / applicable authorization；
- Git facts 仍来自真实 repository；
- CURRENT / Task Capsule 仍受 `standards/planning-and-handoff.md` 约束。

优化目标不是“尽可能少做流程”，而是：**只在真实 failure mode 出现时支付相称的恢复、同步和治理成本，同时保持单步可判、可停、可恢复。**
