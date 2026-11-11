# Kit Candidates

本文件是项目侧唯一的 Kit Candidate owner，只记录由 Agent Workflow Kit 引起、暴露或可能通过修改 Kit 而在多个任务／项目中改善的问题。

项目自身的业务需求、代码缺陷、领域知识、一次性环境故障和只对本项目成立的偏好不得记录在这里；它们应进入项目自己的合同、Finding、Issue、ADR、Operations 或普通文档。

Candidate 是非规范性证据池，不构成实施授权，也不得静默改变 `agents/kit/*.md`、项目 `AGENTS.md` 或当前 Work。

## Candidate Harvest

只在以下时点做一次轻量判断：

- Closeout；或
- 真正有意义、且 reusable cross-Work / cross-project learning 已经 materialize 的 milestone。

判断结果只允许：

```text
Kit Feedback: NONE
```

或：

```text
Kit Feedback: agents/KIT_CANDIDATES.md#<candidate-id>
```

规则：

- `NONE` 不生成 artifact；
- 不 per-IMPL 检查；
- 不 per-RETURN 检查；
- 不新增 Candidate ledger / Gate / mandatory retrospective；
- 只有 reusable cross-Work / cross-project learning 才进入本文件；
- Candidate 不自动升级为 Work，仍需证据、范围和用户授权。

## 记录触发

满足以下条件时 SHOULD 记录候选：

- 同一 Kit 问题在一个项目中重复出现；
- Kit 的默认规则、模板或入口导致明显误解、遗漏、重复状态或额外责任链；
- 项目形成了可跨任务复用的 workaround；
- Agent 在执行 Kit 时需要反复重新设计同一种操作方法；
- 真实项目证据表明现有默认过重、过轻或不适用于某类项目。

## 状态

- `OBSERVED`：已出现一次，通用性尚未证明；
- `PROJECT_VALIDATED`：已在同一项目的第二任务／第二场景复现或验证；
- `FORWARDED`：已提炼并转入 Kit 上游候选池；
- `REJECTED`：确认不适合进入 Kit；
- `PROMOTED`：已由正式 Kit Change 提升，并记录目标资产。

## 候选模板

### `<KIC-P-xxx>`：<候选标题>

#### Metadata

- Status：`OBSERVED`
- First Observed：`<YYYY-MM-DD>`
- Source Work：`<WORK-ID>`
- Source Closeout：`<path or PENDING>`
- Project Profile：`<skill-heavy|hybrid|software-heavy>`
- Kit Version / Source Commit：`<version / sha>`
- Affected Kit Area：`standard / template / operations / adapter / onboarding / tooling`

#### Observation

实际发生了什么？只写与 Kit 行为有关的事实。

#### Kit Relevance

为什么这是 Kit 的通用问题，而不是本项目独有问题？

#### Evidence

- 对应合同、Handoff、Review、Closeout、diff 或运行记录；
- 是否重复出现；
- 造成了什么错误、返工、上下文成本或理解困难；
- 反事实：如果没有 Kit 或采用另一默认，结果会怎样。

#### Current Workaround

本项目目前怎样处理？该处理是否已经在第二任务／第二场景验证？

#### Candidate Improvement

建议修改 Kit 的哪一层：standard、template、operations、adapter、onboarding 或 tooling？

#### Complexity Impact

- 是否增加日常理解负担？
- 是否增加文件、状态树或强制交互？
- 是否可以通过默认值、按需读取或可选模块保持简单？
- 是否会让 LIGHT／常规任务过度治理？

#### Applicability and Counterexamples

适用于哪些项目、Work 或证据形态？哪些情况不应采用？

#### Promotion Recommendation

- `KEEP_LOCAL`
- `NEEDS_ANOTHER_TASK`
- `NEEDS_ANOTHER_PROJECT`
- `FORWARD_TO_KIT`
- `REJECT`

#### Forwarding Record

- Forwarded At：`N/A`
- Upstream Candidate：`N/A`
- Promotion Work：`N/A`
- Final Disposition：`PENDING`

---

当前无候选。
