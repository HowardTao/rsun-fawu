# 法务重建首批任务索引

发布日期：2026-10-22。用户已确认 46 项拆分；正式任务每项一个文件，编号与阻塞关系遵循已批准草稿。当前任务均已发布，未执行。

来源：[重建总规格](../fawu-rebuild/spec.md)、[案件分规格](../case-lifecycle/spec.md)、[前置核验清单](../fawu-rebuild/verification-checklist.md)、[批准的拆分记录](../fawu-rebuild/ticket-breakdown-draft.md)。

## 按依赖选择任务

初始无阻塞任务是 **01**。完成意味着验收及事实证据满足，不只看 `ready-for-agent` 标签；有阻塞的任务在对应前置成果满足后开始。任务类型明确区分核验、功能、验收和分规格准备，准备任务不等于未来业务实现就绪。

01～10 为前置核验，11～32 为必要共用能力与案件功能，33 为案件试点验收，34～46 为后续分规格准备。各项实际状态和验收记录以任务文件为准。

| 编号与任务 | 类型 | 直接阻塞 |
| --- | --- | --- |
| [01 核实测试环境、隔离目标与确认职责](issues/01-environment-baseline.md) | 核验 | None |
| [02 核实统一身份、组织映射及登录退出契约](issues/02-identity-organization-contract.md) | 核验 | [01](issues/01-environment-baseline.md) |
| [03 核实案件审批及旧在途的真实契约](issues/03-approval-inflight-contract.md) | 核验 | [01](issues/01-environment-baseline.md) |
| [04 核定案件字段、状态、参与关系及履行规则](issues/04-case-business-rules.md) | 核验 | [01](issues/01-environment-baseline.md) |
| [05 核实案件历史结构、金额时间及关联样本](issues/05-historical-data-samples.md) | 核验 | [01](issues/01-environment-baseline.md) |
| [06 核定首期角色与案件操作数据范围矩阵](issues/06-case-permission-matrix.md) | 核验 | [02](issues/02-identity-organization-contract.md)、[04](issues/04-case-business-rules.md) |
| [07 核实附件来源与有效访问契约](issues/07-attachment-contracts.md) | 核验 | [01](issues/01-environment-baseline.md) |
| [08 核实有效后台作业及案件通知提醒规则](issues/08-jobs-notifications-baseline.md) | 核验 | [01](issues/01-environment-baseline.md) |
| [09 核定案件关联委托、冻结与联系单的最小契约](issues/09-case-association-contracts.md) | 核验 | [01](issues/01-environment-baseline.md) |
| [10 验证目标运行组合与 PostgreSQL 查询小样](issues/10-runtime-postgresql-validation.md) | 技术核验 | [05](issues/05-historical-data-samples.md) |
| [11 统一登录进入新法务并完成统一退出](issues/11-unified-login-logout.md) | 端到端功能 | [02](issues/02-identity-organization-contract.md)、[10](issues/10-runtime-postgresql-validation.md) |
| [12 自定义角色配置与操作范围授予](issues/12-role-operation-scope.md) | 端到端功能 | [06](issues/06-case-permission-matrix.md)、[11](issues/11-unified-login-logout.md) |
| [13 直接登记案件并按范围保存查询](issues/13-case-registration-query.md) | 端到端功能 | [12](issues/12-role-operation-scope.md) |
| [14 维护参与关系与主责移交后重判访问](issues/14-case-participants-handover.md) | 端到端功能 | [13](issues/13-case-registration-query.md) |
| [15 新案件材料关联与授权下载预览](issues/15-case-attachments-access.md) | 端到端功能 | [07](issues/07-attachment-contracts.md)、[13](issues/13-case-registration-query.md) |
| [16 提交固定立项资料并审批通过正式立项](issues/16-case-initiation-approval.md) | 端到端功能 | [03](issues/03-approval-inflight-contract.md)、[15](issues/15-case-attachments-access.md) |
| [17 同案退回补正重提与合法终止](issues/17-case-resubmission-termination.md) | 端到端功能 | [16](issues/16-case-initiation-approval.md) |
| [18 维护程序事实、阶段进度与独立申请状态](issues/18-case-procedure-progress.md) | 端到端功能 | [16](issues/16-case-initiation-approval.md) |
| [19 受理不明核对及重复迟到结果恢复](issues/19-approval-results-recovery.md) | 端到端功能 | [18](issues/18-case-procedure-progress.md) |
| [20 记录审理结案并继续办理收付及其他履行](issues/20-case-adjudication-obligations.md) | 端到端功能 | [18](issues/18-case-procedure-progress.md) |
| [21 记录特殊事件并保留未办结跟进](issues/21-case-special-events.md) | 端到端功能 | [20](issues/20-case-adjudication-obligations.md) |
| [22 核对履行并授权关闭案件](issues/22-case-closure.md) | 端到端功能 | [20](issues/20-case-adjudication-obligations.md) |
| [23 案件律师委托通过后形成阶段代理关系](issues/23-case-lawyer-engagement.md) | 端到端功能 | [09](issues/09-case-association-contracts.md)、[16](issues/16-case-initiation-approval.md) |
| [24 案件关联冻结账户或资产并查看台账结果](issues/24-case-freeze-association.md) | 端到端功能 | [09](issues/09-case-association-contracts.md)、[13](issues/13-case-registration-query.md) |
| [25 案件联系单申请与协办进展](issues/25-case-contact-sheet-processing.md) | 端到端功能 | [09](issues/09-case-association-contracts.md)、[16](issues/16-case-initiation-approval.md) |
| [26 联系单成果验收及案件关联结果查询](issues/26-contact-sheet-acceptance.md) | 端到端功能 | [25](issues/25-case-contact-sheet-processing.md) |
| [27 历史案件小样迁入 PostgreSQL 并统一查询](issues/27-historical-case-sample-migration.md) | 端到端功能 | [20](issues/20-case-adjudication-obligations.md) |
| [28 历史附件分来源恢复授权访问](issues/28-historical-attachment-access.md) | 端到端功能 | [27](issues/27-historical-case-sample-migration.md) |
| [29 已办结历史只读与专门授权更正](issues/29-closed-history-correction.md) | 端到端功能 | [27](issues/27-historical-case-sample-migration.md) |
| [30 旧在途按申请控写并核对纳入结果](issues/30-inflight-approval-transition.md) | 端到端功能 | [19](issues/19-approval-results-recovery.md)、[23](issues/23-case-lawyer-engagement.md)、[27](issues/27-historical-case-sample-migration.md) |
| [31 案件关键通知发送与防重复恢复](issues/31-case-notification-recovery.md) | 端到端功能 | [08](issues/08-jobs-notifications-baseline.md)、[19](issues/19-approval-results-recovery.md) |
| [32 案件期限提醒与日历贯通](issues/32-case-reminders-calendar.md) | 端到端功能 | [08](issues/08-jobs-notifications-baseline.md)、[20](issues/20-case-adjudication-obligations.md) |
| [33 案件完整链路试用与首个里程碑验收](issues/33-case-pilot-acceptance.md) | 验收 | [14](issues/14-case-participants-handover.md)、[17](issues/17-case-resubmission-termination.md)、[21](issues/21-case-special-events.md)、[22](issues/22-case-closure.md)、[24](issues/24-case-freeze-association.md)、[26](issues/26-contact-sheet-acceptance.md)、[28](issues/28-historical-attachment-access.md)、[29](issues/29-closed-history-correction.md)、[30](issues/30-inflight-approval-transition.md)、[31](issues/31-case-notification-recovery.md)、[32](issues/32-case-reminders-calendar.md) |
| [34 核定诉讼扩展子功能并编写分规格](issues/34-litigation-extensions-spec.md) | 分规格准备 | [01](issues/01-environment-baseline.md) |
| [35 核定查封冻结完整流程并编写分规格](issues/35-freeze-workflows-spec.md) | 分规格准备 | [01](issues/01-environment-baseline.md) |
| [36 核定律所律师合作、费用和评价并编写分规格](issues/36-law-firm-engagement-spec.md) | 分规格准备 | [01](issues/01-environment-baseline.md) |
| [37 核定清欠与明源闭环并编写分规格](issues/37-debt-recovery-spec.md) | 分规格准备 | [01](issues/01-environment-baseline.md) |
| [38 核定合同投融资与履约并编写分规格](issues/38-contract-investment-spec.md) | 分规格准备 | [01](issues/01-environment-baseline.md) |
| [39 核定综合法律事务及量化评估分规格](issues/39-comprehensive-legal-spec.md) | 分规格准备 | [01](issues/01-environment-baseline.md) |
| [40 核定培训与制度指引专题分规格](issues/40-training-policy-spec.md) | 分规格准备 | [01](issues/01-environment-baseline.md) |
| [41 核定知识产权各类别分规格](issues/41-intellectual-property-spec.md) | 分规格准备 | [01](issues/01-environment-baseline.md) |
| [42 核定行政处罚及其他非诉分规格](issues/42-penalty-other-nonlitigation-spec.md) | 分规格准备 | [01](issues/01-environment-baseline.md) |
| [43 核定各类法律事务与联系单完整分规格](issues/43-legal-contact-workflows-spec.md) | 分规格准备 | [01](issues/01-environment-baseline.md) |
| [44 核定绩效重大业绩评分及汇总分规格](issues/44-performance-achievements-spec.md) | 分规格准备 | [01](issues/01-environment-baseline.md) |
| [45 核定外部文件知识与报表分规格](issues/45-knowledge-reporting-spec.md) | 分规格准备 | [01](issues/01-environment-baseline.md) |
| [46 核定剩余共用能力及后台接管分规格](issues/46-shared-capabilities-jobs-spec.md) | 分规格准备 | [07](issues/07-attachment-contracts.md)、[08](issues/08-jobs-notifications-baseline.md) |

## 后续范围

首期十组完整业务保持有效。34～46 取得分规格后继续逐用例拆剩余实施；全历史和附件/身份/审批对账、完整试用、后台接管、恢复演练、联合放行、IT 一次全量切换及旧链退出仍须继续细拆和完成。27～29 的小样与 33 案件里程碑均不能替代这些成果。

本次只发布任务，没有启动核验、业务实现、数据库迁移或部署；现有父规格及决策任务保持原状态。
