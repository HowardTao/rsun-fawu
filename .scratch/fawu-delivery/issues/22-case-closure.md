# 22: 核对履行并授权关闭案件

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 端到端功能

**What to build:** 具有关闭操作及相应范围的人员根据当前审结和全部履行处置结果核对，记录理由依据后确认关闭。

**Blocked by:** [20 记录审理结案并继续办理收付及其他履行](20-case-adjudication-obligations.md)。

**规格覆盖：** C-31～33、C-36；TC-14～17。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[案件流程基线](../../fawu-rebuild/product-workflows.md)；[特殊处理基线](../../fawu-rebuild/execution-exceptions.md)。

## Acceptance criteria

- [ ] 未处理金额/其他义务/处置不明均拒绝。
- [ ] 无需执行者审结后核对办结。
- [ ] 过期页面或并发改变不能非法关闭，留处理人/时间且不新增正常关闭审批。

## 执行边界

完成直接依赖并核对事实后实施本用例，验证外部行为、权限及业务成果；真实平台贯通与测试替身结果分别记录。未核定字段或规则先记录缺口，不用猜测补全。不得把本用例完成当作整域、全量历史或正式上线完成。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
