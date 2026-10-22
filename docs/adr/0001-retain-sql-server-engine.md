---
status: superseded by ADR-0002
---

# 完整重建仍保留 SQL Server 业务库引擎

此决定已被用户于 2026-10-22 更正，由[新业务库采用 PostgreSQL](0002-postgresql-business-database.md)取代。下文保留原取舍记录，不再作为当前技术基线。

旧工程数据访问与同步实现依赖 SQL Server，历史资产及外部平台必须保留。2026-10-22，用户比较 SQL Server 与 PostgreSQL 后，决定新业务库采用 SQL Server，以减少同时更换引擎带来的查询、数据语义和报表迁移工作；PostgreSQL 的许可费用优势不足以替代这些迁移核验。该决定不要求沿用旧表结构或旧服务器版本，具体版本、历史迁移与新旧读写归属另行确定，见[技术路线决策](../../.scratch/fawu-rebuild/issues/07-architecture-technology-decision.md)。
