# Git 安全与执行机制

**版本：v0.3-draft**
**依赖：`core-protocol.md`**

## 1. 目的与范围

本标准规定 Git mutation 的共同安全下限、授权执行语义、`WORKTREE_GIT` / `HOSTED_GIT_API` 两种 mechanics profile，以及 operator-facing checkpoint completion semantics。

本标准只回答两个问题：

1. 已经获得的 Git authorization 怎样在真实 mutation mechanism 上安全执行；
2. mutation 完成后，怎样证明结果仍在授权 envelope 内并可恢复。

它不重新定义业务上是否应获得授权，也不把 `remote` / `computer-side` 等 execution surface 当作 mechanics enum。

```text
Execution surface ≠ Git mechanics profile
mechanics 不授予 authorization
```

## 2. 共同安全不变量

### 2.1 授权先于 mutation

未授权或 silent Git mutation MUST NOT 执行。可执行 mutation 只来自：

- 针对具体动作与范围的 action-specific approval；或
- 当前仍有效、覆盖该动作精确 envelope 的 `Scoped Standing Git Authorization`。

已有有效 standing authorization 时，同一 envelope 内已授权的普通 commit / push **不重复请求** approval；重复询问本身不增加安全性。

standing authorization：

- MUST NOT 扩大用户实际授予的权限；
- MUST NOT 把“authorization exists”解释成“all Git mutations allowed”；
- 在 branch、baseline、target scope、rollback anchor、validation / Review prerequisite、sensitive-data boundary、unrelated concurrent mutation 等 **precondition drift** 后立即暂停受影响动作并重新判断；
- 不静默覆盖任何 protected action。

### 2.2 Protected / destructive boundary

普通 action-specific commit/push approval 或普通 Scoped Standing Git Authorization MUST NOT 静默覆盖：

- force push；
- amend、rebase 或其他 shared-history rewrite；
- destructive reset / clean / discard；
- tag、Release、publication；
- 创建、修改或删除 remote；
- 删除默认分支或其他未明确授权 branch；
- 修改授权范围外 repository / Work / file scope；
- 用户无关修改、敏感信息或不可可靠回滚动作。

若用户确实要求 protected / destructive action，必须重新解析精确目标、影响与恢复路径，并取得覆盖该动作的明确授权。

### 2.3 Sensitive data、scope 与 rollback

任何 profile 都必须：

- 避开 secrets、真实敏感数据和 machine-only state；
- 保留 unrelated user work，不得假定可以清理；
- 在 mutation 前有可识别 rollback anchor；
- 只改变已授权 scope；
- mutation 后执行足够 postcondition verification；
- 未执行的验证、Review 或远端写入不得虚报成功。

## 3. 授权载体

### 3.1 Action-specific approval

没有有效 standing authorization 时，下列 mutation 必须按动作与范围明确获批：commit、push、merge、tag、amend、rebase、reset/clean、remote mutation、branch deletion、discard、publication。

commit approval 不等于 push approval，除非用户明确把二者放入同一 action-specific envelope。

### 3.2 Scoped Standing Git Authorization

standing authorization 至少要能确定：

```markdown
## Scoped Standing Git Authorization

- Repository:
- Work / Goal:
- Allowed branch or branch pattern:
- Allowed actions:
- Exact file / directory scope:
- Preconditions:
- Rollback anchor:
- Expiry / revocation condition:
- Forbidden actions:
- User authorization reference:
```

这些事实可以保存在现有 Primary Contract、CURRENT、用户明确决定或其他既有 durable evidence carrier 中；**不得为了 standing authorization 新增 ledger / lifecycle / registry**。

普通 standing authorization MAY 覆盖：安全 Work branch、明确范围 mutation、semantic/checkpoint commit、当前 Work branch 的 non-force push，以及用户明确包含的其他动作。它是否覆盖 merge 等更高影响动作，只由实际授权文本和适用 protected-control rule 决定，不因模板字段自动获得。

兼容引用锚点：既有 active consumer 曾引用 `### 4.2 Scoped Standing Git Authorization`；本版不据此创建第二个 owner，授权语义仍由本节主责。原 protected-control wording 继续等价成立：`reset、clean、丢弃修改` 与 `tag、Release 或公开发布` 不在普通 standing authorization 内。若 scope / branch / baseline / `Review、验证、Open Findings、PR head SHA` 等 prerequisite 漂移，或出现 `回滚锚点失效`，则 `持续授权立即暂停`受影响 mutation，重新评估后才可继续。

