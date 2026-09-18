# 生产追溯（Production Trace）

**版本：v0.1-draft**
**依赖：`core-protocol.md`**

## 1. 目的与范围

本标准把正式生产运行与其输入、设施版本、输出和质量状态绑定，并规定设施变化后的旧成果处理结论。

本标准不规定 Skill 变更审批、Git 操作、Local Bundle 或公开发布清单。

## 2. 开发与生产

1. 开发设施和生产运行 MUST 分开记录。
2. Work Item 说明设施怎样变化；Run Manifest 说明某次生产实际使用了什么。
3. 测试成功不得自动等同于生产成果已验收。
4. 设施变化不得自动使全部旧成果失效；必须逐项判断重跑策略。

## 3. 必须创建 Manifest 的运行

以下运行 MUST 创建 Run Manifest：

- 正式交付；
- 需要以后复现；
- 使用私有数据形成重要成果；
- 可能因设施变化而重跑；
- 批量生产；
- 用于验收新版设施的首次真实运行。

一次性草稿、明确不保留的探索或与生产无关的小测试 MAY 不登记或简化登记。

## 4. Run 标识与位置

1. 每次需记录的生产运行 MUST 有唯一 Run ID，推荐格式为 `RUN-YYYYMMDD-NNN`。
2. Manifest SHOULD 保存于 `production/manifests/<run-id>.yml`。
3. Manifest MUST 绑定可识别的项目 Git commit；未提交热状态不得作为正式可复现版本。

## 5. Manifest 最低内容

Run Manifest MUST 记录：

- Run ID、项目、状态和生产时间；
- 输入逻辑 ID、路径或哈希；
- repository commit；
- 相关合同、软件和 Skill 版本；
- 影响输出质量时的实际模型和配置；
- 输出路径或逻辑 ID，必要时含哈希；
- 质量状态和 Review 指针；
- rebuild policy 及理由。

Host 只有在影响工具、环境或结果时 SHOULD 记录。

## 6. 敏感数据

1. Manifest MUST NOT 包含密钥、凭据或不必要的隐私信息。
2. 真实敏感路径 SHOULD 使用项目相对逻辑 ID 表达。
3. 输入或输出不能进入仓库时，Manifest MUST 保留可验证的本地指针或哈希策略，但不得泄露内容。

## 7. 质量状态

1. 正式交付的 Manifest MUST 指明质量状态。
2. 人工验收（Human Acceptance，仅在适用时）、正式审查（Formal Review）、受保护的独立审查（Protected Independent Review，仅在要求时）和自动测试是不同证据，MUST 分开记录。
3. 被拒绝或待修复的运行不得标记为 accepted。

## 8. 重建策略

设施或合同变化的 Closeout MUST 对既有成果给出以下一个结论：

- `REQUIRED`：旧成果已不再有效或必须重新生产；
- `RECOMMENDED`：旧成果仍可用，但重跑能带来重要修正或一致性；
- `FUTURE_RUNS_ONLY`：仅未来运行采用新设施，旧成果继续有效；
- `NOT_REQUIRED`：变化不影响既有成果。

结论 MUST 说明理由和受影响版本或 Run 范围。不得只写分类而无影响边界。

## 9. 设施变更责任

1. 软件、Skill 或合同变更的 Primary Task Contract MUST 检查生产影响。
2. Closeout MUST 写入 rebuild policy；若为 `REQUIRED`，MUST 指定重跑责任或建立后续 Work Item。
3. Run Manifest 只记录某次运行事实，不得替代设施变更合同或 Closeout。

## 10. 交叉引用

- Work Item、影响和核心记录：`core-protocol.md`
- Skill governance 与 impact：`normative-asset-change-control.md` + `skill-design-principles.md`
- Git 版本门禁：`git-safety.md`
- 生产资产的接续和交付：`portability-and-distribution.md`

## 11. 来源映射

- 架构说明 v0.5：第 12、14～16 节。
- 项目执行规范 v0.1：第 44～46、52～54 节。
- KC-021 Frozen Full Design：Work B Review + Skill Governance consolidation。
