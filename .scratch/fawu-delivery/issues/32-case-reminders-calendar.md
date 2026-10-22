# 32: 案件期限提醒与日历贯通

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 端到端功能

**What to build:** 根据核定的案件开庭/履行等实际启用规则运行必要提醒和日历能力，责任人员能查看或接收对应结果。

**Blocked by:** [08 核实有效后台作业及案件通知提醒规则](08-jobs-notifications-baseline.md)；[20 记录审理结案并继续办理收付及其他履行](20-case-adjudication-obligations.md)。

**规格覆盖：** G-70～71；C-46；TG-10。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[后台静态研究](../../fawu-rebuild/research/preserved-integration-contracts.md)；[有效流程基线](../../fawu-rebuild/remaining-business-workflows.md)。

## Acceptance criteria

- [ ] 基于实际启用清单及业务日期/规则运行。
- [ ] 时间边界和接收范围有样例。
- [ ] 任务接管、重复运行和隔离发送可验证，不凭旧命令分支定义需求。

## 执行边界

完成直接依赖并核对事实后实施本用例，验证外部行为、权限及业务成果；真实平台贯通与测试替身结果分别记录。未核定字段或规则先记录缺口，不用猜测补全。不得把本用例完成当作整域、全量历史或正式上线完成。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
