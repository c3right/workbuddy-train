# 发现记录

- 工作编号（Work ID）：`WBT-AWK-001`
- 主合同（Primary Task Contract）：`docs/changes/WBT-AWK-001-workflow-kit-onboarding.md`
- 更新日期：`2026-09-18`

## 开放 Finding

无。

## 已关闭 Finding

### F-T02-ENV-001 — Canonical installation validator execution unavailable in remote shell

- Final Status：`CLOSED`
- Scope：validation evidence only
- Prior condition：remote shell 无法同时 materialize target repository 与固定 Kit source。
- Resolution：在 computer-side/local 环境对 target `77c9f751922f346e1719628de2cc72848f9e5309` 与 Kit source `9abc9b97d305432a589cf55923192378854ef283` 运行 canonical read-only validator。
- Result：`PASS_WITH_WARNINGS`
- Exit code：`0`
- Errors：`0`
- Warnings：`1`
- Warning：`MERGE_HISTORY_NOT_FULLY_VERIFIABLE` — no merge baseline; arbitrary historical prose preservation cannot be proven。
- CTRL disposition：non-blocking evidence limitation；installation integrity 未发现 Error。

## 待决定事项

是否授权 default-branch integration。

## 历史入口

- T01 accepted object：`8540d9febc9817c6a7af64df0192a06b3012d37a`
- T02 implementation object：`7932827ae506e1ab92819dc8a265d317c7c5d1c0`
- T03 validated target：`77c9f751922f346e1719628de2cc72848f9e5309`
