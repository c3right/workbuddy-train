# 规范性资产变更控制（Normative Asset Change Control）

**版本：v0.4-draft**
**依赖：`core-protocol.md`、`git-safety.md`**

## 1. 目的与范围

本标准规定规范性资产变更的统一入口、风险分级、工作承载、审查架构、最低证据和简短演进轨迹，使控制强度与语义影响及失效后果相称。

本标准覆盖 Control Plane Entry、Project Domain Entry、Registered Overrides、local-only committed contract、standards、Profile、模板、Manifest、正式 Skill 和具有约束效力的配置。它不提供 Bootstrap、自动迁移、自动修复或固定 Review 工具步骤。

## 2. 规范性资产与触发条件

规范性资产包括：

- 根或目录级 `AGENTS.md`／Kit Control Plane Entry；
- Project Domain Entry 中具有约束效力的领域规则；
- Registered Override registry 及 active Override；
- `.workflow-kit.yml` 中的入口、所有权和 local-only contract；
- Kit standards、安装快照、治理 Profile 和 Layer Manifest；
- 正式 Skill 及其 Reference、Script、Asset 和 input/output contract；
- 具有约束效力的模板、ADR、合同和运行程序。

新增、修改、优化、重构、接口调整、回归修复或正式审查上述资产前，CTRL MUST 先完成 Core 定义的 Formal Work Entry Check，再完成风险初判和承载选择。

讨论、建议、审阅、要求落盘方案或认可判断 MUST NOT 视为实施授权。所有等级都 MUST 有用户对明确修改或明确范围的实施授权。

## 3. 正式 Work 入口与分级顺序

1. 窄范围直接维护只有在同时满足 Core 直接维护边界和本标准全部 LIGHT 条件时，MAY 不建立正式 Work。
2. 任一条件无法证明、出现语义 Finding、需要跨会话接续或需要正式放行时，MUST 建立正式 Work。
3. 直接维护不是第四个风险等级，不得降低授权、Git、专业方法或验证要求。
4. 对需要正式 Work 的规范性资产变更，风险等级只允许：

```text
LIGHT
STANDARD
STRICT
```

5. CTRL MUST：
   1. 先检查任一 STRICT 自动升级条件；
   2. 未命中时逐项证明全部 LIGHT 条件；
   3. 不能完整证明 LIGHT、证据不足或存在合理疑问时定为 STANDARD。

分类依据语义影响和失效后果，不得只依据文件名、目录、行数或实现便利。混合变更使用最高等级；不得拆分规避升级。

**风险等级（Risk level）决定证据深度（evidence depth）和受保护控制的审查强度；它不直接决定是否激活 Formal Review，也不直接决定会话是否需要刷新、上下文是否需要独立，或是否必须由独立 reviewer 执行。**

## 4. LIGHT

降为 LIGHT 必须同时满足：

1. 小型、局部、单一意图，diff 易人工检查；
2. 不新增、删除、放宽或改变义务、禁止、权限、批准点、状态、优先级或默认行为；
3. 无 Script、自动化副作用、敏感数据和外部写操作；
4. 不改变下游接口、规则主归属、兼容性、入口职责或已发布语义；
5. 失败易发现且可通过单一回退恢复；
6. 不与用户决定、Kit Base、有效 Override 或其他正式规则冲突。

典型 LIGHT 包括错别字、失效链接、与主规则等价的澄清和非强制示例。

## 5. STANDARD

STANDARD 是默认等级。未命中 STRICT 但满足任一项时使用：

- 新增或改变规范性行为、默认值、触发条件或执行步骤；
- 新增例外、路由、入口或资产间引用；
- 影响一个明确 consumer、Profile 或安装快照；
- 新增 proposed／suspended／retired Override 记录但不激活优先级；
- 需要常规兼容性、回归或正式审查（Formal Review）；
- LIGHT 条件不能全部证明。

STANDARD 要求与真实 failure mode 相称的证据深度。Formal Review 只有在实际 failure mode、acceptance evidence contract、consumer／compatibility／coherence 风险、Evidence Honesty 或 release decision 需要一个独立 Review function 时才激活；**STANDARD 本身不自动要求 Formal Review**，也不自动要求新上下文 / 独立上下文或 Protected Independent Review。

## 6. STRICT

命中任一项 MUST 自动升级 STRICT：

- 权限、安全边界、用户批准门禁、破坏性动作或外部写操作；
- 权威顺序、角色职责、状态机、Review acceptance contract 或关闭条件；
- Kit Base／Overlay／Override 优先级、protected controls 或 active Override；
- Control Plane Entry 与 Project Domain Entry 的职责或冷启动顺序；
- local-only、秘密、凭据、本机路径或误提交边界；
- 多项目或多个独立 consumer、公共接口、版本迁移或向后兼容；
- 敏感数据、正式数据口径、财务、合同、正式报告或生产追溯；
- 错误难发现、影响难界定、回退困难或旧成果可能失效；
- 修改本标准的风险判据、LIGHT 例外、升级条件或控制流程。

