# 23: 案件律师委托通过后形成阶段代理关系

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 端到端功能

**What to build:** 从已核定来源选择律师及合同，提交一笔案件委托，在平台通过后形成对应阶段代理关系并从案件查看结果。

**Blocked by:** [09 核定案件关联委托、冻结与联系单的最小契约](09-case-association-contracts.md)；[16 提交固定立项资料并审批通过正式立项](16-case-initiation-approval.md)。

**规格覆盖：** C-37；G-34～37；TC-18。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[关联业务代表路径](../../fawu-rebuild/remaining-business-workflows.md)；[范围清单](../../fawu-rebuild/scope-review.md)。

## Acceptance criteria

- [ ] 选择、材料、申请、通过和代理关系形成贯通。
- [ ] 遵守对应操作范围和委托规则。
- [ ] 重复不重复关系，不把同意当费用结清。
- [ ] 完整合作/费用/评价流程另按分规格展开。

## 执行边界

完成直接依赖并核对事实后实施本用例，验证外部行为、权限及业务成果；真实平台贯通与测试替身结果分别记录。未核定字段或规则先记录缺口，不用猜测补全。不得把本用例完成当作整域、全量历史或正式上线完成。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
