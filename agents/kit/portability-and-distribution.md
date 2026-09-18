# 可移植性与分发

**版本：v0.2-draft**
**依赖：`core-protocol.md`、`git-safety.md`、`production-trace.md`**

## 1. 目的与范围

本标准区分：

- 同一项目在不同 execution surface / computer 之间继续；
- shared Git 未承载的真实资产 transfer；
- controlled distribution；
- public release。

核心原则：**先判断状态由 shared Git authority 完整承载，还是存在必须真实搬运的资产。** “跨电脑”本身不自动要求 Transfer Bundle / Snapshot。

本标准不复制普通 Session Handoff、Git mutation mechanics 或 Run Manifest 字段规则。

## 2. 三种顶层模式

每次 portability / distribution 工作仍需明确：

- `PERSONAL_CONTINUATION`：同一所有者继续同一活动项目实例；
- `CONTROLLED_DISTRIBUTION`：向限定接收方交付稳定工作流，由其建立自己的项目状态；
- `PUBLIC_RELEASE`：向不受控环境发布可独立安装、验证、升级和回退的通用产品。

三种模式的业务目标不能混用；其中 `PERSONAL_CONTINUATION` 还要进一步区分 **Git-backed execution-surface handoff** 与 **real asset transfer**。

## 3. `PERSONAL_CONTINUATION`

### 3.1 先判定 handoff 类型

```text
remote ↔ computer-side
or computer A ↔ computer B
        ↓
required continuation state fully present in shared Git authority?
        ├─ YES → Git-backed execution-surface handoff
        └─ NO  → real asset transfer for the missing state
```

execution surface 只描述“在哪里执行”，不决定 Git mechanics；具体 mutation 仍按 `git-safety.md` 的 `WORKTREE_GIT` / `HOSTED_GIT_API` 选择。

### 3.2 Git-backed execution-surface handoff

当继续工作所需状态已经完整存在于 **shared Git authority**，且所引用 checkpoint 满足 Git Safety 的 remote portable completion 条件时，只需恢复：

- repository identity；
- **branch / ref / checkpoint**；
- expected HEAD / rollback anchor（当前动作需要时）；
- **local working-state expectation**，例如“预期 clean”“允许存在某个明确 local-only file”；
- Primary Contract / CURRENT / Review 等必要 context pointer；
- 下一动作需要的 authorization pointer / precondition。

此类 handoff：

```text
NO Transfer Bundle
NO mandatory Transfer Snapshot
NO manifest/hash package merely because execution surface changed
```

如果 shared remote 是项目 authority，而所需 semantic commit 只存在本地、尚未 push，则该 checkpoint 仍是 `LOCAL-ONLY / NOT YET PORTABLE`，不能把 handoff 宣称为 Git-backed portable completion。

Control continuity 的 context 恢复可以按 Work C 的 Reference Pattern 使用；但：

```text
Control Continuity Snapshot ≠ Transfer Snapshot
```

前者是 non-owner 控制上下文辅助，后者只在真实 asset transfer 需要时承担 transfer integrity pointer。

### 3.3 Real asset transfer

只要继续工作还依赖 shared Git 未承载的必要状态，就必须对该资产走真实 transfer integrity path。典型包括：

- `uncommitted local asset`；
- `private workbook`；
- local-only state；
- offline file；
- binary / large asset；
- machine-bound asset；
- shared Git 明确不承载但 continuation 必需的其他文件或数据。

此时仍需按资产风险保留：

- transfer manifest；
- path / size / requiredness；
- integrity / `hash`；
- source freeze / compatibility requirement；
- credential / sensitive-data exclusion；
- recipient verification；
- 必要时的 Transfer Snapshot，用来绑定 Git checkpoint、Bundle ID、环境与恢复检查。

示例载体 MAY 继续使用：

```text
agents/handoffs/transfer/<work-id>-<date>.md
local/transfer-manifest.json
```

但它们只在 real asset transfer 真实需要时创建，不是所有 cross-computer continuation 的默认 ceremony。

### 3.4 Real asset restore

接收侧至少：

1. 恢复已确认 Git checkpoint；
2. 按 transfer manifest 复制缺失资产；
3. 校验 hash / size / compatibility；
4. 验证 sensitive/local-only 边界；
5. 执行 recipient verification / smoke；
6. 确认源端 freeze / parallel-edit policy。