不得因工期、工具可用性或人工方便性降级。STRICT 要求更强的证据深度、失败恢复、兼容／迁移与 protected-control scrutiny；**STRICT 本身不自动要求 Formal Review**，也不会自动触发 Protected Independent Review，即 `Protected Independent Review not automatic`。

## 7. Work 承载方式

### 附属 LIGHT

与当前 Work 目标直接相关的 LIGHT MAY 附属：

- 不建立新 Work ID；
- 在父合同使用稳定条目号；
- 记录意图、文件、LIGHT 判据、授权、baseline、验证和结果；
- 由父 Work 的 Planning、Review、Closeout 和 Git checkpoint 覆盖。

范围扩大、LIGHT 条件失效或出现语义 Finding 时 MUST 返回 CTRL，升级为独立 Work。

### 无正式 Work 的直接维护

没有父 Work 且同时满足 Core 直接维护边界和全部 LIGHT 条件时，MAY 不建立正式 Work，但 MUST：

- 保存简短意图和用户授权；
- 只修改精确列明的文件；
- 检查完整 diff、语义不变、验证和敏感信息；
- 由工作区状态或 Git commit 形成可回退证据；
- 不创建 Planning、Review、Closeout 占位文件，也不得宣称正式 `ACCEPTED`。

一旦需要正式放行、长期接续、独立交付，或出现语义、权限、范围、接口、下游 Finding，MUST 返回 CTRL 建立正式 Work。

### 独立 LIGHT Work

没有合法父 Work，但因接续、独立交付、正式放行或其他控制需要进入正式治理时，LIGHT MUST：

- 分配唯一 Work ID 并登记 WORK_INDEX；
- 使用简短变更档案作为唯一 Primary Contract；
- 记录目标、非目标、文件、判据、授权、Git baseline、验证和验收；
- 形成 Closeout。

### STANDARD 与 STRICT

STANDARD／STRICT MUST 建立独立 Formal Work、完整 Primary Contract、使用 Planning、保留与风险相称的 validation / evidence，并形成 Closeout。是否激活 Formal Review，按第 10 节根据真实 failure mode / evidence contract 单独判断；risk class 本身不是 Formal Review trigger。STRICT 合同还 MUST 明确更深证据、失败后果与恢复、兼容／迁移、旧成果和生产影响，并加强 protected-control scrutiny。

Formal Work 的存在或 STANDARD／STRICT 标签不得单独被解释为“必须 Formal Review”；Formal Review 的存在也不得单独被解释为“必须新会话”或“必须 independent reviewer”。

## 8. Overlay 与 Override 变更要求

1. 新增 Project Overlay 规则前 MUST 证明其属于项目领域事实，而不是 Kit Base 已定义的通用治理正文。
2. Overlay 与 Base 冲突时不得通过措辞变化隐藏冲突；MUST 返回 CTRL 判断是否建立 Override。
3. 新增或修改 Override MUST 指向稳定 `base_rule` 和 `project_rule`，不得复制完整 standard。
4. 激活 Override MUST 使用 STRICT，完成 Authority、scope、依赖、protected controls、兼容、回退、Review 和用户验收。
5. 失效引用、重复 ID、循环依赖、active scope 重叠或 protected-control override MUST 阻断放行。
6. suspended／retired Override 不再覆盖 Base，但保留历史证据和原因。
7. Override 不得保存秘密、凭据、用户名目录或绝对本机路径。

## 9. Local-only 变更要求

1. `.workflow-kit.yml` 可登记 local-only 相对路径、是否 required、ignore 要求和允许根；实际机器值不得提交。
2. 将 local-only 文件加入 required committed list、取消 ignore、开始 tracked 或将秘密／绝对本机路径写入 committed governance config 属于 STRICT Finding。
3. Validator SHOULD 只检查路径、ignore、tracked 和 contract，不读取实际 local-only 内容。
4. local-only 环境事实变化通常不是规范性资产变更；但改变 committed local-state contract、默认 required 行为或安全边界属于本标准范围。

<a id="10-review-architecture-and-evidence"></a>
## 10. 审查架构与证据

### 10.1 正式审查（Formal Review）

**正式审查（Formal Review）**解决的是：

- 合同符合性（Contract Compliance / contract compliance）；
- 权威与一致性（Authority / Coherence）；
- 可操作性（Operability）；
- 证据诚实性（Evidence Honesty）；
- 放行决策（Release Decision）；
- 下游消费者影响、影响范围、回归等当前资产真实 failure mode。

