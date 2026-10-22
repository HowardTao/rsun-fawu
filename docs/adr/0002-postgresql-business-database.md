# 新业务库采用 PostgreSQL

2026-10-22，用户因 SQL Server 可能涉及许可问题，更正 Q41，决定新业务库采用 PostgreSQL，取代[保留 SQL Server 引擎的原决定](0001-retain-sql-server-engine.md)。旧工程的 SQL Server 依赖仍是迁移事实，需核对查询、数据类型、排序规则、金额与时间语义以及外部报表；新业务库的选择不改变历史数据和外部平台必须保留的要求，也不决定旧库迁移、共存或退出方式。具体 PostgreSQL、驱动及数据访问版本须锁定验证，详见[技术路线决策](../../.scratch/fawu-rebuild/issues/07-architecture-technology-decision.md)。
