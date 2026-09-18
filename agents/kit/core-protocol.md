# 核心协议（Core Protocol）

**版本：v0.4-draft**
**适用对象：安装或引用 Agent Workflow Kit 的项目**

## 1. Purpose and Scope

本标准定义所有项目轨道共同遵守的最小控制面：权威、Work、状态载体、四层规则模型、两类入口、所有权、生命周期和自动化边界。

本标准不规定会话路由、Planning 文件操作、Skill 具体设计方法、Git 命令门禁、生产 Manifest 或迁移发布步骤；这些内容由对应 standard／Operations 负责。

## 2. Normative Terms

- **MUST（必须）**：不满足就不能宣称符合本标准。
- **MUST NOT（不得）**：明确禁止。
- **SHOULD（应当）**：默认执行；偏离时必须说明理由和影响。
- **MAY（可以）**：可选能力。
- **用户批准**：用户对具体动作或明确范围作出的清楚授权。

## 3. Authority

1. 项目 MUST 遵守以下总体权威顺序：

   ```text
   用户当前明确决定
   >
   已批准的 Primary Task Contract／正式 Contract／ADR
   >
   有效且已 Review／验收的 Registered Override
     仅在其 base_rule 与 scope 内
   >
   Kit Control Plane Entry／Project Domain Entry／适用 Kit Base
   >
   实际文件、Git diff、测试和真实产物
   >
   正式 Review、Closeout、Run Manifest
   >
   Planning 三件套
   >
   Session Handoff
   >
   聊天内容
   ```

2. Registered Override 只改变被其明确引用的 Kit Base rule，不得静默改变 Primary Task Contract、正式 Contract、ADR 或用户当前决定。
3. Kit standard 只有在项目安装或由 Kit Control Plane Entry 引用后才生效。
4. Kit Base 与 Project Overlay SHOULD 正交；发生实质冲突且没有有效 Override 时，Agent MUST 记录冲突、暂停受影响动作并返回 CTRL／用户。
5. Local-only State 只提供环境事实，不具有规范覆盖权。

## 4. Work Control

### 4.1 Formal Work Entry Check

1. Agent 在建立 Work ID 或套用完整 Work 生命周期前，MUST 先判断当前动作是否需要成为正式 Work。
2. 同时满足以下条件的边界清晰直接工作／维护 MAY 不建立正式 Work：
   - 单一、短期、范围明确，可在当前责任上下文完成，不需要多阶段接续或正式 Review；
   - 不改变治理规则、正式合同、公共接口、默认行为、数据口径、事实主责或需要长期维护的项目状态；
   - 不涉及高风险独立交付、外部写入、敏感信息、破坏性动作或难回退影响；
   - 意图、授权、实际产出或精确变更、验证和必要的 Git／工作区证据可由用户请求、产物、当前父 Work 或本次记录诚实追溯；
   - 涉及规范性资产时，还满足 Normative Asset Change Control 对非语义 LIGHT 直接维护的更窄要求。
3. 不能完整证明上述条件、出现语义 Finding、需要跨会话接续或需要正式放行时，MUST 建立正式 Work。
4. 直接工作／维护不是新的风险等级，不得用于拆分或规避 LIGHT／STANDARD／STRICT、专业生命周期、用户授权或 Git 门禁。
5. 未建立正式 Work 的动作不得宣称获得正式 Work Review、验收或 `ACCEPTED` 状态。

### 4.2 Formal Work Contract

1. 每个正式 Work MUST 有唯一且不可复用的 Work ID。
2. 每个正式 Work MUST 在 `agents/WORK_INDEX.md` 指定且只指定一份 Primary Task Contract。
3. Primary Task Contract MUST 至少说明目标、非目标、范围、约束、影响和验收。
4. 同一项目 MUST 只有一个由根目录 Planning 三件套直接服务的前台活动 Work。
5. WORK_INDEX 只保存导航和状态，不得复制合同或日常进度。
6. Planning、Handoff、README 或聊天内容不得静默改变 Primary Task Contract。
7. 目标、非目标、核心约束或验收重大变化时，实施者 MUST 暂停并返回 CTRL。
8. 不得拆分 STANDARD／STRICT 变更以规避门禁。

## 5. Control Plane and Execution Plane