Formal Review 仅在上述真实 failure mode 或 acceptance evidence contract 形成独立 Review function 的实际需要时激活，例如 implementation checks 不能单独覆盖的 consumer／compatibility／coherence 风险、Evidence Honesty 或 release decision adjudication。STANDARD／STRICT 本身不构成 activation trigger。

所有已激活的 Formal Review MUST 先按 Core 的 Authority、Contract Compliance、Coherence、Operability、Evidence Honesty 和 Release Decision 通用合同检查，再选用与资产、风险及真实 failure mode（actual failure mode）相称的专业证据。

Formal Review **不自动意味着**新会话、新上下文、独立上下文或 independent reviewer。

### 10.2 新上下文 / 独立上下文（Fresh / Independent Context）

**新上下文 / 独立上下文（Fresh / Independent Context）**解决会话或上下文污染（session/context contamination）：当现有上下文会削弱独立判断质量、需要新的认知起点，或明确需要独立判断时，选择新的 context/session routing。

它是 context/session routing 选择，不是 Review 类型本身，也不是 STANDARD／STRICT 的固定附属步骤。

### 10.3 受保护的独立审查（Protected Independent Review）

**受保护的独立审查（Protected Independent Review）**只有当**独立性本身（independence itself）就是 acceptance evidence 的组成部分**时 MUST 启用，例如：

- 外部或合同要求不得自我证明（external / contractual non-self-attestation）；
- 安全、权限、破坏性动作或 release certification；
- 已明确裁定的风险表明 self-review 会使 evidence claim 失效。

以下事实单独都 MUST NOT 触发 Protected Independent Review：

- normative asset；
- STANDARD；
- STRICT；
- Formal Review；
- canonical；
- complexity；
- file count；
- importance。

Protected Independent Review 一旦被 acceptance contract 要求，就属于 protected control，不得由 Override、Profile 或便利性绕过。

### 10.4 按证据选择，而不是固定仪式

风险等级只决定 evidence depth / protected-control scrutiny，不定义固定 ceremony。Review MUST 先识别真实 failure mode，再选择能证明或证伪它的证据。

不得把旧的固定 STANDARD／STRICT package 换成另一套固定 checklist。真实数据、外部状态、生产影响、消费者兼容、安全问题或人类判断，只有在当前 failure mode 命中时才进入证据集合。

## 11. Finding 归属的修复与定向复核

1. Review Finding 为满足原合同进行的修复（remediation）MUST 默认留在**同一 Work（same Work）**返回 IMPL。
2. **原 Review owner（original Review owner）**主责复核该 Finding；复核范围 MUST 与 Finding 的**影响半径（blast radius）**成比例。
3. 已定位的局部 Finding 不得机械触发 full rerun；只有 blast radius 证明更广回归必要时，才扩大验证范围。
4. 只有出现**新目标**、**新 capability**、**新 independent consumer**、核心合同边界变化，或当前 Work contract 无法覆盖的独立问题时，才返回 CTRL 判断是否建立新 Work。
5. 不得新增 `REVALIDATING` state、revalidation lifecycle、separate revalidation ledger，也不得在每次 `RETURN_TO_IMPLEMENTATION` 后机械 full rerun。
6. Finding 的既有状态和 Overall Decision 继续由 Core Review contract 主责；本节只定义 remediation ownership 和 recheck scope。

<a id="12-skill-specific-delta"></a>
## 12. Skill 专属增量（Skill-specific Delta）

正式 Skill 仍属于 normative asset；其通用治理 owner 是本标准，而不是独立 Skill lifecycle。

正式 Skill create、substantial change 或 Review 时，按以下顺序执行：

```text
先应用 Skill Design Principles
→ 识别真实 failure mode（actual failure mode）
→ 只选择适用的证据与验证
```

至少检查：

1. 加载 `skill-design-principles.md`，确认设计没有把开放能力不必要地写死；
2. 明确 input/output interface、producer / consumer 和实际 contract；
3. 检查 existing artifact / downstream impact，以及兼容、迁移或冻结成果是否受影响；
4. 检查 production / rebuild impact：是否需要 rebuild、是否影响 frozen output、是否改变 producer/consumer compatibility；
5. 按本标准完成 risk classification、authorization 和适用的 normative evolution log；
6. executable seam 只有在形成 persistent + recoverable sustained executable subsystem 时才 route 到 Specialist Execution Plane；一个 helper script 单独不足以触发；
7. software behavior seam 只有在 Software TDD Quality Floor 自身 applicability 成立时才适用 TDD，且与 Specialist activation 正交；
8. validation 依据**真实 failure mode（actual failure mode）**选择，不从“这是 Skill”推导固定测试套餐。

### 跨模型验证（Cross-model Validation）

只有当 **cross-model stability** / compatibility 本身是明确 **product promise**、runtime contract 或真实 consumer requirement 时，cross-model validation 才成为 required evidence，并可要求多个目标 model classes。

