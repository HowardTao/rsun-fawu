# 29: 已办结历史只读与专门授权更正

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 端到端功能

**What to build:** 已确认办结历史默认只读，专门授权人员按核定字段更正并查看完整留痕。

**Blocked by:** [27 历史案件小样迁入 PostgreSQL 并统一查询](27-historical-case-sample-migration.md)。

**规格覆盖：** C-44；TC-22。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[历史迁移与过渡基线](../../fawu-rebuild/historical-migration.md)。

## Acceptance criteria

- [ ] 普通编辑拒绝。
- [ ] 留理由、原值、新值、处理人和时间。
- [ ] 更正不重开、不触发历史审批、不改写原身份归属。

## 执行边界

完成直接依赖并核对事实后实施本用例，验证外部行为、权限及业务成果；真实平台贯通与测试替身结果分别记录。未核定字段或规则先记录缺口，不用猜测补全。不得把本用例完成当作整域、全量历史或正式上线完成。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
