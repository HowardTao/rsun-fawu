# 必须保留的登录、审批与历史资产契约核实

核实日期：2026-10-21。用途：为法务系统全面重建的决策地图提供证据。

用户已明确：首期全面重建产品与架构，先覆盖完整业务；MCP 与 AI Agent 的具体使用场景后续规划。首期主要用户为集团法务与业务经办人；现有登录、审批平台和历史数据必须保留。Windows 测试环境可用，但本轮没有访问方式。

本报告只读取原始源码与 DBML 模型，没有运行旧程序、连接数据库或调用外部服务。没有读取或收录密码、令牌、证书和连接串值。知识库按“RSun.FaWu / rsun-fawu / 法务系统”检索未命中已有结论。工程尚无领域词汇表或相关 ADR。

证据分类：**事实**表示代码或模型明确包含的行为；**推断**表示据此提出的规划含义；**运行待验证**表示必须结合实际部署、平台契约和数据才能确定的事项。代码中的实现与常量不等于当前环境启用情况，也不自动成为新产品需求。

## 结论

保留要求至少涉及四组关联：登录名与组织身份、审批平台实例与本地业务记录、历史记录的多种标识、附件元数据与实际文件。现有代码提供了这些关联的线索，尚不足以确定新旧切换方案。尤其应验证审批回调的重复与失败恢复、在途实例归属，以及旧附件预览产生写入的行为。

## 登录与组织授权

### 事实

- 桌面 SSO 入口先检查 `HttpContext.Current.User.Identity.Name`；有值时用该名称调用 `LoginHelper.Login`。否则读取请求中的 `ticket`，没有 ticket 时重定向到登录服务；有 ticket 时调用 `validate?ticket=...&service=...`，按首行 `yes`、次行登录名解析响应，再建立本地登录状态。服务地址来自配置键，本报告未读取其值。[SSO 入口](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/SSO.ashx.cs:34)、[验证及响应解析](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/SSO.ashx.cs:64)。
- 本地登录按 `W2OC.Users` 中的 `LoginName` 精确匹配人员；用户不存在会抛异常。随后保存登录名、姓名、管理员标识与用户部门列表到 Session。登录入口根据 `SSO.ENABLE` 选择 SSO 或旧登录页；Session 超时在代码中设为 120 分钟。[人员匹配与会话](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Code/Helper/LoginHelper.cs:14)、[入口分支](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Code/Helper/LoginHelper.cs:40)、[会话设置](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Code/Helper/LoginHelper.cs:62)。
- Session 缺失时，`GetSession` 尝试解密指定登录名 Cookie 并重新调用 `Login`。这是另一条代码路径；本次没有检查加密实现、部署模块或实际 Cookie 属性，因此不能据此判断整体认证是否安全或当前是否在用。[会话恢复](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Code/Helper/LoginHelper.cs:217)。
- `PowerMgr` 从 `SysPowerSetting` 加载权限，按当前登录名或当前人员的 `DepartmentID` 匹配允许对象；允许用户、菜单和组织字段以逗号分隔。组织展开查询 `FNumber.Contains` 并筛选可见部门；权限缓存超过 60 分钟重新加载，也有显式清除入口。这说明实现中至少存在“授予谁”和“能访问哪些组织”两类字段。[匹配与缓存](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Code/Helper/PowerMgr.cs:16)、[字段映射](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Code/Helper/PowerMgr.cs:49)、[组织展开](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Code/Helper/PowerMgr.cs:81)。
- 组织模型中的人员主键 `ID`、`LoginName`、`CompanyID` 与 `DepartmentID` 为不同字段；部门以 `ID / ParentID` 定义树状关联。不能把姓名、登录名、人员 ID、部门 ID 当作可互换标识。[人员字段](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Data/CINDERELLAW2.dbml:32)、[部门关联](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Data/CINDERELLAW2.dbml:2)。

### 推断与运行待验证

重建需要明确现有 SSO 返回的账号如何映射到新系统主体，哪些组织字段是稳定标识，账号改名、离职和部门调整如何影响历史经办记录及当前访问。保留现有登录不等于复制现有 Session/Cookie 机制，也没有证据表明必须替换 SSO。