没有该承诺时，不自动要求 strong model + low-cost model、双模型回归或任何固定模型组合。

### 人工验收（Human Acceptance）

Human Acceptance 只在存在 **human-owned criterion** 时启用，例如 narrative quality、editorial judgement、subjective design quality、business decision 或 research judgement。

没有 human-owned criterion 时，不得把所有 Skill change 机械升级为用户验收套餐。

### 生产与既有成果

如果真实影响到 production 或 existing artifacts，MUST 判断 rebuild、frozen output、producer/consumer compatibility 和旧成果有效性；未命中这些影响时，不为形式制造 production ceremony。

### 能力选择顺序

完成 Principles 和 failure-mode identification 后，才分别判断是否需要 Formal Review、新上下文 / 独立上下文（Fresh / Independent Context）、Protected Independent Review、Software TDD、Specialist Execution Plane、Production Trace、Human Acceptance、real-run validation 或 cross-model validation。每个能力只按自己的 trigger 激活。

## 13. 授权、Git、演进日志与 Closeout

1. 风险初判、方案认可、Registry 状态或 Review 请求均不替代实施授权。
2. IMPL 只修改批准范围；出现新风险、未授权资产或重大合同变化时返回 CTRL。
3. 已被合同或实际 failure mode 激活且属于必需证据的 Review、入口新鲜度或非关键工具尚未完成时，MAY 继续合同范围内的分析、修复和验证，但 MUST 阻断 `ACCEPTED`；未授权写入、权威冲突、敏感信息、protected controls 或虚假证据必须停止受影响动作。
4. stage、commit、push、merge、tag、历史改写和发布继续遵守 `git-safety.md` 的逐项门禁；Override、直接维护和 LIGHT 不构成豁免。
5. Active Override 只有在正式 Review 通过且用户验收后才可生效。
6. 涉及正式文字 Skill 或其他规范性资产的有效变化时：正式 Work 在 `ACCEPTED`／Closeout 前 MUST 按 `docs/operations/normative-evolution-log.md` 更新根目录 `NORMATIVE_CHANGELOG.md`，或明确写出 `NOT_REQUIRED` 及原因；Direct Maintenance MUST 在最终返回／checkpoint 前完成同一 `UPDATED | NOT_REQUIRED` 判断，不因此创建 Planning／Review／Closeout 占位文件。
7. 已实施、已验证或进入正式方案后被纠偏、回退、取代或拒绝的方向，如形成以后可复用的约束，MUST 使用 `REDIRECT`、`REVERT` 或 `REJECT` 留下简短轨迹；普通脑暴、未成形建议和无复用价值的尝试不得记录。
8. 纯软件代码功能、代码 Bug、代码重构和依赖升级 MUST NOT 因本规则写入规范性资产演进日志；混合 Work 只记录文字 Skill／规范性部分，代码轨迹由 Trellis／软件 Release Notes 管理。
9. 演进日志只记录资产级简短变化、结果／教训和 Work／直接维护 Git 引用；MUST NOT 复制完整合同、逐 commit 细节或完整测试证据。
10. 正式 Work 的 Closeout MUST 记录等级、承载、授权、验证、适用时的 Review 结论、Git、生产影响、`Normative Evolution Log: UPDATED | NOT_REQUIRED`，以及新增／修改／停用 Override 的最终状态；Direct Maintenance 仅在其简短最终证据中保存同一日志判定，不创建 Closeout。
11. 上层 standard SHOULD 短而稳定；逐步操作、schema 示例和工具方法下沉到 Operations、模板或元 Skill。

## 14. 交叉引用

- 权威、四层模型、入口和核心记录：`core-protocol.md`
- Skill 顶层设计原则：`skill-design-principles.md`
- Specialist software seam：`docs/operations/specialist-execution-plane.md`
- Software behavior TDD：`software-tdd-quality-floor.md`
- 责任角色与 Return：`session-routing.md`
- Planning、Handoff 和归档：`planning-and-handoff.md`
- Git 用户门禁：`git-safety.md`
- 生产和旧成果：`production-trace.md`
- 规范性资产简短演进轨迹：`docs/operations/normative-evolution-log.md`
- Wave B 操作：`docs/operations/agents-base-overlay-overrides-local-state.md`

## 15. 来源映射

- 架构说明 v0.5：G12，第 11、13、18 节。
- 项目执行规范 v0.1：第 24～27、32～37、63～64、67、69 节。
- KC-015 Primary Task Contract：入口分离、Override 和 local-only 风险边界。
- KC-019 Primary Task Contract：规范性资产演进日志、代码排除和方向纠偏记录。
- KC-021 Frozen Full Design：Review Architecture、Skill Governance、Skill Design Principles、Work B migration／validation。
- KC-022 accepted foundation：Specialist Execution Plane + Software TDD Quality Floor。
