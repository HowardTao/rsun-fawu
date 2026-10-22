# 08: 核实有效后台作业及案件通知提醒规则

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 核验

**What to build:** 盘点实际运行作业，明确案件试点必须保留的消息、期限提醒、日历和运行归属。

**Blocked by:** [01 核实测试环境、隔离目标与确认职责](01-environment-baseline.md)。

**规格覆盖：** V08；G-70～71。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[后台静态研究](../../fawu-rebuild/research/preserved-integration-contracts.md)；[有效流程基线](../../fawu-rebuild/remaining-business-workflows.md)。

## Acceptance criteria

- [ ] 有实际账号/参数/调度/最近结果。
- [ ] 案件必需事件、接收人和期限规则经确认。
- [ ] 旧新停启和重复处理可验证，不凭分派或注释启停。

## 执行边界

本任务交付核验事实和结论，不实现后续业务功能。保留来源、样本、期望/实际、差异及确认职责；缺访问或材料时记录具体缺口，不能把未核实内容当通过。涉及写回的测试仅使用已经明确的可恢复副本或隔离目标。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
