# 24: 案件关联冻结账户或资产并查看台账结果

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 端到端功能

**What to build:** 按已核定用例关联实际冻结账户或资产，从案件查看正确冻结/解封金额、期限及归属台账。

**Blocked by:** [09 核定案件关联委托、冻结与联系单的最小契约](09-case-association-contracts.md)；[13 直接登记案件并按范围保存查询](13-case-registration-query.md)。

**规格覆盖：** C-38；G-29～30；TC-18。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[关联业务代表路径](../../fawu-rebuild/remaining-business-workflows.md)；[范围清单](../../fawu-rebuild/scope-review.md)。

## Acceptance criteria

- [ ] 关联保存和授权详情贯通。
- [ ] 金额/期限由所属模块解释且有真实样本。
- [ ] 无权限不查询或修改关联，完整续封等流程不由本任务宣称完成。

## 执行边界

完成直接依赖并核对事实后实施本用例，验证外部行为、权限及业务成果；真实平台贯通与测试替身结果分别记录。未核定字段或规则先记录缺口，不用猜测补全。不得把本用例完成当作整域、全量历史或正式上线完成。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
