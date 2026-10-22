# 27: 历史案件小样迁入 PostgreSQL 并统一查询

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 端到端功能

**What to build:** 把核定的不同历史时期案件及其主子、人员、审批和履行小样导入目标库，通过新系统授权查询原标识及关联结果。

**Blocked by:** [20 记录审理结案并继续办理收付及其他履行](20-case-adjudication-obligations.md)。

**规格覆盖：** C-43；TC-21、TC-23；TG-08。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[历史迁移与过渡基线](../../fawu-rebuild/historical-migration.md)。

## Acceptance criteria

- [ ] 有可复核的映射与隔离迁移结果。
- [ ] 金额时间状态和关联逐项对账，不只行数。
- [ ] 异常保原值并跟踪，不宣称已完成全历史迁移。

## 执行边界

完成直接依赖并核对事实后实施本用例，验证外部行为、权限及业务成果；真实平台贯通与测试替身结果分别记录。未核定字段或规则先记录缺口，不用猜测补全。不得把本用例完成当作整域、全量历史或正式上线完成。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
