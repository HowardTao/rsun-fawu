# 03: 核实案件审批及旧在途的真实契约

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 核验

**What to build:** 核定立项和试点相关申请的发起、回传、历史、退回/撤回/终止、实例查询和旧表单依赖，明确受理不明及重传时可用的核对手段。

**Blocked by:** [01 核实测试环境、隔离目标与确认职责](01-environment-baseline.md)。

**规格覆盖：** V04～V05；C-07～23、C-40～42。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[集成静态研究](../../fawu-rebuild/research/preserved-integration-contracts.md)；[身份审批决定](../../fawu-rebuild/issues/08-identity-approval-contract-decision.md)；[历史过渡基线](../../fawu-rebuild/historical-migration.md)。

## Acceptance criteria

- [ ] 记录实际提交/回执/回传及来源/确认规则。
- [ ] 同案补正的实例关系明确。
- [ ] 旧在途唯一原链、必要写入和退出证据可识别，不实施生产切换。

## 执行边界

本任务交付核验事实和结论，不实现后续业务功能。保留来源、样本、期望/实际、差异及确认职责；缺访问或材料时记录具体缺口，不能把未核实内容当通过。涉及写回的测试仅使用已经明确的可恢复副本或隔离目标。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
