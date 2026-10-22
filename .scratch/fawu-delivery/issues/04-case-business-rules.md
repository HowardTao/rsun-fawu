# 04: 核定案件字段、状态、参与关系及履行规则

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 核验

**What to build:** 把案件分规格中待核实的编号/必填、固定提交资料、程序事实、审结、收付和其他义务、关闭及更正字段补成有来源的业务契约。

**Blocked by:** [01 核实测试环境、隔离目标与确认职责](01-environment-baseline.md)。

**规格覆盖：** V09～V10；C-01～44。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[案件流程基线](../../fawu-rebuild/product-workflows.md)；[特殊处理基线](../../fawu-rebuild/execution-exceptions.md)。

## Acceptance criteria

- [ ] 有字段及操作前提/合法转换矩阵。
- [ ] 三类状态独立、审结与履行分开。
- [ ] 特殊标签不自动办结，业务确认有效规则与代表样本。

## 执行边界

本任务交付核验事实和结论，不实现后续业务功能。保留来源、样本、期望/实际、差异及确认职责；缺访问或材料时记录具体缺口，不能把未核实内容当通过。涉及写回的测试仅使用已经明确的可恢复副本或隔离目标。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
