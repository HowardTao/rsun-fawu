# 分诊标签

五个规范角色直接映射为同名字符串。

| 规范角色 | 本工程字符串 | 含义 |
| --- | --- | --- |
| `needs-triage` | `needs-triage` | 等待维护者评估 |
| `needs-info` | `needs-info` | 等待补充信息 |
| `ready-for-agent` | `ready-for-agent` | 规格完整，可由 agent 实施 |
| `ready-for-human` | `ready-for-human` | 需要人工实施 |
| `wontfix` | `wontfix` | 不予处理 |

技能提及分诊角色时，使用表中的本工程字符串。
本地 Markdown 实施任务通过顶部的 `Status:` 行记录这些字符串。
以后调整词汇时，修改“本工程字符串”列，并同步受影响任务的状态。
