# Source Notes

本仓库案例业务内容均为原创虚构材料。

## 第一次培训参考

课程结构与教学策略主要参考：

- Claude Code for Everyone：连续业务故事、项目目录、单文件提取、文件夹综合、参考模板、视觉与外部研究等教学机制；
- Tencent WorkBuddy 官方高效使用技巧：清晰表达、小步推进、多轮调整、使用参考样例、不同任务分开会话、频繁备份；
- WorkBuddyGuide / WorkBuddy 社区蓝皮书：WorkBuddy 入门任务、工作区与文件型任务组织方式。

不直接翻译、改名或重新分发 `Claude Code for Everyone` 的 Basecamp Coffee 原始课程文本或素材。

## 第二次培训 Skill 方案新增参考

### Carl Vellotti｜Claude Code for Everyone

https://github.com/carlvellotti/claude-code-everyone-course

继续参考：

- 连续业务故事；
- 真实项目目录；
- 先制造痛点再引出新概念；
- 前一步产物成为后一步输入；
- 学习过程本身推动一个真实工作。

不采用其 Terminal、slash command、subagent、GitHub、deploy 等技术内容。

### lhfer｜claude-howto-zh-cn

https://github.com/lhfer/claude-howto-zh-cn

重点参考：

- `03-skills/README.md`
- `03-skills/brand-voice/`
- `03-skills/doc-generator/`

用于理解 Skill 的最小结构、触发说明、非代码型 Skill 和后续 references / templates 的渐进方向。

### debs-obrien｜learn-agent-skills

https://github.com/debs-obrien/learn-agent-skills

重点参考其 README Wizard 教程结构：

- 最小 Skill；
- 逐步完善；
- practice project；
- 真实测试；
- 换项目复用。

第二课只借“做出来 → 测 → 改 → 再测”的教学结构，不直接引入 scripts / eval JSON / CLI / GitHub 分享。

### Anthropic｜skills / skill-creator

https://github.com/anthropics/skills

重点参考其后台方法：

```text
capture intent
→ draft
→ test
→ evaluate
→ revise
→ retest
```

对小白前台不使用 benchmark / assertion / baseline / variance 等术语。

### hamzafarooq｜claude-code-starter

https://github.com/hamzafarooq/claude-code-starter

主要作为业务型 Skill 题材库参考，例如：

- Competitor Research；
- Market Sizing；
- Stakeholder Update；
- Business Case；
- Voice DNA。

不直接采用其 MCP、subagent、部署与 API 教学深度。

## 产品事实边界

第二课真正实施前，WorkBuddy Skill 的：

- 创建入口；
- 项目级路径；
- 触发机制；
- 个人级 / 项目级范围；
- 是否需要重载；
- 当前模型兼容性；

都必须以当时 WorkBuddy 官方文档和实机验证为准。

不要把 Claude Code 的目录和行为直接当作 WorkBuddy 事实。
