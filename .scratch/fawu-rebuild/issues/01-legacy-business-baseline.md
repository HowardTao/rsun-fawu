# 核实旧系统完整业务与权限基线

```text
Parent: ../map.md
Type: research
Label: wayfinder:research
Status: resolved
Claimed by: legacy_business_evidence
Blocked by: None
```

## Question

旧代码能够证实哪些完整业务能力、流程、角色和授权规则？形成有出处的业务清单，区分实现存在、当前使用情况和待业务确认事项，作为全量重建范围讨论的依据。

## Dependencies

无，可独立推进。

## Completion criteria

- 按主要业务域抽样核实页面、业务入口、数据及后台任务，避免只凭菜单或文件名断言。
- 每项给出绝对路径和行号；记录未证实的流程与运行状态。
- 形成一份研究报告，不替用户决定保留、调整或废弃能力。

## Answer

已形成主要业务、权限和后台能力的代码证据清单；生产使用情况和完整流程仍需业务及环境验证。

- [研究报告（本地）](../research/legacy-business-baseline.md)
- [已推送的固定提交版本](https://github.com/HowardTao/rsun-fawu/blob/d081defdce728a4df27f100ccb018811aaf57985/docs/research/legacy-business-baseline.md)
- 研究分支：`research/legacy-business-baseline`；提交：`d081defdce728a4df27f100ccb018811aaf57985`。报告已单独提交并推送，未合并到主工程。
- 本地报告为上述固定提交的阅读副本，仅调整本地导航链接。
- 本次仅完成静态证据研究；业务取舍、运行验证、技术及迁移选择由后续决策任务处理。
