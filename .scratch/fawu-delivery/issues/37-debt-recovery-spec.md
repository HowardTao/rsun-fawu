# 37: 核定清欠与明源闭环并编写分规格

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)

**工作类型：** 分规格准备

**What to build:** 核实接收/变更/退回/移交/解决/退房有效流程、明源契约及部分成功恢复，形成清欠分规格。

**Blocked by:** [01 核实测试环境、隔离目标与确认职责](01-environment-baseline.md)。

**规格覆盖：** V04～V05、V09、V11；G-38～41。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[完整范围清单](../../fawu-rebuild/scope-review.md)；[其余业务代表路径与边界](../../fawu-rebuild/remaining-business-workflows.md)。

## Acceptance criteria

- [ ] 两端一致才完成写入，单边/不明保留结果及核对入口。
- [ ] 每条路径实际前提与成果有样本。
- [ ] 不默认分布式事务或新增消息平台。

## 执行边界

本任务交付相关事实、逐域覆盖记录和分规格，不宣告该业务已实现。保留现行有效流程及已定调整；发现新的取舍或冲突时明确提出。分规格完成后按具体端到端用例继续拆实施任务，未完成核验的规则须列影响及通过条件。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
