# Runtime Capabilities

This Project Owned snapshot records capabilities actually evidenced during the current onboarding work. It does not grant authorization and does not bind future CTRL, IMPL or REVIEW roles to a specific host or model.

- Last Verified：`2026-09-18`
- Verified By：`WBT-AWK-001-T02 remote implementation session`
- Project：`WorkBuddy Train`

## 1. 使用规则

1. 只有需要选择 Host、模型、Provider 或 subagent 方式时才读取本文件。
2. 记录当前已验证能力；没有证据的能力保持 `UNKNOWN` 或 `NOT_ASSUMED`。
3. Runtime 事实不创建 Git、文件写入、联网、生产或发布授权。
4. Profile 只表示长期 capability availability，不表示所有专业 Module 当前激活。

## 2. 当前能力

| Host | Provider | Available Models | Subagent Capability | Workspace Access | Network / Tools | Typical Use | Constraints | Last Verified |
|---|---|---|---|---|---|---|---|---|
| ChatGPT | OpenAI | GPT-5.6 Sol | NOT_ASSUMED | Remote repository read/write through authorized GitHub connector | GitHub repository tools available | Bounded repository implementation and review support | Local shell in this session cannot resolve `github.com`; canonical installation validator cannot materialize the two repositories here | 2026-09-18 |

## 3. 当前默认映射

- Routine implementation：`capability-dependent / current authorized session when sufficient`
- Expert implementation：`PENDING`
- Formal review：`separate authorized review context when required by contract`
- Read-only exploration：`current authorized session when sufficient`
- Cross-provider subagent：`NOT_ASSUMED`
- Formal review fallback：`separate session / PENDING`

## 4. 已验证的限制

- 当前 shell 环境无法解析 `github.com`，因此不能在本 session 中通过 clone/mount 方式运行 canonical `scripts/validate_installation.py`。
- Cross-provider subagent capability 未验证。
- WorkBuddy 产品运行时能力不由本次 Kit onboarding 验证。

## 5. 刷新触发

Host、模型、工具权限、网络能力、subagent 能力或实际 Work 依赖的运行事实发生变化时更新。

## 6. 与 Work 的关系

当前 Work 的授权和边界以 Primary Task Contract 为准；本文件只提供运行能力证据。
