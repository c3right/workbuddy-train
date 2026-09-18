# README 与使用导航维护

本文件规定项目根 `README.md` 和 `docs/README.md` 的创建、合并和持续维护。它是 Project Owned Operations，不替代 Primary Task Contract、项目 `AGENTS.md`、已安装 standards 或用户授权。

## 目标与入口

项目入口面最少回答：项目做什么、怎样开始、主要目录／文档在哪里、当前成熟度和限制是什么、Agent 下一步应读什么。

- 根 `README.md`：公共定位、快速开始、稳定结构和使用入口；
- `docs/README.md`：文档树一级导航；
- Source Map：README 章节到权威来源和刷新触发器的映射。

## 事实源

| 动态事实 | 默认权威来源 |
|---|---|
| 版本／发布 | `VERSION`、发布配置或项目等价文件 |
| 重要变化 | `CHANGELOG.md`、Release Notes 或等价文件 |
| 当前 Work | `agents/WORK_INDEX.md` |
| 当前合同与状态 | Primary Task Contract、Planning、Review、Closeout |
| 安装来源与 Profile | `.workflow-kit.yml` |
| 运行环境 | `docs/operations/runtime-capabilities.md` |
| 目录与入口 | 实际文件树、项目规则和正式架构／操作文档 |

README 优先链接这些来源，不复制完整状态和历史。

## 自动区块

允许自动刷新的内容必须放在成对标记之间：

```markdown
<!-- AWK:AUTO:PROJECT_STATUS:BEGIN -->
自动刷新内容
<!-- AWK:AUTO:PROJECT_STATUS:END -->
```

规则：

1. 同一文件内 `BLOCK_ID` 唯一；
2. 自动刷新只允许修改标记内内容；
3. 不得删除或重写标记外人工内容；
4. 标记缺失、重复、嵌套错误或来源冲突时停止并返回 CTRL；
5. 自动区块必须进入 diff、Review 和 Git 用户门禁；
6. 自动区块保持短小，保存摘要和权威链接，不复制完整历史。

## Work Entry 影响检查

新正式 Work 进入 IMPL 前填写：

```text
README / Navigation Impact: NONE | AUTO_REFRESH | STRUCTURAL_REFRESH
Entry Surface Files:
Source Map Impact:
```

### `NONE`

仅当 Work 不影响项目定位、核心能力、安装／使用、一级目录、主要文档、Profile／外部工具入口、版本／成熟度、License 或推荐阅读路径时使用。

### `AUTO_REFRESH`

只需要根据明确来源刷新标记内摘要，例如版本、成熟度、当前 Work 指针和文档入口列表。

### `STRUCTURAL_REFRESH`

需要修改标记外章节、使用说明、目录职责或 Source Map。CTRL 必须判断该变化是否已在合同内、可作为附属 LIGHT，或需要独立 Work。

## 自动触发事件

以下事件发生时，Agent 必须主动执行入口面检查：

- 版本、Release、成熟度或公开状态变化；
- 核心能力、命令、服务或入口新增／移除／重命名；
- 安装、初始化、配置或使用步骤变化；
- 一级目录、主要文档或架构职责变化；
- Profile、Kit 接入、External Managed 或 Runtime 入口变化；
- License、分发方式或安全边界变化；
- Review 发现 README 与实际项目不一致；
- Closeout 形成长期有效的新入口或限制。

## Review／Closeout 门禁

进入正式 Review 或 Closeout 前检查：

- [ ] Work Entry 影响分类仍有效；
- [ ] 受影响入口面文件已列出；
- [ ] 自动标记成对且没有越界修改；
- [ ] 摘要与权威来源一致；
- [ ] 主要文档新增／移动／删除已反映在 `docs/README.md`；
- [ ] Source Map 已更新；
- [ ] 内部链接存在；
- [ ] 功能、成熟度、安全和许可没有被夸大；
- [ ] diff 已展示，Git 动作仍等待用户授权。

Closeout 记录：

```text
README / Navigation Freshness: PASS | N/A | BLOCKED
Updated Entry Surfaces: <paths or NONE>
Source Map Updated: YES | NO | N/A
```

应更新但超出授权时，不得填写 `PASS`；返回 CTRL 扩展范围或建立后续 Work。

## 接入时 create-or-merge

### 没有 README

- 从 Kit common `README.md` 创建；
- 替换占位符，删除不适用章节；
- 保留快速入口、目录、成熟度、Source Map 和维护链接；
- 创建 `docs/README.md` 并验证链接和标记。

### 已有 README

- 先识别原 README 的读者、产品说明和权威内容；
- 建立保留／合并／新增矩阵；
- 不得用 Kit 模板整篇覆盖；
- 只给适合自动维护的摘要增加 `AWK:AUTO` 标记；
- 补足 Agent 导航、成熟度边界、目录职责和 Source Map。

如果项目已有 MkDocs、Docusaurus、`docs/index.md` 等导航，保留现有体系，在 Source Map 记录实际入口，不创建竞争性导航。

## 停止条件

出现以下情况时停止受影响更新：权威来源冲突、自动标记损坏、命令或链接有效性不明、需要删除项目原有说明、改变公开承诺／License／安全声明、扩大 Work 范围、或没有目标项目写入授权。

## 自动化边界

当前“自动”是 Work 生命周期内的 Agent 触发，不是后台任务、Git Hook 或自动提交。未来 Doctor／CI 可只读检查标记配对、Source Map、链接和来源一致性；未来更新工具默认只能生成 preview 或修改标记内区块。