待验证：实际启用的 SSO 分支、IIS 或认证模块建立身份的方式、桌面/移动端登录是否一致、回跳域名和注销行为；至少用集团法务、业务经办人和无授权人员分别对照页面、查询、详情、附件及直接接口访问。上述权限辅助类不能证明每个入口都已正确执行授权。

## 审批发起、回调与在途实例

### 事实

- 本轮抽样核实的 SDK3 发起实现，实际向 `%DM_BC%/NNForm/api/bpmsend/sdk3?type=json` 展开后的地址发送 HTTP POST，使用 multipart 字段 `json`；收到 HTTP 200 后反序列化 `success / data`。这条调用路径不能仅凭工程中的 Ultimus 组件引用描述为“直接调用 Ultimus”。底层平台和实际路由仍待确认。[请求实现](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Config/SDK3Base.cs:199)。
- 发起前创建或查找 `T_ProcessLogs`，查找条件包含流程名、`FromID.Contains(fromId)` 与非完成/非取消状态；草稿状态为 `-1`。发送数据包含代码设置的 `sysName`、本地日志 `ID` 对应的 `dataId`、`processName` 和发起人登录名。日志及表单数据先 `SubmitChanges`，再发远程请求；成功且 `noUi` 时记录 `incident`、审批中状态 `0`，再次保存。[日志与身份字段](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Config/SDK3Base.cs:235)。这只说明有日志复用逻辑，不能证明并发发起或远端重试不会创建重复实例。
- 回调实体包含 `dataId`、`processName`、`incident`、`initiatorName`、`dataVersion`、`currentUserName`、`appResult` 及审批历史等字段；代码注释将 `appResult` 的 `0 / 1 / 2 / 3` 描述为审批中、同意完成、退回发起人、取消终止。[回调结构](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Config/SDK3Base.cs:87)。
- 默认路由为 `api/{controller}/{action}`，应用启动注册该路由，因此源码中可定位回调入口为 `ProcessController.CallBack` 对应的路径；它从请求体反序列化数据，先调用日志回写，再按 `processName` 分派立项、跟进、委托、评定、法律事务和联系单等处理，返回 JSON 的 `success` 与 `data`。实际部署前缀、网关、请求方法及来源认证不在本轮证据内。[路由](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/MVC/RouteConfig.cs:10)、[注册](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Global.asax.cs:14)、[回调入口](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ProcessController.cs:49)。
- 日志回写按 `T_ProcessLogs.ID == dataId` 取记录，若原状态已为 `1` 或 `3` 则返回 `true`，否则写入状态、实例号与序列化审批历史。但控制器在接到该返回后仍继续分派业务回写；日志回写与业务回写使用不同 DataContext。这种终态短路不能证明整个回调幂等，也没有代码证据证明日志更新与全部业务更新、通知发送处于一个原子事务。[日志回写](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Config/SDK3Base.cs:300)、[控制器分派](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ProcessController.cs:57)。
- 业务回写影响超过审批显示状态。例如律师委托通过时更新案件与审批记录，并继续替换阶段律师；跟进回调中有按案件 GUID 写应收应付明细、更新阶段和发送结案通知的路径。[律师委托](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ProcessController.cs:1611)、[阶段变化示例](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ProcessController.cs:1194)、[明细及通知](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ProcessController.cs:1502)。

### 推断与运行待验证

切换时应对照本地日志 ID、业务 GUID、流程名及平台实例号，明确由哪个系统接收既有实例的后续回调，以及原审批链接如何继续打开。不能仅迁移案件主表或统一替换回调地址就声称“审批保留完成”。这是待决方案约束，尚未选定共库、映射迁移或旧系统承接在途实例中的任何一种。

待验证：各类实际在用流程与版本、发起请求及返回数据形状、平台回调来源认证和 ACK 约定、失败后的重试规则、重复及乱序回调、审批日志成功但业务写回失败的恢复、退回后重新提交是否复用实例、是否需要保留旧表单的编辑/审批视图。对 `dataVersion` 等字段当前是否承担版本控制不得作假设。

## 数据与历史记录关联

### 事实

