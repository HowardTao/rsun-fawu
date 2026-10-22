# 05: 核实案件历史结构、金额时间及关联样本

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 核验

**What to build:** 取得不同历史时期的案件、子记录、审批和金额时间样本，核定原标识、实际结构、数据语义与迁移异常。

**Blocked by:** [01 核实测试环境、隔离目标与确认职责](01-environment-baseline.md)。

**规格覆盖：** V06；C-43～44；TG-08。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[历史迁移基线](../../fawu-rebuild/historical-migration.md)；[PostgreSQL 适配核对](../../fawu-rebuild/research/postgresql-compatibility-followup.md)。

## Acceptance criteria

- [ ] 实际结构与 DBML 差异有清单。
- [ ] 金额精度、空值、日期时区及原值可解释。
- [ ] 主子/人员/审批关联和原有异常有证据，不仅统计行数。

## 执行边界

本任务交付核验事实和结论，不实现后续业务功能。保留来源、样本、期望/实际、差异及确认职责；缺访问或材料时记录具体缺口，不能把未核实内容当通过。涉及写回的测试仅使用已经明确的可恢复副本或隔离目标。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
