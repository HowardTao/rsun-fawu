# 17: 同案退回补正重提与合法终止

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 端到端功能

**What to build:** 用户经平台支持的退回/撤回后在同一案件补正重提，原提交及各次历史可查；不再继续时按核定规则保留并标记终止。

**Blocked by:** [16 提交固定立项资料并审批通过正式立项](16-case-initiation-approval.md)。

**规格覆盖：** C-11～14；TC-05、TC-07。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[集成静态研究](../../fawu-rebuild/research/preserved-integration-contracts.md)；[身份审批决定](../../fawu-rebuild/issues/08-identity-approval-contract-decision.md)；[历史过渡基线](../../fawu-rebuild/historical-migration.md)。

## Acceptance criteria

- [ ] 审批中不能替换原提交。
- [ ] 重提与原平台实例关系按实测契约处理。
- [ ] 终止不删除历史、不误标正式立项，不虚报平台已经取消。

## 执行边界

完成直接依赖并核对事实后实施本用例，验证外部行为、权限及业务成果；真实平台贯通与测试替身结果分别记录。未核定字段或规则先记录缺口，不用猜测补全。不得把本用例完成当作整域、全量历史或正式上线完成。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