1. Kit 控制面 MUST 管理：Work、Primary Contract、热状态、责任角色、Review、Closeout、影响判断、用户门禁、规则入口和安装完整性。
2. 专业执行面 SHOULD 由适用工具或流程管理：需要持续软件实施生命周期的 bounded seam 使用 generic Specialist Execution Plane；正式 Skill 由 Normative Asset Change Control 的 Skill-specific delta + Skill Design Principles 治理；生产由具体业务设施。
3. Specialist Execution Plane 只在 bounded subproblem 真实需要跨多步保持 coherent 的 persistent / recoverable software implementation lifecycle 时激活：必须存在 non-trivial executable behavior，并伴随 tests 和／或 dependency/build/release/check concerns。`STRICT`、Work Type、复杂度、Profile、文件／行数或一个 helper script 单独都不是触发条件。
4. 顶层 Work 即使属于 `SKILL_CHANGE`、Migration、Research，也不得压掉其中真实存在的 sustained software subsystem；反之，软件标签也不得自动创建 Specialist task。
5. 控制面 MUST 只保存跨轨道状态、boundary 和 pointer，不得复制执行面内部完整日志、task ledger、journal 或 task state。
6. 当前 execution surface 无法真实执行所需 software seam 时，MUST 保留当前 authority／scope，将 bounded seam route 到具备能力的 execution surface 或 specialist plane；不得虚报测试、构建或 TDD execution。
7. Generic Specialist 语义详见 `docs/operations/specialist-execution-plane.md`。

### 5.1 Four-layer Rule Model

#### Kit Base

1. Kit Base 来自 `.workflow-kit.yml` 指定的固定 source commit。
2. Manifest 标记为 Kit Managed 的 `agents/kit/*.md` snapshots 及其他 Kit Managed 资产属于 Kit Base。
3. 业务项目 MUST NOT 直接修改 Kit Managed 快照。
4. 升级 MUST 选择新的 source commit，比较差异并取得相称授权；不得静默跟随移动上游。

#### Project Overlay

1. Project Overlay 表达项目用途、业务术语、目录、领域流程、专业约束和项目权威来源。
2. Project Overlay 属于 Project Owned。
3. Overlay MUST NOT 复制 Kit Base 已定义的完整通用治理正文，也不得创建相同事实的竞争性来源。
4. Overlay 默认入口是 `.workflow-kit.yml` 登记的 Project Domain Entry。

#### Registered Overrides

1. 项目确需偏离明确 Base rule 时，MUST 在 `.workflow-kit.yml` 登记的 Override registry 中使用“登记＋引用”。
2. Override MUST 至少记录 `id`、`base_rule`、`project_rule`、`reason`、`scope`、`owner`、`status`、`reviewed_at`、Review 引用、验收引用和依赖。
3. 只有 `active` Override 参与规则层优先级；其他状态不覆盖 Base。
4. Active Override 的引用 MUST 存在，scope MUST 明确，依赖 MUST 无循环，并 MUST 经过正式 Review 和用户验收。
5. 同一 Base rule 的 active scope 不得重叠；重复 ID、失效引用、循环或冲突必须失败关闭。
6. Override MUST NOT 绕过 protected controls：用户批准、Git 门禁、acceptance contract 明确要求的 Protected Independent Review、Production Trace、Kit Managed 不可直接修改和敏感数据边界。
7. Override MUST NOT 包含秘密、凭据或绝对本机路径。

#### Local-only State

1. Local-only State 保存机器、Host 或个人环境事实，不是 Overlay 或 Override。
2. Committed `.workflow-kit.yml` 只登记相对路径、ignore 要求和允许模式；实际机器值 MUST 存在于被 ignore 且未 tracked 的 local-only 文件。
3. Local-only 实际文件 MUST NOT 进入 Manifest required committed files。
4. 缺失的 Warning／Error 由 committed contract 的 `required` 决定；文件存在但未 ignore、已 tracked 或路径逃逸时 MUST Error。
5. Validator SHOULD 不读取 local-only 文件内容。

### 5.2 Two Entry Surfaces

#### Kit Control Plane Entry

1. 默认路径是根 `AGENTS.md`，由 `.workflow-kit.yml` 明确登记。
2. 它 MUST 提供：当前 Work、Action Routing Index、Project Domain Entry、Override registry、local-only 边界和停止／返回条件。
3. 它 SHOULD 只保存短摘要和指针，不复制完整 standards 正文或项目全部领域文档。

#### Project Domain Entry

