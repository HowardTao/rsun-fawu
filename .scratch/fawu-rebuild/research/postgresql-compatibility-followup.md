# PostgreSQL 许可与 .NET 10 适配核对

核对日期：2026-10-22。用于[技术路线选择](../issues/07-architecture-technology-decision.md)与[历史迁移规划](../issues/09-historical-data-attachment-migration.md)。新业务库已由用户选定 PostgreSQL；本次仅核对资料，没有选定 ORM、锁定补丁、安装包或连接数据库。

## 可核实的发布与许可事实

| 项目 | 已核实内容 | 官方来源 |
| --- | --- | --- |
| PostgreSQL License | 允许为任何目的使用、复制、修改和分发，无需许可费，要求保留许可声明；不包含维护、技术支持或担保承诺 | [官方许可](https://www.postgresql.org/about/licence/) |
| Npgsql EF Core provider 10.0.0 | NuGet published 字段为 2025-11-22，早于规划日期 | [发布元数据](https://api.nuget.org/v3/registration5-gz-semver2/npgsql.entityframeworkcore.postgresql/10.0.0.json) |
| Npgsql EF Core provider 10.0.3 | published 为 2026-07-10；目标 net10.0，依赖 EF Core / Relational ≥10.0.4 且 <11.0.0，Npgsql ≥10.0.3 | [发布元数据](https://api.nuget.org/v3/registration5-gz-semver2/npgsql.entityframeworkcore.postgresql/10.0.3.json)、[框架与依赖](https://www.nuget.org/packages/Npgsql.EntityFrameworkCore.PostgreSQL/10.0.3) |
| Npgsql 驱动 10.0.0 | published 为 2025-11-22；包页面含 net8.0、net9.0、net10.0 依赖组 | [发布元数据](https://api.nuget.org/v3/registration5-gz-semver2/npgsql/10.0.0.json)、[框架与依赖](https://www.nuget.org/packages/Npgsql/10.0.0) |

发布时间来自带 published 字段的元数据，不依据动态页面倒推。这些包证明已有可供比较的 .NET 10 适配路径，不代表本工程已经选定 EF Core 或这些版本是最终组合。

## 跨引擎迁移核验门槛

- 盘点 LINQ to SQL、T-SQL、存储过程、触发器、同步与报表依赖，不能只换连接字符串或 provider。
- 对账金额精度、舍入、空值、日期范围与时区。[Npgsql 官方时间映射](https://www.npgsql.org/doc/types/datetime.html)区分 UTC DateTime 对应 timestamptz 与 Local/Unspecified 对应 timestamp；向 timestamptz 写非 UTC 值会报错。旧记录的时间含义需先核实。
- 验证中文排序、大小写、搜索、分页及汇总结果，不把不同引擎默认行为当作同一业务口径。
- 保持业务、人员组织、审批实例、状态及附件关联；迁移范围和新旧写入归属由决策明确。
- 验证并发、重复提交、外部回写补偿、最终同步、切换及回退。

PostgreSQL 主版本、真实结构与规模、SQL/报表依赖清单、具体包组合的恢复编译、查询及迁移对账仍未验证。最终数据访问方式及版本由规格锁定，不在本记录中默认决定。
