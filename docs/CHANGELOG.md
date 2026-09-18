# Changelog

## 2026-09-18

### Documentation Consolidation
- 新增 `docs/FIRST-TRAINING-DESIGN-IMPLEMENTATION-HISTORY.md`，把第一次培训从需求形成、参考来源、案例选择、Exercise 设计、Phase 1—4、Dry Run、Immersion Pass、PNG 修复到当前不应回退的设计基线完整落盘。
- 新增 `docs/SECOND-TRAINING-SKILL-TUTORIAL-DESIGN.md`，详细记录“从重复 Prompt 到自己的第一个 Skill”的第二课候选方案。
- 第二课当前状态明确为 **DESIGN PROPOSAL / NOT YET IMPLEMENTED**，后续会话可据此继续 Design Freeze、素材制作、学员包、讲师包和 Dry Run。
- 第二课推荐首个 Skill 为“访谈材料综合 Skill”，主线为：普通任务 → 识别重复规则 → 创建 Skill → 试用 → Review → 修改 → 新材料迁移测试。
- 记录后续可参考的公开项目：`carlvellotti/claude-code-everyone-course`、`lhfer/claude-howto-zh-cn`、`debs-obrien/learn-agent-skills`、Anthropic `skills/skill-creator`、`hamzafarooq/claude-code-starter`。
- README 增加“新会话建议先读”与第二期候选状态，目标是让未来会话无需重新翻聊天记录即可恢复项目脉络。

### Binary Asset Repair
- 修复 `区域经营指标截图.png` 远端二进制损坏问题。
- 修复后正常 Git blob SHA：`223889a30ca67acfe1cbb89898f9c4c972de5415`。
- 修复 commit：`c2d16d0fe0b7f05f0f0ef16bd0f53c81b265394c`。
- 后续二进制培训素材正式分发前应增加“实际下载后可打开”的完整性检查。

## 2026-09-17

### Phase 1
- 新增 `WORKBUDDY-L1-LAB-DESIGN.md` Full Design V0.1。
- 用户接受 Design Acceptance Questions 1—4。
- L2 Demo 交付形态后续裁决为“短研究报告”。

### Phase 2
- 完成“新岚汽车渠道研究项目”原创教学素材。
- 完成 3 份项目背景 / 口径材料。
- 完成项目交接记录。
- 完成华东、华南、西南、华北 4 份区域访谈。
- 完成 `区域渠道经营快照.xlsx`，含门店样本、区域汇总、口径说明。
- 完成 `区域经营指标截图.png`。
- 完成并视觉校验 `优秀内部项目简报样例.docx`。
- Phase 2 标记为 REVIEW READY。

### Phase 3
- 完成 `training/learner/第一次培训实操手册.md`：Exercise 0—6 全员逐步跟做脚本。
- 完成 `training/learner/L1通关卡.md`：L1 最低能力与心智模型验收。
- 完成 `training/instructor/讲师手册.md`：培训节奏、教学控制点、各 Exercise 讲解重点。
- 完成 `training/instructor/标准事实与验收表.md`：项目事实边界、四区预期发现、图片分析与 L2 判断基准。
- 完成 `training/instructor/L2演示脚本.md`：Plan → 证据矩阵 → 人工 Gate → 短研究报告 v1 → Review → v2。
- L2 明确不生成 PPT；演示重点收敛到 Agent 任务规划、证据控制和人工验收。
- 新增 `training/instructor/reset/README.md`，定义无需 Git 的现场恢复方式。
- Phase 3 标记为 COMPLETE / REVIEW READY。

### Phase 4
- 使用 Tencent WorkBuddy + `hy4 preview` 完整实跑 L1 Exercise 0—6 与 L2 Step 1—6。
- 结论：`PASS WITH LIGHTWEIGHT REVISIONS`。
- 新增 `docs/PHASE-4-DRY-RUN-20260917.md`，记录完整运行观察与裁决。
- 学员手册增加“新入职研究员接手项目”的破冰故事。
- Exercise 3 增加“保留同一区域内部不同说法”的提醒。
- Exercise 5 增加“不要把少数人观点升级成区域/跨区共性”的检查项。
- L2 Plan 增加明确停止边界，避免计划通过后直接进入后续执行。
- L2 人工 Gate 增加“少数观点被放大”“证据不足被误写成否定结论”两项检查。
- L2 v2 修改提示改为“看是否有下面的问题，如有则修订”，减少诱导式修订。
- 报告字数规则调整为快速阅读导向：正文尽量 1200—1800 字，必要比较表可保留。
- 讲师手册新增“不要针对某个模型过度补 Prompt”的后台教学原则。

### Post-Phase-4 Immersion Pass
- 学员实际工作目录由 `WorkBuddy-L1-Lab` 改名为 `新岚汽车渠道研究项目`，避免目录名直接暴露培训属性。
- 撤销 Exercise 0 的“只看目录、不读正文”式非自然限制，改为真实接手项目时会说的“先帮我看看这个项目大概是什么情况”。
- 将 Lab 内部的“教学用虚构材料”“本次培训”“学员”等培训口吻移出工作目录；虚构与版权说明只保留在 Lab 外部治理文档中。
- 重制 Excel 口径说明、区域指标图片和历史项目简报样例，清除可见的“教学/虚构/WorkBuddy L1”标记，使 Lab 从 Agent 视角更像一个真实项目目录。
- 对 L1 Exercise 0—6 与 L2 Step 1—6 的示例提示词做自然语言化处理：保留最佳实践中的任务边界、输入、输出和验收要求，但改成更接近真实同事交代工作的表达方式。
- 讲师侧明确：最佳实践不等于“机器指令腔”；学员要学的是把工作说清楚，而不是模仿固定 Prompt 模板。

### Current
- Phase 1—4 均已完成第一轮。
- 当前第一期培训包已进入 **POST-DRY-RUN REVIEW READY** 状态。
