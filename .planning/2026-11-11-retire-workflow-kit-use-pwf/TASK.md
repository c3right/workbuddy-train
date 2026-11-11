# 移除 Workflow Kit，改用 PWF

- 确认：2026-11-11，用户要求本项目不再部署 Workflow Kit，移除当前部署，改用 Planning with Files（PWF），并在 `AGENTS.md` 明确共享规则。
- 基线：`main` / `b920d80823303d3f69dbb04e346b8ef2df55b477`。
- 范围：退役本仓库的 Kit 安装及入口；迁移历史治理记录；停止 WBT-AWK-002 升级路线；建立 `.planning/` 任务导航和跨 Agent、跨会话、跨远端/电脑端接续规则。
- 发布授权：2026-11-11，用户明确要求仅将本次切换提交并推送到 `origin/main`，并回报提交 SHA。
- 不在范围：修改 `training/` 或启动后续课程工作，变更用户级技能/钩子，修改其他远端分支、合并或改写历史。
- 验收：不再有活动 Kit 安装或并行状态入口；任务可从 `AGENTS.md` 与 `.planning/README.md` 定位，PWF 原生解析及计划检查通过；培训产品内容不变，旧安装及升级决定可查。
