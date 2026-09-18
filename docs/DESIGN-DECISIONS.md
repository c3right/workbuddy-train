# Design Decisions

## 2026-09-17 — Phase 1 Acceptance

用户已接受以下四项设计建议：

1. 接受“新岚汽车渠道研究”作为第一次培训的连续案例主场景；
2. 接受 Exercise 0～6 的顺序与深度；
3. 接受第一次培训不引入项目级 Skill、CODEBUDDY.md、AGENTS.md 等隐藏能力；
4. 接受“参考样例 → v1 → review → v2”作为第一次培训实操高潮。

因此：

- Phase 1 Design Freeze：**ACCEPTED**；
- Phase 2 Material Build：**AUTHORIZED**。

## 2026-09-17 — L2 Demo Output Decision

用户决定 L2 Demo 最终交付采用：**短研究报告**。

理由：

- 第一次培训核心是建立正确的 Agent 工作方法与策略，而不是展示特定文件格式能力；
- WorkBuddy 的 PPT 生成质量和稳定性尚未在本培训场景中验证；
- 为避免引入与核心教学无关的不可控因素，L2 不生成 PPT；
- L2 应把注意力集中在：任务定义 → Plan → 多资料综合 → 证据边界 → 中间分析 → 短研究报告 → 人工 Review → v2。

因此，Phase 3 制作 `instructor/L2演示脚本.md` 时，无需再等待 PPT / 报告形态裁决，直接按“短研究报告”设计。


## 2026-09-18 — Post-Phase-4 Immersion Decisions

用户明确确认：

1. 学员 Lab 要“做戏做全套”，从 Agent 视角尽量像真实咨询项目，不提前暴露“教学案例 / 虚构数据 / L1 Lab”等培训属性；
2. Exercise 0 不采用“不准读正文、只能看目录”这种不符合真实工作习惯的限制，改用正常的接手项目表达；
3. 示例 Prompt 保留最佳实践所需的任务边界、输入、输出和验收要求，但措辞要像真人交代工作，避免明显“AI 指令稿 / 机器指令腔”；
4. 第一课学员心智地图继续保持简单，不把 Dry Run 验证出的证据升级、Gate、错误传播等深层方法论塞给小白；
5. 课程后台可以更严格，但前台教学保持轻量：**后台方法可以严，前台教学不要重。**

## 2026-09-18 — Second Training Skill Tutorial Proposal

第二课方向暂定为设计候选，不视为已经批准实施：

> **从重复 Prompt → 把稳定工作方法沉淀成自己的第一个 Skill。**

当前推荐：

- 第一个 Skill：访谈材料综合 Skill；
- 继续采用沉浸式项目目录和真实工作故事；
- 通过“普通任务 → 识别重复规则 → 创建 Skill → 试用 → Review → 修改 → 新材料迁移测试”完成学习闭环；
- 不在第二课一开始引入 Git、CLI、subagent、MCP、scripts、eval framework 等技术内容；
- 真正实施前，重新核验 WorkBuddy 当前 Skill 的创建入口、目录约定、触发机制和模型兼容性。

详细方案见：`docs/SECOND-TRAINING-SKILL-TUTORIAL-DESIGN.md`。