两端存在并行私有数据修改、无法证明 merge correctness 时返回 CTRL，不得自动合并。

## 4. `CONTROLLED_DISTRIBUTION`

交付包 MUST 包含适用的固定版本身份、稳定代码/Skill、合同、必要示例、测试、安装升级说明和 cold-start smoke。

交付包 MUST NOT 包含作者活动 Planning、CURRENT Handoff、私有输入、真实密钥或未验收开发状态。

接收方建立自己的 Work Index、Planning 和项目规则；不得把作者的个人活动项目状态当作共享 current-state owner。

如果 distributed artifact 本身走 Git/Release，其 commit/tag/Release/publication 仍由 `git-safety.md` 与 applicable release contract 控制。

## 5. `PUBLIC_RELEASE`

公开发布前至少验证：

- License / README quick start；
- dependencies / supported environment / safe config example；
- 可公开的 examples；
- input/output contract；
- smoke / troubleshooting；
- CHANGELOG；
- private path / credential / data scan；
- clean-environment cold start。

public push、tag、Release / publication 必须分别具有适用 authorization；普通 standing commit/push authorization 不隐含这些 protected actions。

## 6. Kit Source 与 Installed Snapshot

1. 上游 `standards/*.md`、安装快照 `agents/kit/*.md` 与 Registered Override 的 ownership 遵守 `core-protocol.md`。
2. 项目不得把 Kit source clone 当作业务项目本身。
3. 安装项目使用 `.workflow-kit.yml` 记录 Kit source commit、profile、ownership 与 local-only committed contract。
4. installed snapshots 必须绑定 immutable source commit；execution-surface handoff 不改变该 source identity。

## 7. Upgrade

Kit upgrade：

1. 读取当前 source identity 与目标 CHANGELOG；
2. 比较 managed files；
3. 区分 unmodified / local modified / Project Owned；
4. 生成差异预览；
5. 获得覆盖实际 mutation 的 action-specific 或 Scoped Standing Git Authorization；
6. 应用批准范围；
7. 运行 validation / smoke；
8. 更新 `.workflow-kit.yml`；
9. 若 commit + push 已在同一有效 authorization envelope 内，按 `git-safety.md` 直接执行并验证，**不要求机械地再次单独请求 approval**。

Upgrade 不得静默覆盖 Project Owned / local differences，不得因“升级”自动获得 destructive/shared-history/default-branch/Release 权限。

## 8. Kit Experience Feedback

1. 可能跨项目复用的经验先在项目内验证，再按现行 Candidate owner 判断是否记录。
2. Candidate 不是授权或 roadmap；promotion 仍需新的 Kit Change Work、相称验证和 acceptance。
3. portability field evidence 不得因为单一样本就扩大为 universal transfer machinery。

## 9. 场景速查

| 场景 | 正确路径 |
|---|---|
| remote → computer-side，所有需要状态已 push 到 shared Git authority | Git-backed execution-surface handoff；NO Transfer Bundle |
| computer A → computer B，semantic commit 只在 A 本地 | 先按授权完成 push 或明确承认 `LOCAL-ONLY / NOT YET PORTABLE`；不能伪称 Git-only handoff complete |
| private workbook 未提交且目标机需要 | real asset transfer：manifest + hash + recipient verification |
| local-only credential | 不进入 Git；若确需迁移，走受控私有 transfer，不进入普通 committed bundle |
| planned CTRL succession，无资产变化 | 可用 Control Continuity Snapshot；它不是 Transfer Snapshot |
| public release | 独立 release/publication authorization + release validation |

## 10. 交叉引用

- authority / ownership：`core-protocol.md`
- session/context continuation：`planning-and-handoff.md`
- planned succession：`docs/reference/control-continuity-succession-reference.md`
- commit/push/checkpoint mechanics：`git-safety.md`
- production asset identity：`production-trace.md`
- Human Work View：`docs/reference/human-work-view-reference.md`

## 11. Source Map

- 架构说明 v0.5：原 portability / distribution baseline。
- KC-006：private GitHub multi-computer field evidence。
- KC-021 Frozen Full Design：Work D portability / execution-surface handoff design。
- KC-025：Git-backed handoff 与 real asset transfer 分离；Control Continuity / Transfer Snapshot 解耦。
