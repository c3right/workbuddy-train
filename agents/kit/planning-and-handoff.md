# Planning and Handoff

**版本：v0.4-draft**
**依赖：`core-protocol.md`、`session-routing.md`**

## 1. 目的与范围

本标准规定当前前台 Work Item 的热状态、Delta State Sync、Minimum Sufficient Context、普通责任/上下文交接、状态所有权和 Planning 归档。

本标准不定义 Git 写操作批准或跨电脑资产传输；Transfer Snapshot 由 `portability-and-distribution.md` 负责。

## 2. One Foreground Work Item

1. 根目录 `task_plan.md`、`findings.md`、`progress.md` MUST 只服务一个前台活动 Work Item。
2. 三件套 MUST 记录相同的 Work ID 和唯一 Primary Task Contract 路径。
3. 切换前台 Work Item 前，当前 Work MUST 完成暂停、终止或归档程序。
4. 执行面 MAY 管理多个内部子任务，但顶层三件套只保存当前焦点和跨轨道摘要。

## 3. 文件职责

### `task_plan.md`

MUST 保存目标、当前执行阶段、步骤、下一准确动作、依赖和退出条件。它不得改变 Primary Task Contract，也不得成为 Work 生命周期状态的独立权威。

### `findings.md`

MUST 保存仍会影响当前工作的非 Review 发现、证据、影响、建议处置和待决定事项。Formal Review Finding 以 Review ledger 为准。

### `progress.md`

MUST 保存历史 checkpoint：已经完成的动作、证据、工作区状态、剩余工作和当时的下一动作。它不得成为生命周期状态或 Review Decision 的独立权威，也不得成为逐条命令日志。

三件套 SHOULD 使用普通 Markdown，默认进入 Git 跟踪。

## 4. Canonical Current-state Ownership

当前状态必须按职责单点主责：

1. `agents/WORK_INDEX.md` MUST 是 Work 生命周期状态的唯一当前权威。
2. `agents/reviews/<work-id>.md` MUST 是 Review Decision、Open Findings 和 Recheck 结论的唯一权威。
3. `task_plan.md` 只记录执行阶段、下一动作和退出条件；如需显示生命周期状态，MUST 使用指针式表述，例如“Current lifecycle status：见 `agents/WORK_INDEX.md`”，不得复制另一套状态值。
4. `findings.md` 不得复制 Formal Review Open Findings。
5. `progress.md` 只记录某时点已经发生的 checkpoint；MUST NOT 用现在时宣告当前生命周期状态或当前 Open Findings。
6. `agents/handoffs/CURRENT.md` 只提供恢复封套、权威指针和下一准确动作；只在真实责任/上下文交接需要 durable recovery envelope 时更新，MUST NOT 成为 lifecycle、Finding、Review verdict、Git facts 或 authorization 的独立 owner。
7. 同一事实出现在非 owner 面时，只保存稳定 pointer、事件时间或必要短摘要，并明确 canonical owner。

当前 owner 速查：

```text
Lifecycle status owner → agents/WORK_INDEX.md
Review decision owner → agents/reviews/<work-id>.md
Execution next action → task_plan.md
Non-Review finding → findings.md
Historical checkpoint → progress.md
Durable handoff envelope → agents/handoffs/CURRENT.md
```

## 5. Delta State Sync

State Sync 的目标是保持事实一致，不是机械 touch 文件。

每次发生责任/上下文切换、重要 checkpoint、关键验证、范围或授权变化、准备 Review/Closeout、长时间暂停等事件时，MUST 先做 **owner evaluation**：

1. 识别本轮实际发生变化的事实；
2. 每个 delta 只写入 canonical owner；
3. 核对其他 owner/consumer 不与该事实矛盾；
4. 只有下一动作实际依赖 Git / authorization / execution-surface 前提时，才核验对应事实。

Mandatory event 触发的是 owner evaluation，不是 mandatory file write。

因此：

```text
clean RETURN / handoff
+
no owned-fact delta
→ zero unnecessary writes
```

