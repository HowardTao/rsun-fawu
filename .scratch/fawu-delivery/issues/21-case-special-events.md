# 21: 记录特殊事件并保留未办结跟进

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 端到端功能

**What to build:** 主责按有效人工记录维护和解、中止、特殊结案等事件、依据和材料，义务未处理完毕时继续跟进。

**Blocked by:** [20 记录审理结案并继续办理收付及其他履行](20-case-adjudication-obligations.md)。

**规格覆盖：** C-34～36；TC-16。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[案件流程基线](../../fawu-rebuild/product-workflows.md)；[特殊处理基线](../../fawu-rebuild/execution-exceptions.md)。

## Acceptance criteria

- [ ] 界面保存和结果查询可追溯。
- [ ] 记录事件不自动减额、完成履行或关闭。
- [ ] 沿核定的既有审批控制，不追加自动核销或例外关闭。

## 执行边界

完成直接依赖并核对事实后实施本用例，验证外部行为、权限及业务成果；真实平台贯通与测试替身结果分别记录。未核定字段或规则先记录缺口，不用猜测补全。不得把本用例完成当作整域、全量历史或正式上线完成。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
