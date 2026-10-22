# 10: 验证目标运行组合与 PostgreSQL 查询小样

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 技术核验

**What to build:** 验证所选 .NET、Vue/Element Plus、PostgreSQL、驱动/数据访问与 Ubuntu/Nginx 同域组合能运行，代表金额时间查询保持核定语义。

**Blocked by:** [05 核实案件历史结构、金额时间及关联样本](05-historical-data-samples.md)。

**规格覆盖：** V12（运行组合部分）、V06。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[技术路线](../../fawu-rebuild/architecture-options.md)；[PostgreSQL 适配核对](../../fawu-rebuild/research/postgresql-compatibility-followup.md)；[部署约束](../../fawu-rebuild/delivery-constraints.md)。

## Acceptance criteria

- [ ] 锁定具体版本并有构建/运行及数据库小样结果。
- [ ] 金额时间/中文排序搜索差异可解释。
- [ ] 确需 Windows 适配时有证据与调用/恢复/退出设计，不创建假业务。

## 执行边界

本任务限于已选运行组合和代表数据的技术核验，记录实际版本及验证结果，不新增产品业务或未证实的技术平台。依赖的真实数据语义未明确时先记录缺口，不猜测转换。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
