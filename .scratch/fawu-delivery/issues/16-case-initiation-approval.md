# 16: 提交固定立项资料并审批通过正式立项

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 端到端功能

**What to build:** 新法务从案件提交核定立项资料和材料，记录本次提交与实例；审批在既有平台办理，通过后正式立项并可查看结果历史及跳转。

**Blocked by:** [03 核实案件审批及旧在途的真实契约](03-approval-inflight-contract.md)；[15 新案件材料关联与授权下载预览](15-case-attachments-access.md)。

**规格覆盖：** C-07～10、C-16～18；TC-04、TC-08。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[集成静态研究](../../fawu-rebuild/research/preserved-integration-contracts.md)；[身份审批决定](../../fawu-rebuild/issues/08-identity-approval-contract-decision.md)；[历史过渡基线](../../fawu-rebuild/historical-migration.md)。

## Acceptance criteria

- [ ] 缺主责/必填或权限拒绝不产生外部申请。
- [ ] 审批期间固定该次资料。
- [ ] 有效通过只产生一次核定立项成果，不虚构法院程序，受理不明先保留待确认且禁止盲目重发。

## 执行边界

完成直接依赖并核对事实后实施本用例，验证外部行为、权限及业务成果；真实平台贯通与测试替身结果分别记录。未核定字段或规则先记录缺口，不用猜测补全。不得把本用例完成当作整域、全量历史或正式上线完成。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
