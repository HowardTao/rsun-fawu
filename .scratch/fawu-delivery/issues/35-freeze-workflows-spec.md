# 35: 核定查封冻结完整流程并编写分规格

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)

**工作类型：** 分规格准备

**What to build:** 核对主诉/被诉台账、关联匹配、解封续封、金额期限及提醒，形成完整冻结业务分规格。

**Blocked by:** [01 核实测试环境、隔离目标与确认职责](01-environment-baseline.md)。

**规格覆盖：** V09、V11；G-29～32。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[完整范围清单](../../fawu-rebuild/scope-review.md)；[其余业务代表路径与边界](../../fawu-rebuild/remaining-business-workflows.md)。

## Acceptance criteria

- [ ] 每个有效流程有样本/起止和异常成果。
- [ ] 来源/金额/期限/授权明确。
- [ ] 试点关联能力可复用，未完成全域实现不标验收通过。

## 执行边界

本任务交付相关事实、逐域覆盖记录和分规格，不宣告该业务已实现。保留现行有效流程及已定调整；发现新的取舍或冲突时明确提出。分规格完成后按具体端到端用例继续拆实施任务，未完成核验的规则须列影响及通过条件。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