## 4. `WORKTREE_GIT` mechanics profile

`WORKTREE_GIT` 用于真实工作树、index 与本地 Git 命令是 mutation mechanism 的场景。它不意味着 execution surface 必须是 `computer-side`。

### 4.1 Preflight 与 dirty-state 分类

mutation 前至少确认 repository、branch、HEAD、rollback anchor、remote/tracking（若 push）、worktree/index 状态与 authorization envelope。

按真实状态区分：

- **clean worktree**：无未解释 local changes；
- **unrelated dirty state**：存在可明确归属、与当前 scope 不相交的修改；必须保留并避开；
- **mixed file changes**：同一文件同时包含当前 Work 与无关改动；必须用明确 hunk/等价机制分离，无法可靠分离就暂停；
- **ambiguous dirty state**：归属或相交关系不清，必须 fail closed。

不得自动 stash/reset/clean 解决 dirty state。

### 4.2 精确 staging

1. stage MUST 使用**明确路径**或交互式片段选择；
2. 默认 MUST NOT 使用 `git add .`、`git add -A`、`git commit -a`；
3. stage 后 MUST 检查 `git diff --cached`；
4. committed set MUST 等于授权且已验证的 semantic unit；
5. 不得暂存用户 unrelated changes。

### 4.3 Commit / push

- commit 前确认 staged diff、validation sufficiency、sensitive-data boundary 与 rollback anchor；
- push 前确认 remote identity、目标 branch、non-force / fast-forward 条件与 standing authorization preconditions；
- push 失败时不得把 local commit 宣称为 remote portable checkpoint。

## 5. `HOSTED_GIT_API` mechanics profile

`HOSTED_GIT_API` 用于 GitHub / GitLab 等 hosted SCM API 是 mutation mechanism 的场景。它不意味着 execution surface 必须是 `remote`；同一个 remote execution surface 也可能使用 worktree Git。

每次 hosted mutation **先按 semantic dependency 分类**，不得按 API convenience 分类。

### 5.1 `base-dependent / coupled` mutation

如果 correctness / meaning 依赖任一事实：

- branch HEAD / base commit；
- parent commit 或 ref；
- **多文件共同状态**；
- repository-wide consistency；
- 某个读取时基线 A 对 mutation 语义的解释；

则属于 `base-dependent / coupled`。

必须：

```text
read expected parent/ref
→ build the complete semantic unit
→ atomic or equivalent fail-closed CAS
→ single ref transition / equivalent atomic publish
→ verify resulting ref + content postconditions
```

其中：

- `expected parent/ref` 是并发前提，不得只依赖 target blob SHA；
- `CAS` 指 compare-and-swap 或语义等价的 fail-closed ref transition；
- coupled multi-file unit **不得逐文件顺序写入**，再在最后才发现 split state；
- target file 的 blob 未变化并不能证明 branch base 未变化。

Mandatory adversarial invariant：

```text
read base = A
target blob 未变化
branch moves A → B
mutation meaning depends on A
→ 写入前失败
```

也就是说，branch/ref 已 stale 时必须在 publish 前失败；不得因为 target blob SHA 仍相同就把 stale-base mutation 当成安全。

### 5.2 `truly path-local` mutation

只有明确证明 **unrelated branch movement is semantically irrelevant** 时，才可把 mutation 分类为 `truly path-local`。

此时 MAY 使用：

```text
target-blob optimistic concurrency
+
postcondition verification
```

要求：

- 读取并绑定目标 path/blob 的当前版本；
- unrelated branch movement 对该 path 的 correctness/meaning 确实无影响，并有可解释依据；
- 目标 blob 已变化时 fail closed；
- 写入后核实 path content/blob 与相关 ref/postcondition；
- 一旦发现跨文件、base、parent、ref 或 repository-wide dependency，立即升级为 `base-dependent / coupled`。

不得把所有 Hosted API 写操作都升级成 heavyweight object/CAS flow；真正 path-local 的小改可以保持轻量 optimistic concurrency。

## 6. Commit Candidate：Reference / evidence aid

