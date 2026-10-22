# 31: 案件关键通知发送与防重复恢复

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 端到端功能

**What to build:** 实现核定的案件关键事件通知，真实测试渠道或隔离接收目标可观察结果，部分失败可恢复且不无意重复发送。

**Blocked by:** [08 核实有效后台作业及案件通知提醒规则](08-jobs-notifications-baseline.md)；[19 受理不明核对及重复迟到结果恢复](19-approval-results-recovery.md)。

**规格覆盖：** C-18、C-46；G-70～71；TC-08；TG-10。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[后台静态研究](../../fawu-rebuild/research/preserved-integration-contracts.md)；[有效流程基线](../../fawu-rebuild/remaining-business-workflows.md)。

## Acceptance criteria

- [ ] 接收人和内容按有效规则。
- [ ] 业务成功与发送结果可核对。
- [ ] 重复回传/恢复不重复必要通知，旧新执行归属有记录，不新增渠道。

## 执行边界

完成直接依赖并核对事实后实施本用例，验证外部行为、权限及业务成果；真实平台贯通与测试替身结果分别记录。未核定字段或规则先记录缺口，不用猜测补全。不得把本用例完成当作整域、全量历史或正式上线完成。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
