# 选择完整重建的产品技术与业务模块路线

```text
Parent: ../map.md
Type: grilling
Label: wayfinder:grilling
Status: resolved
Claimed by: root
Blocked by: 02, 03, 05, 06, 13
```

## Question

在完整业务目标和既有集成约束下，选择新产品技术栈、业务模块划分及旧系统过渡路线。业务规则怎样集中维护并可供界面与后续业务接口复用？

## Inputs

- [上线、部署与维护约束](../delivery-constraints.md)
- [技术候选补充核对](../research/technology-candidate-followup.md)：结合团队经验的 .NET、Element 系前端、Ubuntu LTS 及数据库候选资料；具体版本和兼容性仍需锁定验证。

## Dependencies

- [核实必须保留的登录、审批和历史资产契约](02-preserved-integration-contracts.md)
- [研究重建技术候选与业务接口复用条件](03-rebuild-technology-options.md)
- [明确新产品角色、流程和关键业务模型](05-product-roles-workflows.md)
- [确认上线、部署和维护硬约束](06-delivery-deployment-constraints.md)
- [明确其余业务域的流程与关键规则](13-remaining-business-workflows.md)

## Discussion materials

- [产品技术与业务模块路线](../architecture-options.md)：已确认的前后端、模块职责、部署及过渡原则；数据库更正与未验证前提。

## Confirmed decisions

2026-10-22，用户在 Q39–Q44 及 Q41 更正中确认：

- 后端采用 .NET 10 LTS / ASP.NET Core 10，前端采用 Vue 3 / Element Plus。
- 后端采用一个应用，按业务模块组织；规则集中在模块内，页面与后台作业调用模块接口并统一执行授权和业务校验，未来 MCP 复用这些业务能力。
- 新业务库采用 PostgreSQL，覆盖 Q41 最初的 SQL Server 选择；更正原因是 SQL Server 可能涉及许可问题。具体版本、新表结构、历史迁移及外部报表适配尚未确定。
- 采用模块职责表作为规格基线，业务模块维护自己的记录、状态、金额及办结规则，其他模块经接口协作；共用能力负责授权和平台衔接，不统一解释所有业务成果。
- 主应用采用 Ubuntu 24.04 LTS + Nginx，同域托管前端与后端接口。
- 优先直接适配现有平台接口；仅当验证证明必须依赖 Windows / .NET Framework 组件时，允许隔离的 Windows 集成过渡进程，并明确调用责任、失败处理和退出条件。

上述是路线决定，不是部署或兼容验证结果。SQL Server 旧库及外部组织、审批、文件等平台的资产保留和读写归属继续在相应决策中明确。

## Comments

- 2026-10-22：其余业务规则事项已解决，开始选择技术路线。SQL Server 依赖已补充静态证据，实际版本和部署未核实；技术候选等待用户决定。
- Q39–Q41 已确认前后端组合、单个后端应用按业务模块组织，以及 SQL Server 引擎；数据库取舍记录于[保留 SQL Server 引擎的决策](../../../docs/adr/0001-retain-sql-server-engine.md)。
- Q42–Q44 确认模块职责基线、Ubuntu + Nginx 同域部署和有条件的 Windows 集成过渡原则。
- 用户随后更正 Q41 为 PostgreSQL，原因是 SQL Server 许可顾虑；原数据库决定已被[PostgreSQL 决策](../../../docs/adr/0002-postgresql-business-database.md)取代，其余选择不变。

## Completion criteria

- 比较有证据支撑的路线，列明权衡和未验证前提。
- 确定业务规则、数据读写和外部集成各自的责任；不在界面或未来 MCP 中重复实现核心规则。
- 只有满足难逆转、真实取舍且未来容易误解的决定才提出 ADR。

## Answer

完整重建采用 .NET 10 LTS / ASP.NET Core 10 + Vue 3 / Element Plus，新业务库采用 PostgreSQL；主应用 Ubuntu 24.04 LTS + Nginx，同域提供前端与接口。后端为一个应用，按[模块职责基线](../architecture-options.md#模块职责基线已确认)组织；不机械地把业务分组变成独立部署服务。

每个业务模块负责自己的记录、业务校验、状态、金额与办结条件，其他模块通过其接口协作。页面和后台作业复用模块接口及统一授权；后续 MCP 也复用这些业务能力，具体 AI 场景继续在本轮范围外。共用能力处理身份授权、附件、审批与通知等平台衔接；审批回传交给所属业务模块解释业务效果，不能以通用状态覆盖案件程序事实或所有业务完成条件。

保留既有外部平台，优先直接适配。实测证明旧组件确有 Windows / Framework 限制时才采用隔离的 Windows 集成过渡进程；调用权限、失败恢复及退出条件在集成规格中明确。本轮未证明需要该进程，也没有保留旧界面作为首期产品范围的决定。

数据库更正及理由见[新业务库采用 PostgreSQL](../../../docs/adr/0002-postgresql-business-database.md)。旧 SQL Server 依赖必须进入跨引擎迁移与报表核验；新旧库、历史附件及在途审批的读写权威由后续历史保留与切换事项明确，不预设双写。

框架补丁、PostgreSQL 版本、驱动与数据访问方式、组件兼容、浏览器、真实部署及备份恢复仍须在规格中锁定并验证。已选路线不等于兼容实验通过；本事项完成架构路线选择，没有实施业务代码或执行迁移。
