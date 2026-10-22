# 02: 核实统一身份、组织映射及登录退出契约

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 核验

**What to build:** 核定稳定人员标识、权威组织来源、旧新身份对照，以及真实登录、禁用和统一退出链路。

**Blocked by:** [01 核实测试环境、隔离目标与确认职责](01-environment-baseline.md)。

**规格覆盖：** V02；G-01、G-08～12。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[SSO 文档核对](../../fawu-rebuild/research/sso-document-contracts.md)；[身份与审批决定](../../fawu-rebuild/issues/08-identity-approval-contract-decision.md)。

## Acceptance criteria

- [ ] 不以姓名匹配身份。
- [ ] 改名/离职样本保留原归属。
- [ ] 真实注册、属性、回跳和退出能力有证据，不假定 OIDC 或组织字段。

## 执行边界

本任务交付核验事实和结论，不实现后续业务功能。保留来源、样本、期望/实际、差异及确认职责；缺访问或材料时记录具体缺口，不能把未核实内容当通过。涉及写回的测试仅使用已经明确的可恢复副本或隔离目标。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
