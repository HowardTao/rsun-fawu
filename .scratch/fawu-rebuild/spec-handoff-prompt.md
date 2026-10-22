# 规格交接提示词

用途：在 rsun-fawu 工程调用 `/to-spec`，合成总规格与案件分规格。阶段依据见[已确认的实施路线](implementation-roadmap.md)，本提示词供下一阶段使用，本轮尚未生成规格正文。

复制以下提示词开始下一阶段：

```text
$to-spec

请根据已经确认的法务系统完整重建决策，合成规格。本次只写规格与核验事项，不实现业务代码、执行迁移或部署。

新工程：/Users/tony/Documents/我的工作空间/rsun-fawu/
旧代码：/Users/tony/Documents/我的工作空间/RSun.FaWu/
决策地图：/Users/tony/Documents/我的工作空间/rsun-fawu/.scratch/fawu-rebuild/map.md
实施路线：/Users/tony/Documents/我的工作空间/rsun-fawu/.scratch/fawu-rebuild/implementation-roadmap.md

先读取工程 AGENTS.md 及其事项跟踪、分诊、领域文档入口，使用 GLOSSARY.md 与当前有效 ADR。沿地图按需读取已解决事项、业务与迁移验收基线及原始代码事实，保留用户最新的数据库更正：新业务库 PostgreSQL，旧 SQL Server 依赖是迁移输入。

输出：
1. .scratch/fawu-rebuild/spec.md：完整重建总规格，覆盖十组业务、产品/技术约束、阶段依赖、前置核验及正式验收；作为各分规格索引。
2. .scratch/case-lifecycle/spec.md：案件完整链路首份分规格，覆盖已确认的角色权限、登记立项补正、程序事实与进展、主责移交、结案履行关闭、必要关联能力及历史/在途处理。

沿用已确认的用户取舍直接综合，不重新采访已经回答的问题。状态全集、平台字段、SQL 与真实数据情况等缺口，在规格中列明核验来源、影响的用例和通过条件；业务取舍确实新增或冲突时明确提出，不能凭菜单、文档示例或猜测填补。

以业务模块的用例接口作为主要行为验证入口，采用已确认的案件端到端试点和直接接口/附件授权预期；关键 UI 与真实外部平台另验证贯通。规格的 Implementation Decisions 描述模块职责、接口及行为，不写假想实现路径或代码。未执行的验证如实标注。

使用 to-spec 模板和本地 Markdown 跟踪约定。保持第一期完整业务目标，案件是首个验证链路；MCP/AI 协同具体工具在业务重建后另规划。
```