- `xcfwxt.dbml` 包含 `dat_SuSongAJ` 与 `dat_AnJianLR` 两组案件模型，均有整数自增主键、`SYS_GUID`、`SYS_PARENT_GUID`、登录名与组织字段；子表也有父 GUID 字段。存在两组模型本身不能证明两者都在当前业务中使用，更不能据此合并或删除旧表。[诉讼案件模型](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Data/xcfwxt.dbml:539)、[案件录入模型](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Data/xcfwxt.dbml:4027)、[子表形状](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Data/xcfwxt.dbml:524)。
- 审批关联模型同时含整数 `AnJianID`、字符串 `AnJianGUID`、自身 `SYS_GUID`、审批类别、状态与旧表单 URL；`T_ProcessLogs` 中还有 `FromID`、`FromData`、`OtherJSON`、`AppHistory` 和 `SKD3Data`。DBML 还包含独立审批历史表。保留范围需要核对结构化记录、JSON 快照与外部平台历史之间的关系。[案件审批关联](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Data/xcfwxt.dbml:1105)、[日志模型](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Data/xcfwxt.dbml:1124)、[审批历史模型](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Data/xcfwxt.dbml:1045)。
- 代码实际用审批记录的 `AnJianGUID` 查案件，并用案件 `SYS_GUID` 关联律师明细；附件转换将业务 GUID 写入 `SysPageFiles.PID`，业务字段还可保存包含附件 ID/名称的 JSON 列表。这支持应用层关联的存在，不能证明数据库中每条关联都有效。[案件关联](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ProcessController.cs:1615)、[附件关联](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ProcessController.cs:1585)、[附件 JSON 示例](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ProcessController.cs:1170)。
- 另外存在组织库与审批库的 DBML，审批库模型包含流程名、实例号和启动时间字段。模型存在不证明部署中的物理数据库、读写权限、直连使用频率或 Schema 版本。[组织模型](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Data/CINDERELLAW2.dbml:1)、[审批模型](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Data/Rsun_BPM.dbml:76)。

### 推断与运行待验证

保留历史数据的验收应覆盖案件、阶段、人员、审批、附件及关键金额/时间的关联一致性，不能只比较总行数。是否保留原主键、建立旧新 ID 对照、保留 JSON 原文，以及历史记录是否可继续编辑，需要后续决策。

待验证：当前物理 Schema 与 DBML 差异；表/视图/触发器/存储过程及后台依赖；各业务表记录量与增量变化；重复 GUID、孤儿子记录、删除标记、空值与 JSON 可解析性；不同历史时期状态语义；已离职或不存在账号的历史显示；迁移时写入来源、冻结窗口、对账口径和回退要求。只索取去标识的统计与样本，不以源码推导数据规模或清洁程度。

## 历史附件

### 事实

- `SysPageFiles` 模型区分自身字符串主键 `ID`、业务关联 `PID`、路径 `Path`、类型、大小、`BatchId`、外部整数 `FileID`、预览能力和 URL。元数据记录与文件内容不是同一资产。[附件模型](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/Data/xcfwxt.dbml:864)。
- 预览分支区分 `OA`、`uploadLite` 与旧版文件；OA 预览在该方法里返回空字符串，uploadLite 可直接返回已存预览 URL。旧版附件若尚无 BatchId，会将文件名与 `Server.MapPath` 展开的本地文件交给 `UploadLite.UploadFiles`，并回写预览能力、BatchId、URLPreview、FileID。因此一次“预览验证”可能调用外部服务并更新数据库。[预览分支及写回](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/FileServerController.cs:38)。
- OA 下载方法按当前登录用户获取临时访问凭据并重定向到配置展开的文件地址；其他分支按已存路径生成浏览器打开行为。源码中的上传入口允许任意扩展名并设置 500 MB 大小上限；这些是旧实现参数，尚未确认实际业务规则或代理限制。[下载分支](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/FileServerController.cs:94)、[上传入口](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/FileServerController.cs:25)。

### 推断与运行待验证

附件迁移或兼容必须识别存储类型，并维持“业务字段/附件记录/外部文件”三者的引用，不可假设全部文件都在一个本地目录或全部 URL 永久有效。附件预览测试应在可恢复、与生产隔离的测试副本上进行。

待验证：各类型数量与实际可下载比例、旧物理目录和文件是否完整、UploadLite 文件与批次对应、URL 的有效期及授权、OA 下载是否仍在使用、多文件批次如何对应记录、缺失/同名/大文件表现、历史链接兼容，以及经办人能否读取不属于其授权案件的文件。

## 后台同步与消息入口

### 事实

