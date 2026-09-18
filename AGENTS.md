# WorkBuddy Train — Kit 控制面入口

## 安装合同

- Kit profile：`skill-heavy`
- Install record：`.workflow-kit.yml`
- Project Domain Entry：`docs/project/domain-entry.md`
- Registered Overrides：`agents/overrides/registry.json`
- Local-only contract：`.workflow-kit.yml#local_state`

`agents/kit/*.md` 是固定 source commit 的 Kit Base 快照，项目不得直接修改。

## 自然语言 Reference 调用入口

以下三个 canonical intent 是薄型 natural-language routing alias，不是 command parser。用户使用语义等价的自然语言表达时也应路由到同一 intent，不要求逐字匹配 canonical phrase；入口只负责读取与执行对应 Reference，不复制其正文。

### 按轻量探索治理规则

读取 `agents/kit/lightweight-exploration-reference.md`。第一轮响应复述其中的 Core Principle，明确确认“当前 Work 后续按该 Reference 治理”，然后继续当前 Work；不创建 LIGHTWEIGHT_MODE，不要求内部开关，也不自动建立 Human Gate。

### 做CTRL交接

读取 `agents/kit/control-continuity-succession-reference.md` 并把该 intent 解释为 planned succession。第一轮响应复述其中的 Core Principle，明确当前进入 planned succession，refresh canonical repository facts，并生成最小 CTRL Continuity Delta 草案，至少包含：

- Current Control Framing
- Decision Lineage
- Rejected / Deferred Paths
- Next Decision Boundary

先让人工确认 / 修正 Delta 草案。只有人工确认后，才按既有 Planning / Handoff owner 规则决定是否 durable 落盘，并输出 successor CTRL 短提示词；不创建 Delta ledger。canonical phrase 本身不自动授权 Git 写入，commit / push 仍受当前 authority 与 Git safety 约束。

### 重建CTRL

读取 `agents/kit/control-continuity-succession-reference.md` 并把该 intent 解释为 old CTRL unavailable / forced CTRL reconstitution。第一轮响应复述其中的 Core Principle，明确当前进入 forced CTRL reconstitution，不先要求用户从零解释整个 Work，而是先执行 repository-first bounded recovery：

```text
canonical owners
→ latest durable evidence
→ stale-dispatch reconciliation
→ current control state
```

随后生成 Reconstructed CTRL Continuity Delta，明确区分 CONFIRMED / RECONSTRUCTED / UNCERTAIN，只把真正影响后续路线的少量 UNCERTAIN 项提交人工回答 / 校准；校准后形成 calibrated successor CTRL 并继续控制。人工记忆或旧 conversation evidence 可以提高 judgement continuity，但不得覆盖 canonical repository authority。

三个 intent 都不创建 Mode、不创建新的 lifecycle、不创建 command / alias / invocation registry、不创建 mutable preference 或 Delta ledger，也不创建新的 authority owner；它们不自动授予 Git、Formal Review、production / release、merge 或 main integration 权限。

## Minimum Sufficient Context（最小充分恢复）

Mandatory read-set 不是“重要文件清单”，而是如果不读就不能安全或正确完成当前任务的最小集合。

通常按以下顺序建立当前 authority：

1. 本文件与 `.workflow-kit.yml`；
2. `agents/overrides/registry.json`；
3. `agents/WORK_INDEX.md`；
4. 有活动 Work 时读取 Primary Task Contract；
5. 只读取当前 assignment 所需的 Planning / CURRENT / Review owner；
6. `agents/kit/core-protocol.md#12-action-routing-index`；
7. 只读取当前动作适用的 standard；
8. 只有需要领域信息时读取 `docs/project/domain-entry.md` 及其 pointer；
9. 只有需要本机事实时检查 local-only state。

historical evidence、retrospective、archive、old Review 默认 pointer-first / on-demand。Cold Start 不等于 Full Historical Reload。

## 控制面

- 建立 Work ID 前先按 Core 执行 Formal Work Entry Check；边界清晰的短期直接工作可不建立完整 Work，规范性资产直接维护还必须是非语义 LIGHT；两者仍需授权、产出／精确 diff、验证和必要证据。
- 每个正式 Work 只有一个 Work ID 和 Primary Task Contract，并登记在 `agents/WORK_INDEX.md`。
- CTRL 定义和授权；IMPL 只在批准范围内实施；REVIEW 执行 Formal Review。Formal Review 不自动要求新会话或 independent reviewer；只有独立性本身属于 acceptance evidence 时才启用 Protected Independent Review。
- Session action 与 Context strategy 分开判断；常用组合为 `STAY + CONTINUE`、`STAY + REFRESH`、`CREATE + BOUNDED`、`CREATE + INDEPENDENT`。role change、Formal Review、复杂度或 stronger capability need 单独均不自动 `CREATE`。
- `CREATE` / `RETURN` 只触发 Delta State Sync owner evaluation，不机械 touch Planning 三件套或 CURRENT；没有 owned-fact delta 且现有 canonical state 足够时允许 zero-write。
- `agents/handoffs/CURRENT.md` 只在真实责任/上下文交接需要 durable recovery envelope 时使用。Task Capsule 只能是 CURRENT 的 bounded shape 或从 canonical owners 生成的 ephemeral view，不是新 owner。
- 规范性资产变更先按 `agents/kit/normative-asset-change-control.md` 分级；正式 Skill create/substantial change/Review 先加载 `agents/kit/skill-design-principles.md`，再按实际 failure mode 选择验证。
- Profile 只声明长期预设；专业 Module 默认休眠，由当前意图／合同按需激活，用户无需管理内部开关。
- Human Acceptance 只在真实 human-owned criterion 存在时启用；Formal Work、`STRICT`、Review 或 normative change 标签本身不自动创建 Human Gate。
- README／Navigation Impact 和新鲜度按 `docs/operations/readme-navigation.md` 检查。

本节只提供入口摘要；完整义务由适用 standard 主责。

## 四层边界

- **Kit Base**：`agents/kit/*.md` 和其他 Kit Managed 资产；固定来源，不直接修改。
- **Project Overlay**：`docs/project/domain-entry.md` 及其项目权威来源；表达领域规则，不复制 Base 正文。
- **Registered Overrides**：`agents/overrides/registry.json`；仅登记＋引用，有效 scope 内优先。
- **Local-only State**：`.workflow-kit.local.yml` 或 `local/` 中的机器事实；不得提交，不具有规范覆盖权。

Override 不得绕过用户批准、Git 门禁、acceptance contract 明确要求的 Protected Independent Review、Production Trace、Kit Managed 边界或敏感信息边界。引用失效、冲突或越权时停止受影响动作并返回 CTRL／用户。

## 停止与返回

以下情况不得自行继续：

- 是否需要正式 Work 无法判断；或需要正式 Work 时 Work、合同、权限或 Return Target 不清；
- Base、Overlay 或 Override 实质冲突；
- Override 引用失效、重复、循环、scope 重叠或命中 protected control；
- local-only 状态被纳入提交、未 ignore 或含敏感信息；
- 需要未获批准的文件修改、Git 写动作、外部写入或正式生产；
- Manifest、source commit、所有权或安装完整性无法可靠确认。

## Git 与数据安全

commit、push、merge、tag、历史改写、remote、分支删除和公开发布必须取得适用的用户明确批准或有效 Scoped Standing Git Authorization。秘密、真实敏感数据和机器专属状态不得进入 Git。
