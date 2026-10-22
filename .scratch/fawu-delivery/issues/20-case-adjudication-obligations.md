# 20: 记录审理结案并继续办理收付及其他履行

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 端到端功能

**What to build:** 用户记录核定审结结果和依据，持续维护应收应付、已收已付、其他履行事项、期限和处理依据；审结仍可未履行。

**Blocked by:** [18 维护程序事实、阶段进度与独立申请状态](18-case-procedure-progress.md)。

**规格覆盖：** C-28～30；TC-13、TC-15。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[案件流程基线](../../fawu-rebuild/product-workflows.md)；[特殊处理基线](../../fawu-rebuild/execution-exceptions.md)。

## Acceptance criteria

- [ ] 金额精度及计算采用核定口径，历史原值不重算。
- [ ] 审结、执行完毕分别表达。
- [ ] 非金额义务和处置不明不被零余额掩盖。

## 执行边界

完成直接依赖并核对事实后实施本用例，验证外部行为、权限及业务成果；真实平台贯通与测试替身结果分别记录。未核定字段或规则先记录缺口，不用猜测补全。不得把本用例完成当作整域、全量历史或正式上线完成。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
