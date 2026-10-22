# 28: 历史附件分来源恢复授权访问

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 端到端功能

**What to build:** 为迁入的代表历史案件恢复 OA、uploadLite、本地等实际来源材料的有效访问，案件记录、元数据与内容可对账。

**Blocked by:** [27 历史案件小样迁入 PostgreSQL 并统一查询](27-historical-case-sample-migration.md)。

**规格覆盖：** C-39、C-43；TC-19、TC-21。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[历史附件基线](../../fawu-rebuild/historical-migration.md)；[附件静态研究](../../fawu-rebuild/research/preserved-integration-contracts.md)。

## Acceptance criteria

- [ ] 各实际来源分别有访问及关联证据。
- [ ] 缺失/过期/不支持预览留说明。
- [ ] 未授权请求拒绝，潜在写回预览只在隔离副本验证。

## 执行边界

完成直接依赖并核对事实后实施本用例，验证外部行为、权限及业务成果；真实平台贯通与测试替身结果分别记录。未核定字段或规则先记录缺口，不用猜测补全。不得把本用例完成当作整域、全量历史或正式上线完成。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
