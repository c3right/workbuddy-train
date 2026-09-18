# CTRL 连续性与接续 Reference Pattern

**定位：Reference Pattern / non-owner**  
**适用：Work 级 CTRL 的 planned succession 与 unexpected-loss reconstitution**

本参考只负责判断连续性的 operational route，不拥有 correctness-critical current state，也不创建第二套正式状态。

> **Core Principle：Repository 保证事实连续性，CTRL Continuity Delta 保证判断连续性；主动交接由旧 CTRL 压缩关键决策链，被动重建由新 CTRL 基于 repository、人工输入和可恢复会话证据重建 Delta，再经人工校准后继续控制。**

## 1. 基本原则

1. **CTRL 是 Work 级长期控制会话。** CTRL 持续掌握 Work 的决策链、路由逻辑、当前 framing 与下一控制判断；IMPL / REVIEW 会话默认可替换，不要求通过保留同一执行会话来维持 Work correctness。
2. **Canonical Repository State 是唯一正式事实与 authority 基线。** 生命周期、Primary Contract、Planning、Review verdict / Open Findings、Git facts、authorization、production / release state 继续由既有 canonical owner 主责。
3. **`CTRL Continuity Delta` 只保存 repository 之外、但会显著影响 successor CTRL 判断质量的控制上下文。** 它不复制当前正式状态，不形成第二套 lifecycle、assignment state、Review state 或 authorization。
4. Repository 提供 correctness floor；Delta 提高 judgement continuity / recovery fidelity。若两者冲突：

> canonical owner wins。

## 2. CTRL Continuity Delta 的内容边界

### 2.1 MAY 保存

Delta SHOULD 只保存“丢失后不会破坏正式事实，但会让 successor 明显重复推理、误读路线或错过判断边界”的增量，例如：

- `Current Control Framing`：当前如何理解问题、为什么沿当前路线控制；
- 关键 `Decision Lineage`：重要 pivot、rollback、战略性否定或路线选择背后的最小因果链；
- `Rejected / Deferred Paths`；
- reopen conditions；
- `Next Decision Boundary`：接班后第一件真正需要判断的事；
- 必要 human judgement context；
- context hazards / contamination risks；
- 只为定位使用的 canonical pointers。

### 2.2 MUST NOT 拥有

Delta 不得拥有或取代：

- Work lifecycle；
- Primary Task Contract；
- current assignment / execution next action；
- Review verdict / Open Findings；
- non-Review canonical finding；
- Git facts / HEAD / committed artifact state；
- authorization；
- production / release state；
- correctness-critical recovery fact。

核心判据：

> **如果某条信息丢失会影响 correctness、authority、authorization 或正式状态，它就不能只存在于 CTRL Continuity Delta 中。**

不得建立 Delta ledger、rolling state、固定刷新周期、completion / return registry 或 recovery state owner。

## 3. 主动 CTRL 交接 — Planned Succession

旧 CTRL 仍可靠时，优先采用 planned succession。

### 3.1 何时检查是否需要换 CTRL

出现以下任一信号时 SHOULD 检查是否需要主动接续，而不是机械维持原会话：

1. 会话接近容量，continuity 已开始不可靠；
2. CTRL 给新 Task 的 prompt 越来越多用于解释历史、失效结论或旧上下文；
3. Work 经历明显 pivot、rollback、战略性否定或目标重定义，旧上下文开始干扰当前判断；
4. 到达自然控制断点，新阶段更适合从更干净的 bounded context 继续。

这些信号只触发“是否接续”的判断，不自动创建新 lifecycle、Fresh Review 或额外 gate。

### 3.2 一次性交接

决定接续时，由旧 CTRL 生成一次 `CTRL Continuity Delta`。最小内容为：

1. `Current Control Framing`
2. 关键 `Decision Lineage`
3. `Rejected / Deferred Paths`
4. `Next Decision Boundary`

可按需要附加 reopen conditions、human judgement context、context hazards 与 canonical pointers。

Delta 是**一次性交接材料**，不持续滚动维护。若 durable handoff envelope 确有必要，可按 `standards/planning-and-handoff.md` 既有 CURRENT / handoff 规则嵌入辅助段落或作为一次性 handoff 附件；不得因此创建新的 Delta owner。

### 3.3 Successor 起步

successor CTRL 先恢复 canonical owners，再读取 Delta。Delta 的 `Next Decision Boundary` 只告诉 successor “第一件应判断什么、哪些事实先刷新、哪些历史按需展开”，不是新的 next-action owner。

## 4. 被动 CTRL 重建 — CTRL Reconstitution

旧 CTRL 已不可用且没有可靠 Delta 时，进入 `CTRL Reconstitution`。目标不是复刻旧 CTRL 的完整 reasoning transcript，而是恢复一个 correctness 足够、决策链基本对齐、上下文更干净、能够继续高质量控制 Work 的 successor CTRL。

默认先做 **bounded reconstitution**，不直接 Full Historical Reload。

### 4.1 信息来源

Reconstitution MAY 使用三类信息：

1. **Canonical Repository State**：correctness / authority 的基线；
2. **human recall / confirmation**：人工对关键决策链、取舍、rejected path、判断背景的回忆与确认；
3. **recovered conversation evidence**：可从旧 CTRL 会话恢复出的关键片段。