1. 默认路径是 `docs/project/domain-entry.md`，由 `.workflow-kit.yml` 明确登记。
2. 它 MUST 指向项目用途、术语、目录、专业流程、领域约束和项目权威文档。
3. Profile 增量 SHOULD 合并到 Project Domain Entry，不应扩张根 AGENTS。
4. Control Plane Entry 与 Project Domain Entry MUST 是两个不同文件。

#### Cold Start / Minimum Sufficient Context

```text
Control Plane Entry
→ .workflow-kit.yml
→ Override registry
→ WORK_INDEX
→ 有活动 Work 时读取 Primary Task Contract
→ 按当前 assignment 的 Minimum Sufficient Context 只读必要 Planning / CURRENT / Review owner
→ Action Routing Index
→ 当前动作适用的 standard
→ 需要领域信息时读取 Project Domain Entry 及其指针
→ 需要环境事实时检查 local-only state
```

Mandatory read-set 是“如果不读就不能安全或正确完成当前任务”的最小集合。historical evidence、retrospective、archive、old Review 默认 pointer-first / on-demand；Cold Start 不等于 Full Historical Reload。不得要求每次无差别加载全部 standards、全部领域文档或整个 repository 历史。

### 5.3 On-demand Module Activation

1. Profile 描述项目长期形态和 **capability availability**，不表示所有专业 Module 对每项工作永久生效。
2. Module 使用以下解释性语义，不构成持久运行时状态机：
   - `CORE`：正式 Work 共同遵守的治理下限；
   - `AVAILABLE / DORMANT`：能力可用，但当前不创建文件、不增加步骤或关闭义务；
   - `ACTIVE_FOR_CURRENT_WORK`：当前用户意图、Primary Contract 或项目事实命中触发条件；
   - `EXPERIMENTAL / PROJECT_LOCAL`：仅在项目内验证，尚未成为 Kit 通用能力。
3. Agent MUST 根据当前动作自动识别适用 Module，并通过 Action Routing Index 只读取对应规则；用户不需要记忆或操作内部 Module 开关。
4. Profile、代码目录、已安装工具或历史上使用过某 Module，单独均不足以激活它。
5. `specialist_execution_plane` capability 在 Profile 中可用，但只有第 5 节的 sustained software seam 判据满足时才 active；`software_tdd` capability 只有 software behavior changes 且存在 stable / repeatable / automatable behavior seam 时适用。
6. `skill_design_principles` capability 只在正式 Skill create、substantial change 或 Review 时加载；它提供设计原则，不自动激活 Specialist、TDD、Production、cross-model validation 或 Protected Independent Review。
7. `software_tdd` 与 `specialist_execution_plane` 正交：TDD 适用时不得为了保存 chronology 而反向创建 Specialist lifecycle；Specialist active 也不自动证明 TDD 适用。
8. 激活专业 Module 只增加当前工作所需的专业义务，不得静默改变合同、授权、风险等级或其他休眠 Module。
9. 当前 Work 结束后，未被项目权威文件明确设为持续默认的专业 Module 恢复为 `AVAILABLE / DORMANT`。

## 6. Lifecycle Separation

1. Kit Work、Specialist software implementation 和生产运行的责任边界 MUST 分离；只有命中 Specialist semantic applicability 的 software seam 才进入独立可恢复的 specialist implementation lifecycle。
2. 正式 Skill 是 normative asset，不建立 standalone Skill lifecycle；其通用 governance 由 `normative-asset-change-control.md` 的 Skill-specific delta 主责，设计原则来自 `skill-design-principles.md`。
3. Software TDD 是 behavior-seam quality floor，不是新的生命周期；其适用性按 `software-tdd-quality-floor.md` 独立判断。
4. 每项变更 MUST 执行接口影响检查；跨多个轨道、多个独立消费者、语义口径或迁移周期的变化 SHOULD 升级为父级数据合同变更。
5. 涉及生产运行或旧成果影响时 MUST 遵守 `production-trace.md`。生产 Work 本身不自动激活 Specialist Plane；repair/facility/software seam 满足第 5 节时可单独激活。
6. 正式 Work 关闭前 MUST 有可识别的验收、适用时的 Review 结论、Git 和生产影响结论。

## 7. Core Records

