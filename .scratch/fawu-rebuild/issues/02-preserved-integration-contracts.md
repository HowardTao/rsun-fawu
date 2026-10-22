# 核实必须保留的登录、审批和历史资产契约

```text
Parent: ../map.md
Type: research
Label: wayfinder:research
Status: resolved
Claimed by: preserved_contracts_research
Blocked by: None
```

## Question

为了保留现有登录、审批平台和历史数据，旧实现暴露了哪些身份、组织授权、审批发起/回调、数据库及附件契约？哪些内容必须在 Windows 测试环境验证后才能确定重建方案？

## Dependencies

无，可独立推进。

## Completion criteria

- 核实当前代码路径，区分引用的组件与实际调用的接口。
- 覆盖账号标识、组织授权、审批状态回写、在途实例、历史记录及附件存储。
- 提供验证清单与证据，明确静态代码无法确定的数据规模、启用配置和运行行为。

## Answer

已核实身份、SDK3审批与历史标识/附件契约，并列出Windows验证清单；运行兼容性、整体幂等性和真实资产规模未证实。

- [研究报告（本地）](../research/preserved-integration-contracts.md)
- [已推送的固定提交版本](https://github.com/HowardTao/rsun-fawu/blob/81206ef5bac3163da792789fa796b07f00c58392/docs/research/preserved-integration-contracts.md)
- 研究分支：`research/preserved-integration-contracts`；提交：`81206ef5bac3163da792789fa796b07f00c58392`。报告已单独提交并推送，未合并到主工程。
- 本地报告为上述固定提交的阅读副本，仅调整本地导航链接。
- 本次仅完成静态证据研究；业务取舍、运行验证、技术及迁移选择由后续决策任务处理。