若没有 owned-fact delta，且现有 canonical state 已足以恢复，MAY `RETURN` 或完成 handoff 而不修改 Planning 三件套或 CURRENT。

**Delta State Sync ≠ 不读、不验证、相信旧状态。** 下一动作需要的 authority、assignment、authorization、风险和 repository facts 仍必须按 Minimum Sufficient Context 核验。

## 6. Minimum Sufficient Context

Mandatory read-set 定义为：

> 如果不读，就不能安全或正确完成当前任务的最小集合。

Agent MUST 根据以下因素决定 read-set：

- current authority；
- 当前 assignment / Return Target；
- affected canonical owner；
- applicable authorization；
- 与下一动作直接相关的风险与 failure mode。

historical evidence、retrospective、archive、old Review、已解决 discussion 默认采用：

```text
pointer-first / on-demand
```

只有当前任务的 correctness、争议 adjudication 或 evidence contract 需要时才展开。

Cold Start 也不得被解释为 Full Historical Reload。新会话只需建立当前任务所需的最小可靠上下文。

## 7. Session Handoff 与 CURRENT

1. 只有真实责任或上下文交接需要 durable recovery envelope 时，才 SHOULD 更新 `agents/handoffs/CURRENT.md`。
2. `STAY + CONTINUE` 的普通连续推进通常不需要 CURRENT diff。
3. `STAY + REFRESH` 只有在 handoff envelope 自身事实发生变化时才更新 CURRENT。
4. `CREATE` 不自动要求 CURRENT；如果新会话可从现有 canonical owners 安全恢复且没有新的 handoff delta，允许 zero-write。
5. 真正需要 CURRENT 时 SHOULD 包含：
   - Work ID、From Role、To Role、Session Action、Context Strategy、Return Target、Prepared At；
   - canonical authority pointers；
   - Purpose；
   - Delta Since Previous Handoff；
   - Authorized Scope；
   - Required Output；
   - Do Not Do；
   - Minimum Read Set。
6. Handoff 不得重新定义 Contract、lifecycle、Review verdict、Git facts 或 authorization。
7. 跨电脑、交付给其他执行面或长期冻结时，仍按 `portability-and-distribution.md` 判断是否需要 Transfer Snapshot。

## 8. Task Capsule

Task Capsule 只允许两种形态：

1. CURRENT 内的 bounded-assignment shape；或
2. 从 canonical owners 生成的 ephemeral dispatch view。

Canonical inputs 至少 MAY 包括：

- `agents/handoffs/CURRENT.md`；
- `task_plan.md`；
- Primary Task Contract；
- applicable authorization。

Task Capsule MUST NOT 拥有或独立维护：

- lifecycle；
- next action；
- Finding / Review verdict；
- Git facts；
- authorization。

不得新增 Task Capsule state file、Capsule ledger、Capsule sync gate 或第三套 mutable assignment state。

若 Capsule 与 canonical owner 不一致：

> canonical owner wins。

## 9. Human Acceptance 与 Progressive Formalization

Human Acceptance 只在验收条件中存在真正由人承担的 human-owned criterion 时启用，例如主观质量判断、业务取舍、风险接受或最终用户决策。

以下标签单独均不自动创建 Human Gate：

- Formal Work；
- `STRICT`；
- Formal Review；
- normative change。

Progressive Formalization / De-escalation 是 failure-mode-driven guidance，不是新的普适 lifecycle 或 state machine：

- failure mode、可恢复性、执行面或 evidence need 增加时 MAY 增加相称控制；
- failure mode 消失后 MAY 撤掉临时控制，回到更轻的运行方式；
- De-escalation 不得削弱 Authority、Evidence Honesty、authorization、Production Trace、required Review 或已真实存在的 human-owned criterion。

## 10. Post-merge Reconciliation

正常路径 SHOULD 在 merge 前完成 Review、适用时的用户验收、Closeout 和可预见状态同步，使 merge 后无需纯状态提交。