| 记录 | 唯一职责 |
|---|---|
| Primary Task Contract | 为什么做、做什么、守住什么、怎样验收 |
| Planning 三件套 | 当前推进、开放发现和最新 checkpoint |
| Session Handoff | 真实责任／上下文交接需要时的 durable recovery envelope；不拥有 lifecycle、Review、Git 或 authorization |
| Review | Formal Review 激活时的正式 Finding 和放行结论 |
| Closeout | 终止节点的可读历史主线 |
| Git | 真实文件差异和可回滚基线 |
| Override registry | 对 Base rule 的受控偏离和证据 |
| `.workflow-kit.yml` | 安装、入口、所有权和 local-only committed contract |
| Specialist internal evidence | 由被选择的 specialist plane 主责；Kit 只保存 pointer / boundary |
| TDD chronology | 复用 specialist existing owner、Formal Work `progress.md`／checkpoint 或既有 durable action/Git evidence carrier |

同一事实 MUST 由一类记录主责；其他记录只保存指针或必要摘要。不得新增 TDD ledger、TDD lifecycle、TDD Gate 或专用 TDD state file。Task Capsule、Control Continuity Snapshot 和 Lightweight Reference 同样不得成为新的 current-state owner。

## 8. Review

1. Formal Review 一旦按适用规则被激活，MUST 保存于 `agents/reviews/<work-id>.md`，由 REVIEW 维护；仅符合规范资产直接维护边界的窄范围核查 MAY 按变更控制标准合并记录。
2. Review MUST 包含 Scope、Evidence、Findings 和 Overall Decision。
3. 所有正式 Review MUST 检查：
   - **Authority**：用户决定、合同、Base／Overlay／Override 和所有权是否正确；
   - **Contract Compliance**：目标、非目标、范围和验收是否满足；
   - **Coherence**：规则、实现、文档、状态和消费者之间是否一致；
   - **Operability**：实际是否可运行、接续、验证和回退；
   - **Evidence Honesty**：未执行的测试、Review、验收或生产不得宣称通过；
   - **Release Decision**：明确 `PASS`、接受风险、返回实施或阻塞。
4. Formal Review 是放行判断，不等于 Fresh / Independent Context，也不等于 Protected Independent Review。三者的责任边界和启用条件由 `normative-asset-change-control.md#10-review-architecture-and-evidence` 主责。
5. 通用 Review 负责组合证据和作出放行结论，不得替代软件、正式 Skill、数据、事实核验或生产的专业 Review 方法。
6. Finding MUST 记录 Severity、Status、合同引用、证据、影响、Required Change、Acceptance Check、Implementation Response 和 Recheck Result。
7. Finding Status 只允许：`OPEN`、`IN_PROGRESS`、`READY_FOR_REVIEW`、`RESOLVED`、`ACCEPTED_RISK`、`REJECTED`。
8. 只有 REVIEW 或 CTRL 可以标记 `RESOLVED` 或 `ACCEPTED_RISK`；IMPL 只能提交证据并标记 `READY_FOR_REVIEW`。
9. Overall Decision 只允许：`PASS`、`PASS_WITH_ACCEPTED_RISK`、`RETURN_TO_IMPLEMENTATION`、`BLOCKED`。
10. 为满足原合同而修复 Review Finding，MUST 默认返回同一 Work 的 IMPL；same Work remediation 由 original Review owner revalidate，范围与 Finding blast radius 成比例。只有原合同无法覆盖的新目标、新 capability、新 independent consumer、合同核心边界变化，或原 Work 已可诚实放行的额外优化，才返回 CTRL 判断是否建立新 Work。
11. 不得创建 `REVALIDATING` state、独立 revalidation lifecycle／ledger，也不得在每次 RETURN 后机械 full rerun。
12. 已被合同或实际 failure mode 激活且属于必需证据的 Review 未通过或风险未明确接受时，Work MUST NOT 进入 `ACCEPTED`；这只阻断状态提升，不阻断合同范围内的分析、修复和验证。
13. Active Override 的 Review MUST 检查 Authority、scope、protected controls、兼容性和回退，不得只检查 JSON 语法。

## 9. Closeout and Decision Promotion

