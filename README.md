# WorkBuddy Train

面向非技术同事的 WorkBuddy 实操培训项目。

## 当前目标

第一期培训只聚焦两件事：

1. **认知重塑**：从“网页聊天”迁移到“围绕真实工作目录持续做事的 Agent”。
2. **L1 工具跑起来**：让学员亲手完成一次“理解资料 → 执行任务 → 生成文件 → 检查 → 修改”的完整闭环。

L2“单项任务做出来”在第一期仅由讲师演示，不要求全员现场达成。

## 当前状态

- Phase 1 — Full Design：**ACCEPTED**
- Phase 2 — Material Build：**COMPLETE / REVIEW READY**
- Phase 3 — Learning Pack：**COMPLETE / REVIEW READY**
- Phase 4 — Dry Run / Validation：**COMPLETE / PASS WITH LIGHTWEIGHT REVISIONS**

当前培训包状态：**POST-DRY-RUN REVIEW READY**。

L2 Demo 已确定采用：**短研究报告**。不生成 PPT，不加入外部 Web 搜索，不引入 Skill、Connector、subagent、CLI、Git 或开发环境配置。

## 建议审阅顺序

1. [学员第一次培训实操手册](learner/第一次培训实操手册.md)
2. [L1 通关卡](learner/L1通关卡.md)
3. [讲师手册](instructor/讲师手册.md)
4. [标准事实与验收表](instructor/标准事实与验收表.md)
5. [L2 短研究报告演示脚本](instructor/L2演示脚本.md)
6. [Phase 4 Dry Run 记录](docs/PHASE-4-DRY-RUN-20260917.md)

## 关键位置

- [WorkBuddy L1 Lab — Full Design V0.1](docs/WORKBUDDY-L1-LAB-DESIGN.md)
- [Design Decisions](docs/DESIGN-DECISIONS.md)
- [Source Notes](docs/SOURCE-NOTES.md)
- [Phase 4 Dry Run](docs/PHASE-4-DRY-RUN-20260917.md)
- [Changelog](docs/CHANGELOG.md)
- [学员项目目录](lab/新岚汽车渠道研究项目/)
- [Lab Reset 说明](instructor/reset/README.md)

## 学员项目目录

`lab/新岚汽车渠道研究项目/` 是学员在 WorkBuddy 中直接打开的工作目录。

目录内部按一个真实咨询项目的口吻组织，不放“培训案例”“虚构数据”“L1 Lab”之类会破坏代入感的提示。培训属性、版权和案例虚构说明只保留在项目目录之外的本仓库文档中。

项目目录已经包含：

- 项目背景与研究边界；
- 项目交接记录；
- 华东、华南、西南、华北四份区域访谈；
- 基础经营数据 Excel；
- 区域经营指标视觉材料；
- 与主案例业务不同的历史项目内部简报参考样例；
- 输出目录说明。

所有案例业务内容、人物与数据均为原创虚构教学材料。

## 第一期核心心智模型

```text
先选对工作目录
→ 先让 Agent 看懂资料
→ 把大工作拆成小步骤
→ 说清楚：做什么 / 有什么 / 怎么样
→ 必要时给参考样例
→ 让 Agent 真正生成 / 修改文件
→ 人检查事实、逻辑和证据边界
→ 具体反馈，继续修改
→ 重要成果保留 v1 / v2
→ 明显换任务时，新建 Task
```

这张心智地图保持简单。Phase 4 中验证出来的更深层质量控制方法主要进入讲师手册和 L2 Demo，不增加第一次培训学员的认知负担。

## 设计来源

本项目参考：

- Carl Vellotti 的 `Claude Code for Everyone` 的“单一连续业务场景 + 项目目录 + 逐步实操”教学机制；
- Tencent WorkBuddy 官方《高效使用技巧》中“清晰表达、小步快跑、多轮调整、给参考样例、不同任务分会话、备份/版本管理”等原则；
- WorkBuddyGuide / workbuddy.homes 的入门任务设计。

> 说明：本项目不会复制或翻译 `Claude Code for Everyone` 的原始案例文本和素材。考虑其公开页面标注的 CC BY-NC-ND 4.0，本项目只借鉴教学结构与机制，案例内容全部重新原创并中文化。