后两类只能提高 reasoning continuity；不得覆盖 repository authority，也不得成为新的 canonical owner。

### 4.2 Forced RETURN-boundary reconciliation

forced loss 时，不得只读 `task_plan.md` / CURRENT 后机械 replay 其中可能 stale 的 dispatch。successor SHOULD 按以下顺序恢复：

```text
recover canonical owners
→ refresh latest remote HEAD / relevant diff / durable evidence
→ reconcile newest evidence with in-flight / dispatch-facing assignment
→ if child result is already durable, do not replay completed dispatch
→ inspect assignment exit evidence
→ decide Review / targeted remediation / accept / stop / next control decision
```

Minimum Sufficient recovery route 通常是：

```text
AGENTS / authority entry
→ WORK_INDEX
→ Primary Task Contract
→ task_plan / CURRENT
→ Review owner / findings / progress（按命中读取）
→ latest remote HEAD / relevant durable result
→ return-boundary reconciliation
→ expose unresolved uncertainty
→ resume CTRL decision
```

这只是 recovery route，不创建 completion ledger、return registry、second next-action owner 或新的 State Sync obligation。若 formal Review 已按 canonical owner durable 化，则以 Review ledger 为准；若正式状态本应 durable 却只存在于丢失聊天中，那是具体 Work instance 的 canonical-state violation，不能用 Delta 补成 authority。

### 4.3 Reconstructed CTRL Continuity Delta

完成 bounded evidence recovery 后，新 CTRL 主动生成 `Reconstructed CTRL Continuity Delta`，并对其中判断逐项区分：

- `CONFIRMED`：由 repository / durable evidence 直接支持；
- `RECONSTRUCTED`：由现有 evidence、human recall 或 recovered conversation evidence 合理重建；
- `UNCERTAIN`：可能影响当前路线或下一控制判断，现有证据不足。

Reconstructed Delta 的内容边界与第 2 节相同：只保存 continuity context，不复制或重定义 canonical current state。

### 4.4 Human calibration

对真正影响当前路线、但仍是 `UNCERTAIN` 的少量问题，新 CTRL SHOULD 主动请求人工校准。人工可：

- 确认关键决策链；
- 修正 successor 的重建；
- 补充旧 CTRL 中未 durable、但仅影响 judgement continuity 的上下文；
- 提供旧会话关键片段。

校准链路为：

```text
repository facts
+ human recall
+ recovered conversation evidence
→ Reconstructed CTRL Continuity Delta
→ CONFIRMED / RECONSTRUCTED / UNCERTAIN
→ human calibration
→ calibrated successor CTRL
```

人工校准后的 Delta 成为 successor 后续判断的 continuity 起点，但仍不成为 repository authority。若人工输入与 canonical facts 冲突，先按 owner 规则解决正式事实；不得以记忆覆盖 canonical owner。

## 5. 与 CURRENT / Planning / Task Capsule 的关系

- CURRENT 只在真实责任/上下文交接需要 durable recovery envelope 时使用；
- `CTRL Continuity Delta` MAY 作为 CURRENT 中的辅助段落或一次性 handoff 附件，但只按现有 handoff owner 规则承载；
- Task Capsule MAY 从 canonical owners 生成 ephemeral dispatch view；
- Delta、CURRENT、Task Capsule 都不得形成第三套 mutable assignment state；
- Delta 不主责 `execution next action`，`Next Decision Boundary` 也不是 Planning 的替代品；
- 是否发生 Planning / CURRENT 写入，仍由 `standards/planning-and-handoff.md` 的 owner evaluation / Delta State Sync 决定，不因 succession / reconstitution 名称机械 touch 文件。

## 6. Session / Review / Git 边界

1. CTRL continuity 与 Session routing 分离。planned succession / reconstitution 可以使用 `CREATE + BOUNDED`，但实际 session/context strategy 仍由 `standards/session-routing.md` 根据 continuity、independence、contamination 与 execution surface 判断。
2. CTRL continuity 不创建新的 Review 类型，不改变 Formal Review / Independent Review trigger。
3. Delta 不携带或扩大 Git authorization。commit / push / merge / protected actions 仍由当前有效 authorization 与 `standards/git-safety.md` 主责。
4. production / release / publication authority 不从 Delta、human recall 或 recovered conversation evidence 获得。

## 7. Recovery correctness floor

forced reconstitution 的成功标准不是“恢复旧 CTRL 的全部想法”，而是：

- current Work / scope / lifecycle 可从 canonical owner 恢复；
- authority / authorization 可核验；
- Review / Finding / Git / durable result 可按 owner 恢复；
- stale dispatch 可通过 latest-evidence reconciliation 识别；
- 影响当前路线的 continuity context 能以 Reconstructed Delta + human calibration 收敛；
- unresolved uncertainty 被显式暴露，而不是猜测后继续。

因此：

```text
Repository → fact continuity / correctness floor
CTRL Continuity Delta → judgement continuity / recovery fidelity
```

两者职责不同；缺一段 reasoning 不等于 canonical gap，只有 correctness-critical fact 缺少 durable owner 才需要升级为 canonical-state 问题。
