# 其余业务域主流程核对与保留原则

关联事项：[明确其余业务域的流程与关键规则](issues/13-remaining-business-workflows.md)。

九组业务均已纳入首期。本表用每组一条实际源码路径核对主流程或主要场景；成果仅指该代表路径的结果，不代表整组全部流程已经核实。生产使用、完整权限及外部规则仍需结合测试环境确认。

## 代表路径与事实边界

| 业务 | 已核实的代表路径及成果 | 操作者与尚待核实的边界 | 来源 |
| --- | --- | --- | --- |
| 查封冻结 | 关联冻结账户 → 保存账户/资产明细 → 汇总冻结、解封、剩余金额及到期日 | 保存留有当前人员和组织信息；具体写权限未核实。读取的是本地冻结数据中心，主诉、续封及上游同步未全核实 | [被诉冻结表单](../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/AnJianCFGL_BSCF.aspx#L48)、[保存与汇总](../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/AnJianCFGL_BSCF.aspx.cs#L78) |
| 律所律师与委托 | 准备律师库 → 保存合作委托 → 发起合作审批 → 同意后回写委托及关联律师记录 | 律师导入明确检查律所事务管理员，不能据此推定全部委托操作权限。审批同意不代表合同签署或费用结算已完成 | [律师导入权限](../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/LvShiController.cs#L28)、[合作申请](../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/LiuChengController.cs#L2113)、[回调](../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ProcessController.cs#L1993) |
| 清欠 | 准备接收信息和日志 → 明源回写成功 → 提交本地接收记录 | 接收人记录为当前人员；完整授权及前置状态检查未核实。明源失败会跳过本地提交，明源成功但本地提交失败未见统一补偿 | [接收方法](../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/QingQianController.cs#L54)、[明源结果校验](../../../RSun.FaWu/fwxt.Web/fwxt.Web/Code/Api/QingQianApi.cs#L87) |
| 合同与投融资 | 投融资项目登记 → 项目进度、尽调与协议维护 → 成功时显示合同归档/履约记录 → 合同附件打包 | 保存前汇总内部承办法务及履约标记；默认经办人不等于权限检查。该代表路径未发现直接审批；重大合同等其他路径继续核实 | [项目表单](../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/TouRongZiXMGL.aspx#L42)、[保存事件](../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/TouRongZiXMGL.aspx.cs#L24)、[合同打包](../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/TouRongZiXMGLController.cs#L16) |
| 非诉事务 | 行政处罚登记 → 维护进展、撤销/变更/维持等结果 → 维护金额、执行标记和附件 | 未付金额有前端计算，服务端校验及具体授权未核实。综合法律、培训、制度专题、知识产权等仍按范围清单保留，不能由此一张表推定全部流程 | [行政处罚表单](../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/XingZhengCFGL.aspx#L42) |
| 法律事务与联系单 | 法务联系单保存 → 申请审批同意 → 协办人待办/未读 → 协办打开后已读 → 办理进展与验收申请 → 验收同意后已办结 | 读取变已读明确核对协办账号；其他授权未完整核实。申请同意不是办结。一般法律事务及诉讼联系单未全部核实 | [协办读取](../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/LianXiDanGLZX.aspx.cs#L19)、[申请及验收](../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/LiuChengController.cs#L1219)、[两次回调](../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ProcessController.cs#L127) |
| 绩效与重大业绩 | 申报及参与比例 → 草稿/待评分 → 初评 → 复核 | 原保存事件推进已初评、已复核；没有据此证明两步必须由不同人员执行。评分权限、有效公式及汇总使用仍需确认 | [申报保存](../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/ZhongDaYJSB.aspx.cs#L28)、[评分保存](../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/ZhongDaYJPF.aspx.cs#L23) |
| 文件知识与报表 | 进入法务页面 → 加载外部文件应用或指定报表 | 外部产品本体按已确认约束保留；其认证、发布/审核、计算口径及刷新不可从 iframe 推断为本地实现 | [文件应用](../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/FaLvGJK.aspx#L11)、[综合报表](../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/SuSongAJZHBB.aspx#L24) |
| 共用能力与后台作业 | kaiting 命令 → 查询启用提醒规则及开庭信息 → 生成站内消息并调用通知渠道 → 保存消息 | 程序分派及发送链有效；真实任务调度、运行账号、规则和渠道启用/送达仍未核实。权限、附件、分享及主数据同步继续按既有范围核对 | [命令分派](../../../RSun.FaWu/fwxt.Web/fwxt.MgrSvr/Program.cs#L80)、[开庭提醒](../../../RSun.FaWu/fwxt.Web/fwxt.MgrSvr/AnJianLY.cs#L105) |

## 已发现的实现疑点

- 清欠的外部成功与本地提交之间未发现统一事务或补偿，不能描述为已经原子完成。
- 联系单发起成功后的部分代码修改一个数据上下文，却提交另一个上下文；回调另有提交。不能认为发起时的状态已经可靠持久化。
- 绩效保存事件改变评分状态，未证明已校验初评、复核的操作权限或人员关系。

这些是实现与核验问题，不自动成为需要原样保留的业务规则。

## 已确认的保留与调整原则

2026-10-22，用户在 Q36–Q38 确认现行有效流程作为基线、逐域核对调整，清欠回写两边一致后确认完成，重大业绩初评和复核分别授权并允许同一人员兼任。完整决定与异常处理要求见[关联事项的答案](issues/13-remaining-business-workflows.md#answer)。

角色继续采用自定义与操作/数据范围成对授权的既定原则。具体字段、全部子流程及生产样例由后续规格与环境核验补齐；本表不表示这些内容已经验收。
