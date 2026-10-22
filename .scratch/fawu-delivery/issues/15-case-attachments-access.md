# 15: 新案件材料关联与授权下载预览

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 端到端功能

**What to build:** 经办人在案件中按已核定方式添加和关联新材料，授权人员能够使用平台实际支持的下载及预览。

**Blocked by:** [07 核实附件来源与有效访问契约](07-attachment-contracts.md)；[13 直接登记案件并按范围保存查询](13-case-registration-query.md)。

**规格覆盖：** C-09、C-39；TG-08；TC-03、TC-19。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[历史附件基线](../../fawu-rebuild/historical-migration.md)；[附件静态研究](../../fawu-rebuild/research/preserved-integration-contracts.md)。

## Acceptance criteria

- [ ] 业务记录、附件元数据和实际文件相互对应。
- [ ] 未授权直接访问拒绝。
- [ ] 支持的能力按真实平台验证，不伪造不可用预览。

## 执行边界

完成直接依赖并核对事实后实施本用例，验证外部行为、权限及业务成果；真实平台贯通与测试替身结果分别记录。未核定字段或规则先记录缺口，不用猜测补全。不得把本用例完成当作整域、全量历史或正式上线完成。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
