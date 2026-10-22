# 11: 统一登录进入新法务并完成统一退出

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 端到端功能

**What to build:** 真实统一身份用户从浏览器进入新法务，身份映射正确；未映射、未授权或禁用身份不能进入相应业务，统一退出效果明确。

**Blocked by:** [02 核实统一身份、组织映射及登录退出契约](02-identity-organization-contract.md)；[10 验证目标运行组合与 PostgreSQL 查询小样](10-runtime-postgresql-validation.md)。

**规格覆盖：** G-01、G-08～11；TG-01。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[SSO 文档核对](../../fawu-rebuild/research/sso-document-contracts.md)；[身份与审批决定](../../fawu-rebuild/issues/08-identity-approval-contract-decision.md)。

## Acceptance criteria

- [ ] 界面与服务端身份贯通，映射可持久化追溯。
- [ ] 直接访问受保护入口不能绕过检查。
- [ ] 实际浏览器统一退出与本地会话结束均验证。

## 执行边界

完成直接依赖并核对事实后实施本用例，验证外部行为、权限及业务成果；真实平台贯通与测试替身结果分别记录。未核定字段或规则先记录缺口，不用猜测补全。不得把本用例完成当作整域、全量历史或正式上线完成。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