`Commit Candidate` 从固定 Gate 降级为 **Reference / evidence aid**。

以下情况 SHOULD 形成具体展示：

- 正在请求 action-specific approval；
- 人需要决定 included/excluded scope；
- 存在 material risk、敏感边界或 rollback trade-off；
- 当前证据需要一个可读的 commit decision pack。

已有有效 standing authorization、scope/validation 清晰且没有新的 human decision boundary 时，不得为了每个 checkpoint 机械重复制造低信息审批。

可用格式：

```markdown
## Commit Candidate
- Purpose:
- Included files:
- Explicitly excluded files:
- Sensitive-data check:
- Validation:
- Suggested message:
- Rollback base:
- Authorization:
```

它只是 evidence aid；没有有效 authorization 时不能把它解释为 approval。

## 7. Checkpoint completion semantics

Planning checkpoint、local Git commit 与 remote portable checkpoint 是三个不同概念。

### 7.1 Planning checkpoint

Planning 中记录阶段事实，不自动要求 Git commit，也不代表 Git state 已 portable。

### 7.2 Local commit

当 shared remote 是项目 authority，而 semantic commit 还没有成功 push 时：

```text
LOCAL-ONLY / NOT YET PORTABLE
```

它可以是有价值的 rollback anchor，但不能声明 cross-surface / cross-computer 已可从 shared authority 恢复。

### 7.3 Remote portable completion

当同时满足：

```text
shared remote is project authority
+
commit + push already authorized
+
semantic commit
+
push
+
sufficient postcondition verification
→ checkpoint COMPLETE
```

`sufficient postcondition verification` 至少证明：目标 remote/ref 指向预期 commit，mutation scope 正确，非授权 branch/remote 未改变，必要 validation 仍成立。

如果项目不以 shared remote 为 authority，则由该项目明确 authority contract 定义 portability；不得机械套用 push requirement。

## 8. Mutation 后验证

任何已授权 mutation 后，按 mechanics profile 检查：

### `WORKTREE_GIT`

- branch / HEAD；
- worktree / index；
- committed scope；
- remote tracking / pushed ref（若适用）；
- standing authorization preconditions 是否仍成立。

### `HOSTED_GIT_API`

- expected parent/ref 是否被满足；
- ref transition 是否原子/等价 fail-closed；
- resulting ref / commit / tree / path postcondition；
- coupled unit 是否完整；
- path-local case 是否仍满足“unrelated movement semantically irrelevant”的前提。

对同一已授权 commit/push 动作完成验证后，不应再为了形式重复请求 approval。

## 9. 场景速查

| 场景 | 结果 |
|---|---|
| clean worktree + exact stage + valid standing auth | 可 commit；若 push 同样在 envelope 内则继续 push，无需重复 approval |
| unrelated dirty state | 避开、精确 stage；不得清理用户修改 |
| mixed file changes | hunk/等价精确分离；不能可靠分离则暂停 |
| Hosted API base-dependent，branch 已从 A 移动到 B、target blob 未变 | expected parent/ref 不满足；写入前失败 |
| Hosted API coupled multi-file | atomic or equivalent fail-closed CAS；不得 sequential split write |
| Hosted API truly path-local | target-blob optimistic concurrency + postcondition verification |
| ordinary standing auth 遇到 force push / destructive reset | 授权不足；重新取得明确 protected-action authorization |
| local commit 未 push，而 shared remote 是 authority | `LOCAL-ONLY / NOT YET PORTABLE` |
| semantic commit 已 push 且 remote ref/postconditions 已验证 | `checkpoint COMPLETE` |

## 10. 交叉引用

- 总体 authority / authorization：`core-protocol.md`
- Planning / Session continuity：`planning-and-handoff.md`
- execution-surface handoff / real asset transfer：`portability-and-distribution.md`
- Remote-first active consumer：`docs/operations/remote-first-deployment-controller.md`
- Human-facing conditional projection：`docs/reference/human-work-view-reference.md`

## 11. Source Map

- 架构说明 v0.5：原 Git safety baseline。
- KC-018：Goal-scoped standing authorization 与逐动作批准冲突修复。
- KC-021 Frozen Full Design：Work D Git mechanics / portability / Human Work View design。
- KC-025：authorization/mechanics 分离、Hosted API concurrency、checkpoint completion semantics。
