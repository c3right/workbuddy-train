# Skill 设计原则

**版本：v0.1-draft**
**类型：薄型 Kit Base Standard / 模型与供应商中立（model/vendor-neutral）/ 项目中立（project-neutral）**

## 1. 目的与边界

本标准只保存长期稳定的正式 Skill 顶层设计原则。它定义设计取向，不定义独立 Skill lifecycle、固定 DoD、固定 Review 套餐、固定模型组合、固定 prompt 模板或项目专有生产路径。

这些原则必须能在模型能力继续增强时仍然成立。本标准**不是 lifecycle（not a lifecycle）**，也不替代 `normative-asset-change-control.md`、Specialist Execution Plane、Software TDD Quality Floor 或 Production Trace。

正式 Skill 的治理顺序是：

```text
先应用 Skill Design Principles
→ 识别真实 failure mode（actual failure mode）
→ 只选择适用的证据与验证
→ 只有其他能力自身触发条件成立时才启用
```

“这是 Skill”本身不得直接推出正式审查（Formal Review）、新上下文 / 独立上下文（Fresh / Independent Context）、受保护的独立审查（Protected Independent Review）、TDD、Specialist Execution Plane、Production Trace、人工验收、真实运行验证或跨模型验证的固定套餐。

## 2. 守住下限，放开上限

（Guard the Floor, Preserve the Ceiling）

Skill 规则只守住正确性（correctness）、安全性（safety）和 contract 所需的关键下限。超过下限后，应尽量保留模型判断、自主组合、表达方式和能力上限。

开放任务不得仅为了形式上的可靠性被写成逐步操作配方（procedural recipe）。只有真实失败模式证明需要约束时，才增加必要护栏。

## 3. 文字优先，只工程化确定性接口

（Text-first; Engineer Only Deterministic Seams）

文字型 Skill 默认用文字表达语义、判断、边界、流程和责任。

只有确定性机制（deterministic mechanism）确实增加价值时，才引入 Script、schema、parser、state machine、validator 或 rigid routing。一个 helper script 或少量可执行片段不自动要求把整个 Skill 工程化。

若形成持续、可恢复的 executable subsystem，按 Specialist Execution Plane 自身触发条件路由；若 software behavior 发生变化且存在 stable / repeatable / automatable seam，独立按 Software TDD Quality Floor 判断。

## 4. 按责任渐进加载

（Progressive Disclosure by Responsibility）

Skill 主体主责入口、流程和路由；Reference 主责详细知识、细节规则和按需材料。

默认采用渐进加载（progressive loading）：

- 先加载 Skill 主体；
- 根据当前任务责任再加载相应 Reference；
- 不把全部知识堆入主 Skill；
- 不把大量 Reference 在每次调用时机械预加载。

## 5. 基于证据演进，而不是补丁累积

（Evidence-driven Evolution, Not Patch Accumulation）

Skill 演进主要来自反复出现且被观察到的失败（recurring observed failure）或真实证据，而不是每遇到一个问题就叠加一条补丁。

维护时应：

- 合并重复规则；
- 删除失效或已被能力进步淘汰的规则；
- 优先修根因（root cause）；
- 不把临时 workaround 永久化；
- 避免 Skill 越改越长、越改越路径化。

单次偶发失败可以形成观察，但只有当证据足以证明长期约束有价值时，才提升为稳定规则。

## 6. 与治理规则的关系

正式 Skill 仍是 normative asset。其 create、substantial change 和 Review 的治理 owner 是 `normative-asset-change-control.md` 的 Skill-specific delta。

本标准不包含具体模型、供应商、业务项目 topology、固定 image/text generation flow 或固定 cross-model testing ceremony。需要这些约束时，必须来自明确产品承诺、consumer contract、项目 Overlay／Contract 或真实 failure mode，而不是本标准默认施加。