若 PR 已完成 merge：

1. 先判断默认分支是否已经能从 merge commit、Work Index 和 Review ledger 恢复事实；可以恢复时使用 `0` 次 reconciliation。
2. 确需更新仓库当前状态时，最多允许 `1` 次纯状态 reconciliation，并一次性更新生命周期 owner、Review pointer、归档／Closeout pointer 和必要导航。
3. Human Acceptance 只在存在真正 human-owned criterion 时启用；当该 criterion 存在且用户验收已知、有明确正面证据时，该次 reconciliation SHOULD 直接写入最终状态。聊天沉默、尚未决定、仅完成实施／Review／merge，均不构成用户验收。
4. 用户验收尚未知时，生命周期 owner MUST 使用 `INTEGRATED / ACCEPTANCE_PENDING`；Review 有未解决 Finding 时 MUST 使用 `INTEGRATED / REMEDIATION_REQUIRED`。其他载体只引用 owner。
5. **Implementation complete / merge complete 不等于 Work accepted。** 在用户验收仍 pending 时，生命周期 owner MUST NOT 使用 `COMPLETE`、`COMPLETED`、`DONE`、`CLOSED`、`ACCEPTED`、`WORK_COMPLETE`、`Work complete` 或其他表示 Work 已最终完成／验收的同义终态。
6. 只有当 Primary Task Contract 要求的用户验收已经真实发生，并且 Review／测试／Git／生产影响等适用退出条件已满足时，才 MAY 进入 `ACCEPTED` 或项目定义的等价最终状态。
7. 已经使用一次 post-merge reconciliation 后，MUST NOT 再为用户摘要、Goal complete、merge SHA、CI run 或把“待完成”改成“已完成”创建第二次纯状态提交。
8. 后续状态变化如确需写入 Git，MUST 与实质 remediation、Closeout／归档或下一项已授权的实质变更合并；不得单独追逐状态文字。
9. 第二次纯状态 reconciliation MUST 形成治理负担 Finding，而不是被视为正常收尾。

## 11. Planning Archive

1. Work Item 进入 `ACCEPTED`、长期 `SUSPENDED`、`ABANDONED`、`SUPERSEDED`，或切换到另一个需要完整前台状态的 Work Item 时，三件套 MUST 原样归档到：

   ```text
   agents/planning-archive/<work-id>/
   ```

2. 归档顺序 MUST 是：最终 checkpoint → Closeout／Suspension Closeout → 归档三件套 → 更新 Work Index → 创建新的空白三件套 → 填入新 Work ID 和唯一 Primary Task Contract → 输出并检查 Git diff。
3. 已由 Git 跟踪的文件 SHOULD 保留可识别的 rename diff。
4. Planning 归档不得合并成单一摘要文件。
5. 归档后的 Git 写动作仍须遵守 `git-safety.md`。
6. 若归档发生在 merge 后，必须计入第 10 节的一次 reconciliation 预算。

## 12. SESSION_INDEX

只有存在多个长期会话并频繁 `RETURN`，且该索引真实降低恢复成本时 MAY 创建 `agents/SESSION_INDEX.md`。它只保存会话、角色、Work ID、canonical owner pointers、最新输入和 Return Target，不得成为 lifecycle/assignment owner，也不强制记录 Host 或模型。

## 13. Cross-References

- Work Item 和核心记录：`core-protocol.md`
- Session / Context 2×2：`session-routing.md`
- Git 状态和提交门禁：`git-safety.md`
- Transfer Snapshot：`portability-and-distribution.md`
- 轻量探索：`docs/reference/lightweight-exploration-reference.md`
- Planned CTRL succession：`docs/reference/control-continuity-succession-reference.md`

## 14. Source Map

- KC-018：S-12 single-owner / zero-or-one post-merge reconciliation floor。
- KC-021 Frozen Full Design：Work C。
- KC-024 Primary Task Contract：RO-02、RO-03、RO-04、RO-08。