- 管理程序无参数时调用上月月报计算；有参数时按 `kaiting`、`lvyue`、`shangsuqixian`、冻结到期、投后/重大合同履约、日程与延迟提醒等分派。`ProjectSync.Sync` 与 `MessageBase.Send` 在该 Main 内的出现为注释，不能按注释认定它们仍在调度。[管理程序入口](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.MgrSvr/Program.cs:61)。
- 独立同步程序启动计时器，触发后停止计时器、同步律所、等待后同步甲方并退出。律所及甲方按 `Fid` 更新；律所类型有删除原关联再插入的路径。这是一次进程运行中的实现，不能证明 Windows 上的任务频率或当前部署。[同步入口](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.TongBu/Data_Synchronization/Program.cs:22)、[律所更新](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.TongBu/Data_Synchronization/LvSuoTongBu.cs:185)、[甲方更新](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.TongBu/Data_Synchronization/JiaFangTongBu.cs:192)。
- 另外存在用户/项目同步实现：项目同步在事务内清空 `ESB_PROJECT` 再批量写入；用户同步含清空 `SSO_USER` 和 `DN_USER` 的实现。本轮定位到代码但未发现管理程序 Main 的有效调用，因此它们属于待核实的部署依赖，不能直接列为正在运行的任务。[项目写入](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.MgrSvr/ProjectSync.cs:78)、[用户暂存写入](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.MgrSvr/UserSync.cs:118)、[用户更新](/Users/tony/Documents/我的工作空间/RSun.FaWu/fwxt.Web/fwxt.MgrSvr/UserSync.cs:225)。

### 推断与运行待验证

全面重建的切换设计应盘点 Web 以外的写入者和通知发送者，明确它们是否保留、迁移或调整。需要 Windows 计划任务/服务及其参数、运行账号、调度窗口、最新运行结果、源数据负责人和实际收件人渠道的去敏清单；尤其确认旧新程序是否可能同时写同一数据或重复通知。

## Windows 测试环境最小验证清单（本轮未执行）

| 验证点 | 最小动作与样本 | 应留下的证据 |
|---|---|---|
| 部署基线 | 由环境负责人提供 Web/后台版本、启用模块、逻辑服务名称、任务清单与访问方式；不提供任何秘密值 | 源码/部署版本对应及当前启用分支，未知项责任人 |
| 身份桥接 | 集团法务、经办人、无授权账号各测试登录、注销、超时与重新登录；核对去标识登录名、人员/组织标识 | 当前身份源、映射规则与旧新回跳约束 |
| 授权范围 | 同一去标识案件对照列表、详情、直接接口、导出、附件；至少跨一个部门范围 | 哪些操作允许/拒绝的业务确认表；权限变化生效时机 |
| 审批闭环 | 对当前在用的流程类别列清单；代表流程在隔离测试中走发起、审批中、通过、退回重提、终止 | 去敏请求/回调形状、dataId/业务 GUID/incident 对照、历史与状态前后差异 |
| 回调恢复 | 在可恢复副本中验证重复、乱序及业务回写失败后的重试，通知接收器应隔离 | 是否重复修改明细/阶段/附件或通知；平台 ACK 与重试时序、人工恢复入口 |
| 在途实例 | 只读列举各实际流程的在途数量及状态分布，抽查旧审批链接、旧表单可否继续处理 | 回调归属、表单依赖与实例关联覆盖率；切换方案所缺事实 |
| 历史数据 | 对照当前 Schema，抽取已结案、退回、在途和不同历史年份的去标识记录链 | 表/JSON/主键关联、金额时间及审批历史的对账项；孤儿与异常统计 |
| 历史附件 | 按 OA、UploadLite、旧本地文件取样；仅在隔离副本验证会写回的预览路径 | 文件可用性、关联完整性、权限、预览写回变化及可恢复结果 |
| 后台作业 | 先读取调度及日志，人工确认有效入口；需要执行时用副本与隔离发送渠道 | 当前实际任务及数据写入者、业务日历和消息规则；新旧双运行风险 |

上述清单是下一步待验证工作，不是本轮通过的验收。身份/审批/文件接口的运行证据、历史数据统计及组织平台约束齐备后，才能比较兼容、迁移和切换方案。技术栈、数据迁移路径、审批承接方式与上线窗口均未在此报告中确定。