1. Work 在 `ACCEPTED`、长期 `SUSPENDED`、`ABANDONED` 或 `SUPERSEDED` 时 MUST 创建 Closeout。
2. `ACCEPTED` Closeout 前 MUST 确认合同、适用时的 Review 结论、Planning、Git、生产影响和入口面新鲜度；Human Acceptance 只在 Primary Task Contract 存在真正 human-owned criterion 时属于适用验收证据。
3. Closeout MUST 记录原始目标、最终结果、重要决定、合同偏离、适用时的 Review／验收、Git 证据、生产影响、已知限制、长期决策提升和未来入口。
4. 长期知识按职责提升：控制面摘要到 AGENTS；领域规则到 Project Domain Entry／权威文档；架构到 ADR；接口到 contracts；环境程序到 Operations；跨项目经验到 KIT_CANDIDATES。
5. Candidate Harvest 只在 Closeout，或 reusable cross-Work / cross-project learning 已经实际 materialize 的 meaningful milestone 做一次轻量判断：`Kit Feedback: NONE | <candidate pointer>`。`NONE` 不生成 artifact；不得 per-IMPL、per-RETURN 检查，也不得新增 Candidate ledger、Gate 或 mandatory retrospective。
6. Closeout 不得替代 Git 历史、Primary Task Contract 或已激活的正式 Review。

## 10. File Ownership

1. **Kit Managed**：由 Kit 发布和升级管理；项目 MUST NOT 直接修改。
2. **Project Owned**：由项目维护；Kit 升级 MUST NOT 覆盖。
3. **External Managed**：由外部工具维护；Kit MUST NOT 修改其内部实现或 Hook。
4. Kit 上游 `standards/*.md` 是发布源；业务项目 `agents/kit/*.md` 是固定快照。
5. Local-only 实际状态不属于 required committed ownership list。

## 11. 自动化与 Git 授权边界

Kit 自动化 MUST NOT：

- 选择 Host 或模型；
- 执行**未授权或 silent Git mutation**；
- 把普通 commit/push authorization 扩大为 merge、tag、shared-history rewrite、destructive reset/clean/discard、Release/publication 或其他 protected action；
- 覆盖 Project Owned 或 Kit Managed 本地差异；
- 修改 External Managed；
- 读取 local-only 文件内容或传输私有数据；
- 自动生成、激活或迁移 Override；
- 自动修复安装；
- 建立隐藏的持久 Module 状态或因 Profile 自动启用全部专业流程。

Git mutation 的 Core invariant：

```text
Unauthorized / silent Git mutation
→ FORBIDDEN

Valid action-specific authorization
OR valid Scoped Standing Git Authorization
→ executable only inside exact 精确 envelope
```

当 action-specific authorization 或 `Scoped Standing Git Authorization` 已覆盖当前 commit / push 的 repository、branch、scope、preconditions 与 rollback boundary 时，Agent MAY 执行该动作并完成验证；同一有效 envelope 内**不重复请求** approval。

standing authorization 不扩大权限。任何 branch/baseline/target scope/rollback anchor/validation prerequisite/sensitive-data boundary/unrelated mutation 的 **precondition drift** 都使受影响动作暂停并重新评估；必要时重新取得授权。

force push、destructive reset/clean、shared-history rewrite、tag/Release/publication 等 **protected action** 不因普通 standing authorization 静默获得许可。

自动化 MAY 生成只读检查、dry-run、差异预览、候选动作，或在有效授权 envelope 内执行已授权且满足 `git-safety.md` mechanics/postcondition 的 mutation；高风险状态变化仍由其专属授权边界控制。

## 12. Action Routing Index

本节是动作到首读 standard 的唯一权威索引。它只导航现有规则，不复制其他 standards 正文，不创造新授权。项目入口和 Operations SHOULD 只链接本节或提供短摘要。

