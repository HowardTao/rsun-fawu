# 研究重建技术候选与业务接口复用条件

```text
Parent: ../map.md
Type: research
Label: wayfinder:research
Status: resolved
Claimed by: technology_options_research
Blocked by: None
```

## Question

依据官方文档，哪些 .NET 产品与架构路线适合重建完整法务业务并保留现有集成？比较有限的候选，说明部署、身份接入、测试与未来 MCP 接入的前提和限制；本任务不替用户选择技术栈。

## Dependencies

无，可独立推进。

## Completion criteria

- 只引用官方文档、标准或官方源码；区别验证事实与方案判断。
- 核实当前 .NET 支持与旧 System.Web/WebForms 兼容边界，不依据版本名称推断能够直接迁移。
- 未来 MCP 只作为业务接口复用的约束研究，不定义首期工具或 AI 产品场景。
- 列出仍取决于企业部署环境、团队能力和集成验证的选择。

## Answer

已按官方来源比较现代 .NET 产品路线及旧集成过渡条件；部署、数据库、接口兼容与最终技术选择仍待用户和环境确认。

- [研究报告（本地）](../research/rebuild-technology-options.md)
- [已推送的固定提交版本](https://github.com/HowardTao/rsun-fawu/blob/3aaf981ea92e4ba011b03ac6ef04ffa4353e8974/docs/research/rebuild-technology-options.md)
- 研究分支：`research/rebuild-technology-options`；提交：`3aaf981ea92e4ba011b03ac6ef04ffa4353e8974`。仅提交该报告并推送，未合并到主工程。
- 本地报告为上述固定提交的阅读副本，仅调整本地导航链接。
- 已核实官方支持期与 WebForms/现代 .NET 的兼容边界；报告比较两个现代产品路线和必要时的旧集成过渡条件，不构成技术选型决定。
- SSO 文档按用户要求留到后续身份衔接任务；本次没有读取或确认其协议兼容性。
- 未来 MCP 资料使用明确版本或动态仓库快照；未确认最新协议或包版本的内容已注明，不能视为首期工具设计或长期支持承诺。
