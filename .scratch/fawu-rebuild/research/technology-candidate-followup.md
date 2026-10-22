# 技术候选补充核对

规划日期：2026-10-21（Asia/Shanghai）。用于本工程技术候选比较，不是已完成的选型或运行验证。

## 官方事实与候选条件

| 项目 | 可确认事实 | 本工程仍需核验 |
| --- | --- | --- |
| .NET 10 / ASP.NET Core 10 | 既有研究已核实 .NET 10 为 LTS，支持至 2028-11-14；见[原技术研究](rebuild-technology-options.md) | 选定补丁、第三方组件及实际部署兼容 |
| Ubuntu LTS | .NET 10 官方 OS 列表列 Ubuntu 22.04、24.04、26.04，页面标注 2026-09-28 更新 [S1] | CPU、系统依赖、运维方案；数据库服务器须另核支持矩阵 |
| Element UI 与 Element Plus | Element UI 官方保持 Vue 2.x，并推荐 Vue 3 使用 Element Plus；Element Plus 基于 Vue 3，首个稳定版于 2022-02-07 发布 [S2][S3] | 组件版本、表格/表单/上传与团队适应；旧组件 API 不自动兼容 |
| 浏览器 | Vue 2 于 2023-12-31 结束官方支持，Vue 3 不支持 IE11 [S4] | 公司实际客户端及现代浏览器支持要求；未查到 Element Plus 固定 LTS/EOL 承诺 |
| SQL Server | EF Core 有微软维护的 SQL Server provider [S5] | 实际旧库版本、生产许可、兼容级别及历史 SQL/报表依赖 |
| PostgreSQL | 官方许可允许无许可费使用；Npgsql 有 EF Core provider 10.0 文档 [S6][S7] | 锁定包的发布时间、TFM、EF Core 依赖及数据库版本；跨引擎迁移、备份和运维成本 |

SQL Server provider 的动态详情页出现 SQL Server 2019+ 要求及 EF Core 11 示例，而通用 provider 表曾列 SQL Server 2012+。不能将这些不同范围直接作为锁定 EF Core 10 的最低要求，应按具体包版本和服务器版本核对。Npgsql 页面本次未提供可核实的发布日期，也不倒推包在规划日期的可用性。

SQL Server 2022 的 Developer 版仅用于开发测试，Express 免费但单库上限 10 GB [S8]。这是该版本的示例限制，不能代替新生产环境的版本、容量与许可选择。PostgreSQL 无许可费也不代表迁移和长期维护没有成本。

## 对本工程的初步建议

- 优先评估 ASP.NET Core / .NET 10 LTS 与 Vue 3 / Element Plus，沿用团队的 .NET 和 Element 系组件经验。
- 主应用服务器优先评估 Ubuntu 24.04 LTS。既有 SDK、文件依赖及运维方式仍需实际验证；不据此认定旧系统整体可跨平台。
- SQL Server 可作为迁移成本优先的数据库候选，与 PostgreSQL 比较。实际数据引擎与版本、历史 SQL、存储过程、排序规则、金额时间语义及报表依赖仍需核实。
- 最终数据库、部署和框架版本由后续技术决策确定；本次没有安装软件、连接数据库或访问生产配置。

## 官方来源

- **S1**：[.NET 10 支持的操作系统](https://github.com/dotnet/core/blob/main/release-notes/10.0/supported-os.md)
- **S2**：[Element UI 官方 README](https://github.com/ElemeFE/element/blob/dev/README.md)
- **S3**：[Element Plus 官方 README](https://github.com/element-plus/element-plus/blob/dev/README.md)
- **S4**：[Vue 官方 FAQ](https://vuejs.org/about/faq.html)
- **S5**：[微软 SQL Server EF Core provider](https://learn.microsoft.com/en-us/ef/core/providers/sql-server/)
- **S6**：[Npgsql EF Core provider 10.0](https://www.npgsql.org/efcore/release-notes/10.0.html)
- **S7**：[PostgreSQL 许可](https://www.postgresql.org/about/licence/)
- **S8**：[SQL Server 2022 版本与功能限制](https://learn.microsoft.com/en-us/sql/sql-server/editions-and-components-of-sql-server-2022?view=sql-server-ver16)

动态网页及仓库反映本次读取内容；明确历史日期之外，不据此倒推某版本在规划日期已发布。此补充资料用于本仓库候选评估。
