# 30: 旧在途按申请控写并核对纳入结果

Status: ready-for-agent

**Parent:** [完整重建总规格](../../fawu-rebuild/spec.md)；[案件完整链路分规格](../../case-lifecycle/spec.md)

**工作类型：** 端到端功能

**What to build:** 对试点旧在途委托保留唯一旧链及补正，限制该申请及依赖操作，其他合法办案在新系统继续，旧结果核对后纳入对应业务。

**Blocked by:** [19 受理不明核对及重复迟到结果恢复](19-approval-results-recovery.md)；[23 案件律师委托通过后形成阶段代理关系](23-case-lawyer-engagement.md)；[27 历史案件小样迁入 PostgreSQL 并统一查询](27-historical-case-sample-migration.md)。

**规格覆盖：** C-40～42；TC-20；TG-09。

**事实与规则来源：** [前置核验清单](../../fawu-rebuild/verification-checklist.md)；[历史迁移与过渡基线](../../fawu-rebuild/historical-migration.md)。

## Acceptance criteria

- [ ] 原链/新申请归属可核对。
- [ ] 不锁整案，程序事实仍可维护。
- [ ] 旧结果不覆盖新事实或重复委托效果，旧链退出条件有证据但不在本任务切换生产。

## 执行边界

完成直接依赖并核对事实后实施本用例，验证外部行为、权限及业务成果；真实平台贯通与测试替身结果分别记录。未核定字段或规则先记录缺口，不用猜测补全。不得把本用例完成当作整域、全量历史或正式上线完成。

## Comments

- 2026-10-22：用户已确认首批 46 项拆分，按已批准草稿发布。本任务尚未执行，验收项均未完成。
