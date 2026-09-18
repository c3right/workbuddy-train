# Software TDD Quality Floor（软件 TDD 质量下限）

**版本：v0.1-draft**
**类型：轻量 Kit Base Standard / vendor-neutral**
**默认：按 software behavior seam 惰性适用**

## 1. 目的与适用性（Purpose and Applicability）

本标准只定义软件行为变更的最低 TDD 证据下限，不定义具体测试框架、任务系统、vendor、语言或开发生命周期。

TDD 适用当且仅当：

```text
software behavior changes
AND
stable / repeatable / automatable behavior seam exists
```

“software behavior”包括可执行代码、runtime、parser、转换器、validator、自动化规则、API／接口实现以及可重复执行的软件设施行为。纯文字、研究判断、叙事、一次性人工分析或不存在稳定自动化 seam 的变化不因复杂度而自动适用 TDD。

TDD 与 Specialist Execution Plane、Trellis、Profile、Work Type 和风险等级正交。Specialist Plane inactive 时仍可能适用 TDD；`STRICT` 或 software-heavy 本身也不能证明 TDD 适用。

## 2. 最低纪律（Minimum Discipline）

当 §1 适用时，最低顺序为：

1. **实施前识别 seam（Identify seam before implementation）** — 实施前明确要改变的目标行为及其可重复观察方式；
2. **观察真实 RED（Observe real RED）** — 在同一 behavior seam 上真实执行检查并观察失败；
3. **验证 RED（Validate the RED）** — RED MUST 来自目标行为缺失／错误，而不是环境、路径、fixture、权限、依赖缺失或测试本身损坏；
4. **最小 GREEN（minimal GREEN）** — 做满足目标行为的最小实现，再在同一 seam 上观察通过；
5. **相关回归（relevant regression）** — 运行与该 seam 及其实际消费者相称的回归；
6. **Bug 回归（bug regression）** — 对可重现 bug，MUST 在 fix 前先得到一个 **failing regression test before the fix**。

不得先完成实现，再制造“像 RED 一样”的失败来追认 TDD。

## 3. 证据诚实性（Evidence Honesty）

```text
test exists ≠ TDD proved
```

以下证据边界必须保持：

- 新增测试第一次真实运行就是 PASS → `coverage hardening`，不是 RED evidence；
- 只看到测试文件或最终 PASS → 只能证明 coverage / regression 当前存在，不能证明 RED → GREEN chronology；
- RED 来自环境、路径、fixture、权限或依赖故障 → 不是目标 behavior RED；
- 当前 execution surface 不能运行目标测试／检查 → **MUST NOT claim RED / GREEN / regression completed**；应 route capability 或明确 evidence pending；
- 未保存 durable chronology 时，后续声明只能是 `test / regression coverage exists`，不得升级为 `RED → GREEN chronology proved`。

## 4. 不适用声明（NOT_APPLICABLE）

TDD judgement 对当前 Work 有实际意义、但 §1 不成立时 MAY 使用：

```text
TDD: NOT_APPLICABLE
Reason: <why no stable automatable software behavior seam exists>
Substitute validation: <evidence appropriate to the actual failure mode>
```

`NOT_APPLICABLE` 不是免验证。Substitute validation 必须针对真实失败模式，例如语义 Review、静态一致性检查、事实核验、人工验收或受控 production evidence。

纯文字／研究 Work 一般不需要为了形式写一条 TDD 记录；只有 TDD 判断本身会影响执行或放行时才需要落盘。

## 5. Chronology 证据归属（Chronology Evidence Ownership）

TDD chronology 复用既有 evidence owner；Kit 不新增 TDD 专用状态系统。

### 5.1 Specialist Plane active

由 **specialist plane's existing execution/check/task evidence owner** 保存 RED、GREEN、regression chronology。Kit Work 只保留 boundary / pointer 和跨轨道结论，不复制 specialist 内部 run history。

### 5.2 Specialist Plane inactive + Formal Work

由 **existing Work checkpoint / `progress.md`** 保存最小、事实性的 chronology，例如：

```text
TDD checkpoint — <behavior seam>
RED: <test/command or run pointer> → <target-behavior failure>
GREEN: <same seam> → PASS
REGRESSION: <relevant suite> → <result>
```

这只是现有 Work evidence 的一部分，不是第二份 TDD ledger。

### 5.3 无 Formal Work 的 bounded／direct maintenance

如果以后需要支持“本次确实执行过 TDD”的声明，chronology MUST 进入该维护本来就使用的 **existing durable action/Git evidence carrier**，例如 semantic commit body 或已有 maintenance/change record。

没有 durable chronology 时，只能声明 coverage / regression exists。

## 6. 禁止新增的治理机制（Forbidden New Governance Machinery）

本标准明确要求：

- **no dedicated TDD ledger**；
- **no TDD lifecycle**；
- **no TDD Gate**；
- **no dedicated TDD state file**。

TDD 是 behavior-seam quality floor，不是新的 Kit Work 状态机，也不要求为了 TDD 单独创建 Specialist task、Planning、Review 或审批。

## 7. 与其他权威的关系（Relationship to Other Authorities）

- Generic Specialist Execution Plane boundary：`docs/operations/specialist-execution-plane.md`
- Work / evidence honesty / Action Routing：`core-protocol.md`
- Formal Skill governance：`normative-asset-change-control.md` 的 Skill-specific delta；设计先读 `skill-design-principles.md`
- Production behavior / old outputs：`production-trace.md`
- Git evidence：`git-safety.md`

具体 specialist tool 可以检查 TDD evidence 是否诚实，但不得重定义本标准的适用性或把自己的 task state 提升为 Kit TDD authority。