| 动作 | 首读 standard | 补充文件／规则 | 停止／返回条件 |
|---|---|---|---|
| 判断是否需要正式 Work、建立 Work ID 或重大修改 Primary Contract | `core-protocol.md` | Control Plane Entry、WORK_INDEX、拟议合同、task_plan；再按资产类型读取专业 standard | 直接工作／维护条件无法证明、Work ID／唯一合同不清、存在另一前台 Work、范围或授权冲突 |
| 判断当前动作激活哪些 Module | `core-protocol.md` | Profile、Project Domain Entry、Primary Contract；命中后读取专业 standard | 触发事实、授权、专业边界或与项目既有方法的关系不清 |
| 判断 bounded subproblem 是否需要 Specialist Execution Plane | `core-protocol.md` | `docs/operations/specialist-execution-plane.md`、当前软件 seam、现有项目 workflow／External Managed pointer | 只有 STRICT／Work Type／复杂度／文件数／helper-script 等 proxy，或 execution capability／owner 不清 |
| 判断 software behavior seam 是否适用 TDD、保存 RED→GREEN chronology | `software-tdd-quality-floor.md` | Specialist evidence owner（若 active）或现有 Work／durable action evidence | 无 stable automatable seam、RED 原因不真实、当前 surface 不能执行却试图宣称完成 |
| 判断或输出 `STAY`／`CREATE`／`RETURN` | `session-routing.md` | `planning-and-handoff.md`、当前合同；CURRENT 仅在真实 durable handoff need 时读取 | Delta State Sync owner evaluation 未完成、Return Target／授权不清 |
| 更新 Planning、Handoff、切换 Work 或归档三件套 | `planning-and-handoff.md` | Core、合同、WORK_INDEX；Git/authorization 只在下一动作需要时核验 | canonical owner 矛盾、三件套指向不同 Work、归档顺序或必要前提不清 |
| 修改或 Review 规范性资产 | `normative-asset-change-control.md` | Core、Git Safety、资产专属规则 | 未分级、未授权、范围扩大或命中更高风险 |
| 修改或 Review 正式 Skill 资产 | `normative-asset-change-control.md` | `skill-design-principles.md`；按实际 seam 再读 Specialist／TDD／Production | 未加载 Principles、input/output／producer/consumer／实际影响不清，或试图从“Skill”直接套固定验证套餐 |
| 执行 Git 写动作 | `git-safety.md` | 当前合同、实际 Git mechanics profile、Git/worktree 或 Hosted API facts；必要时 Portability | 无 action-specific/standing authorization、authorization envelope/precondition drift、unrelated/ambiguous mutation、base-dependent stale ref、protected action 不在授权内或恢复性不清 |
| 执行正式生产或判断旧成果 | `production-trace.md` | 合同、输入、设施版本、Git commit、质量证据 | 开发／生产边界、版本、敏感数据或重跑责任不清 |
| 跨电脑/执行面接续、真实资产传输、交付、公开发布或 Kit upgrade | `portability-and-distribution.md` | Git Safety、Planning、Production Trace | Git-backed / real-asset 类型不清、checkpoint 不 portable、真实资产 integrity 不足、发布批准、私有边界或恢复验证不清 |
| 选择 Profile、应用模板或验证安装 | `core-protocol.md` | 应用导览、Profiles、Manifest README、Validator Operations | 读取／写入授权、Profile、merge、source commit 或所有权不清 |
| 修改 Overlay、登记 Override 或处理 local-only state | `core-protocol.md` | Control Entry、Domain Entry、registry、workflow、Wave B Operations、规范资产变更控制 | Base／Overlay 冲突、失效引用、scope 冲突、protected control、秘密／绝对路径或 ignore／tracked 边界错误 |

一个动作命中多行时 MUST 读取所有适用首读 standard。发现索引与正文冲突时按第 3 节处理并停止，不得现场解释绕过规则。

## 13. Cross-References

- 责任角色与路由：`session-routing.md`
- 热状态与交接：`planning-and-handoff.md`
- Specialist Execution Plane：`docs/operations/specialist-execution-plane.md`
- Software TDD Quality Floor：`software-tdd-quality-floor.md`
- Skill Design Principles：`skill-design-principles.md`
- 规范性资产变更与 Skill-specific delta：`normative-asset-change-control.md`
- Git authorization / mechanics / checkpoint：`git-safety.md`
- 生产追溯：`production-trace.md`
- 接续和发布：`portability-and-distribution.md`
- Human Work View conditional projection：`docs/reference/human-work-view-reference.md`
- Wave B Operations：`docs/operations/agents-base-overlay-overrides-local-state.md`

## 14. Source Map

- 架构说明 v0.5：第 3～7、10～15、17～20 节。
- 项目执行规范 v0.1：第 1～9、16～18、28～31、44～46、63 节。
- KC-015 Primary Task Contract：四层模型、两类入口、Override 和 local-only 边界。
- KC-021 Frozen Full Design：Specialist/TDD foundation（Work A）、Review + Skill Governance consolidation（Work B）、Session Routing / Delta State（Work C）与 Git/Portability/Human Work View（Work D）。
- KC-025：Core Git authorization execution invariant 与 action routing reconciliation。
