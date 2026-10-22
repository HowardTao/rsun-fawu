# 旧法务系统业务与权限基线

研究日期：2026-10-21。旧代码根目录：`/Users/tony/Documents/我的工作空间/RSun.FaWu/`。

## 结论与证据边界

旧系统实现范围覆盖案件与诉讼、查封冻结、律所律师与委托、清欠、多种非诉事务、法律联系单、法务绩效、知识文件与报表，还包含独立消息和主数据同步程序。下面按实际控制器、页面控件、保存事件、数据访问和后台调用整理出处，供全面重建的业务清单讨论使用。

本报告是有限静态抽样，未运行旧程序、连接业务数据库或接口，也未访问配置中的密钥值。实现存在不代表当前生产启用，也不代表流程已被完整核实。菜单用于发现候选业务，不能证明当前使用情况；组件引用不能证明当前运行架构。未全面检查每个字段、接口、保存规则和状态转换，不能将本报告称为已经验收的“完整业务全集”。

用户已确认的规划约束是：首期全面重建产品和架构，先重构完整业务功能；MCP/AI 的具体场景后续规划；主要用户为集团法务和业务经办人；现有登录、审批平台和历史数据必须保留。以上是用户决策，不是代码推断。本报告不决定新产品范围、技术栈、业务调整或术语定义。

## 主要业务覆盖与实际证据

### 案件、诉讼与查封冻结

- **案件立项与业务阶段变化。** [LiuChengController.cs:68](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/LiuChengController.cs#L68) 的 `AnJianLiXiangProcess` 读取 `dat_AnJianLR`，行 79–96 检查已有流程并发起诉讼立项审批。[ProcessController.cs:664](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ProcessController.cs#L664) 的立项回调在行 706–718 写立项时间、审批状态和案件步骤，按仲裁标记进入“仲裁中”或“一审中”；行 726 起写诉讼目标与下一步计划子表。已证实审批结果会驱动案件状态与数据变化；全部立项校验、驳回重提和后续阶段转换未全面核实。
- **案件关联对象与第一代理人约束。** [AnJianController.cs:94](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/AnJianController.cs#L94) 行 101–107 查询同案件已有“第一代理人”，检测重复；行 121–122 查询案发单位和对方当事人。已证实存在多对象案件结构和代理人校验方法；所有入口是否调用该校验、是否有数据库约束待验证。
- **账户冻结数据与关联提醒。** [AnJianController.cs:31](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/AnJianController.cs#L31) 查询 `dat_AnJianCFGL_ShuJuZX`，行 69–80 返回申请人、申请/实际冻结金额、到期日与匹配状态；行 123–139 根据案件标记与案发单位匹配生成可能冻结的提醒。代码中部分当事人匹配条件已注释，不能将注释中的“当事人模糊匹配”当成有效规则。数据中心上游来源、主诉/被诉查封完整流程与匹配质量待核实。
- **跟进、结案与执行存在审批入口和数据结构。** [ProcessController.cs:65](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ProcessController.cs#L65) 将诉讼跟进回调分派到 `WeiHuCallBack`；[SDK3Base.cs:156](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Config/SDK3Base.cs#L156) 定义结案执行的应收、应付、履行期限、执行完毕及律师评价回写字段。[MainConfigMenu.cs:43](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Config/MainConfigMenu.cs#L43) 另列再审、结案执行、协助执行、督办、人民来信等候选入口。这里前两项证实实际回调与结构，后者仅属导航证据；不能认定各项已完整核实。

### 律所、律师与合作委托

- **律师库导入及组织身份关联。** [LvShiController.cs:28](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/LvShiController.cs#L28) 行 34–37 检查“律所事务管理员”；行 49–54 排除已有未删除账号，行 67–71 从 W2 人员数据取联系方式并写入 `LvShi`。是否允许外部律所人员直接登录、当前律师账号来源及完整启停用规则待确认。
- **案件律师委托。** [LiuChengController.cs:1462](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/LiuChengController.cs#L1462) 参数包含委托起止阶段、金额、框架合同和收费模式；行 1487–1500 检查律师选择，以非 `HongYang` 律所识别外部律师，并根据内部承办法务区分共同/外部代理。行 1620–1626 构造案件律师委托审批。费用规则、变更撤销、各阶段委托重叠与合同校验未全面核实。
- **独立律所合作委托。** [LiuChengController.cs:2113](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/LiuChengController.cs#L2113) 读取 `LvSuo_WeiTuo`，行 2145–2151 生成框架合同查看链接；行 2154–2163 联查委托律师和联系方式；行 2165–2178 将附件批次加入审批并调用 SDK3。它不是仅有律所主数据维护，也有合作事项记录。框架合同系统的权威来源与委托结算全过程待确认。
- **律师评价。** [LvShiController.cs:190](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/LvShiController.cs#L190) 行 202–209 更新专业能力、执行态度、案件结果、评价说明与总分，权重为 0.4/0.25/0.35。只证实该方法的计算行为，不能确定这仍是有效业务口径。

### 清欠

- **接收、接收人变更与操作日志。** [QingQianController.cs:25](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/QingQianController.cs#L25) 修改 `T_E_OWEROOM` 接收法务并写日志；行 54–87 的接收方法更新状态、接收日期和当前人员，并调用 `QingQianApi.updateYQRasonSp` 回写明源状态。[ProcessController.cs:1837](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ProcessController.cs#L1837) 实现清欠退回审批回调，行 1877 调明源回写。清欠含跨系统操作，不只是本地列表。移交、解决、退房完整条件、外部写回失败补偿与实际生产接口待核实。

### 非诉事务、合同与投融资

- **综合法律事务。** [FLZHSWController.cs:11](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/FLZHSWController.cs#L11) 按城市公司、城市与资质登记标记查询 `dat_ZHFLSW`，组合承办人与项目名称。[MainConfigMenu.cs:110](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Config/MainConfigMenu.cs#L110) 指向录入与量化评估入口。查询行为已证实，量化评估公式与地产/商业口径尚未核实。
- **合同查询与履约台账。** [ContractController.cs:13](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ContractController.cs#L13) 查询供应商编码对应且 `ContractType == 1` 的 `dat_Contract`。结合委托方法的框架合同字段，可确认存在框架合同关联，但不能据此推断完整合同起草/签署功能。[AnJianLY.cs:336](../../../../RSun.FaWu/fwxt.Web/fwxt.MgrSvr/AnJianLY.cs#L336) 行 342–348 联查重大合同履约主/明细表和应办结期限，行 367–378 写站内消息并发钉钉。常规合同登记、主数据来源和重大合同完整流程待进一步核实。
- **投融资与投后履约。** [LiuChengController.cs:2226](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/LiuChengController.cs#L2226) 实现投融资律师委托申请。[TouRongZiXMGL_LY.aspx:13](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/TouRongZiXMGL_LY.aspx#L13) 绑定 `dat_TouRongZiXMGL_LY`，行 14–22 包含事项描述、合同依据、应办结期限、进展、办结标记/日期与附件。项目立项、合同履约联动、投后审批全部路径未全面核实。
- **培训事务。** [PeiXunSWGL.aspx:42](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/PeiXunSWGL.aspx#L42) 绑定 `dat_PeiXunSWGL`，行 45–65 提供课程、事务归属、培训对象/类别、人数、时间、培训人、地点、情况说明及附件。[PeiXunSWGL.aspx.cs:27](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/PeiXunSWGL.aspx.cs#L27) 新建时默认经办人。已证实登记表单和加载行为；保存能力依赖表单组件，其完整行为与生产使用情况未运行验证。
- **制度、指引与专题事务。** [ZhiDuZYZTSWGL.aspx:42](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/ZhiDuZYZTSWGL.aspx#L42) 绑定对应数据表，行 50–63 提供分类、名称、成果级别、内容和附件；[ZhiDuZYZTSWGL.aspx.cs:27](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/ZhiDuZYZTSWGL.aspx.cs#L27) 默认经办人。这里证实成果登记界面，不能认定包含文件审批发布全过程。
- **知识产权登记。** [ZhiShiCQGL_ZLDJ.aspx:42](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/ZhiShiCQGL_ZLDJ.aspx#L42) 绑定专利登记表，行 52–61 提供申请和类型信息；行 70–93 包含状态、授权证书、有效期、许可/出质、年费及附件。[MainConfigMenu.cs:139](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Config/MainConfigMenu.cs#L139) 另列商标、美术著作权、域名和软件著作权，四类仅作候选覆盖项；本轮深入抽样的是专利表单。状态选项不证明合法转换规则或自动到期提醒已实现。
- **行政处罚与其他非诉事项。** [XingZhengCFGL.aspx:42](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/XingZhengCFGL.aspx#L42) 绑定行政处罚表，行 55–77 提供处罚单位/类型/时间、金额、决定书及附件；行 86–95 提供进展、结果、已付未付金额和执行完毕标记。该页行 43 的 `PageType` 写成“重大合同履约监控新建”，与其实际字段不同，应核实是否只是复制遗留或影响日志，不能用它命名业务。[QiTaFSSWGL.aspx:42](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/QiTaFSSWGL.aspx#L42) 绑定其他非诉事务表，行 55–60 提供类别、经办人、登记时间、事项说明和附件。

### 法律联系单、绩效、文件与报表

- **法律事务审批与联系单。** [ProcessController.cs:89](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ProcessController.cs#L89) 分派法律事务审批、诉讼业务/执行联系单、法务联系单及验收回调。[LiuChengController.cs:1219](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/LiuChengController.cs#L1219) 与行 1304 分别实现法务联系单申请和验收申请。发起及回调入口存在；责任交接、协办/抄送、验收条件与超期规则待完整核实。
- **重大业绩评分有保存前状态变化。** [ZhongDaYJPF.aspx.cs:23](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/ZhongDaYJPF.aspx.cs#L23) 将“待评分”改为“已初评”，并把初审分赋给复审分；原为“已初评”则改为“已复核”。[MainConfigMenu.cs:178](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Config/MainConfigMenu.cs#L178) 另列重大业绩申报/评分/汇总。评分动作已证实，申报周期、分值公式与审核授权待确认。
- **法律文件库与诉讼综合报表嵌入外部页面。** [FaLvGJK.aspx:11](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/FaLvGJK.aspx#L11) 的 iframe 指向法务域名下 `fmapp` 文件应用；[SuSongAJZHBB.aspx:24](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/SuSongAJZHBB.aspx#L24) 的 iframe 指向报表服务 `.cpt` 页面。已证实嵌入方式，无法从此页确定外部功能、数据口径、权限与部署。[MainConfigMenu.cs:164](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Config/MainConfigMenu.cs#L164) 中旧制度库、旧工具库、判例库及更多报表也应进入业务清单确认，不能按“旧”字样直接判为废弃。

## 角色、权限与组织模型

| 已证实机制 | 代码证据 | 尚未确定 |
| --- | --- | --- |
| 当前权限按登录名或所属部门匹配 | [PowerMgr.cs:31](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Code/Helper/PowerMgr.cs#L31)，行 35–38 | 每个页面/API 是否执行检查，跨部门任职与组织变更后的效果 |
| `SysPowerSetting` 保存权限类型、菜单、目标组织和允许用户/组织 | [PowerMgr.cs:55](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Code/Helper/PowerMgr.cs#L55)，行 61–73 | 生产授权记录、例外授权、默认拒绝和管理员旁路 |
| 授权组织会按部门路径扩展 | [PowerMgr.cs:96](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Code/Helper/PowerMgr.cs#L96)，行 99–103 用 `FNumber.Contains` 和可见标记取组织 | 是否准确表达业务要求的“本组织及下级”，组织路径特殊值是否误匹配 |
| 权限类型含菜单、督办、工作台、法律审批、清欠及其他数据查看 | [MainConfig.cs:62](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Config/MainConfig.cs#L62)，行 64–73 | 查看/修改/分享/导出权限的完整矩阵 |
| 律师导入另查 `FWPDRSet` 的“律所事务管理员” | [LvShiController.cs:34](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/LvShiController.cs#L34) | 所有法务业务角色、角色兼任、角色与组织范围交叉规则 |
| 表单可默认当前组织人员为经办人 | [PeiXunSWGL.aspx.cs:27](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Forms/HongYang/PeiXunSWGL.aspx.cs#L27) | 是否允许修改经办人、经办人与承办人/审批人的业务区别 |

以上机制说明权限不是单一“管理员/普通用户”二分。集团法务与业务经办人是用户确认的新产品主要用户群，不能直接等同于代码中的授权类型或角色字符串。准确身份和授权矩阵需要生产角色配置、业务责任清单及真实用户用例共同确认。

## 登录、审批、附件与后台任务

| 实际入口与行为 | 证据 | 重建前需要验证的事实 |
| --- | --- | --- |
| SSO handler 无 ticket 时跳登录，有 ticket 时调用 CAS 式验证，返回 `yes` 后按账号登录 | [SSO.ashx.cs:34](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/SSO.ashx.cs#L34)，行 43–77 | 当前生产主入口、协议版本、账号唯一标识、注销与会话失效策略 |
| SDK3 POST 发审批；先写流程日志，成功后写实例与状态 | [SDK3Base.cs:201](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Config/SDK3Base.cs#L201)，行 208–220 和 235–290 | 必须保留平台的实际接口契约、流程定义/版本、在途流程和平台权威数据 |
| 审批回调保存结果/历史并按流程名反写业务数据 | [SDK3Base.cs:300](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/Config/SDK3Base.cs#L300)，[ProcessController.cs:49](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/ProcessController.cs#L49) | 鉴权、重放/重复回调、回调失败恢复、状态一致性；本轮未作安全或完整性审计 |
| 附件按 OA、uploadLite、旧本地文件分支处理；预览旧文件会上传并写回元数据 | [FileServerController.cs:38](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/FileServerController.cs#L38)，行 46–85 | 各类存储数量、文件资产可用性、访问控制、迁移后老链接兼容 |
| 分享创建记录与压缩包，写一天启用期限，并有下载日志 | [FileShareController.cs:44](../../../../RSun.FaWu/fwxt.Web/fwxt.Web/MVC/Controllers/FileShareController.cs#L44)，行 81–89；行 29 写日志 | 期限是否真正执行、分享权限及外部使用方式 |
| 后台以命令参数执行开庭/履约/上诉/查封冻结/投后/合同/延迟提醒及日历 | [MgrSvr/Program.cs:80](../../../../RSun.FaWu/fwxt.Web/fwxt.MgrSvr/Program.cs#L80)，行 82–115 | Windows 任务计划或其他调度配置、执行频率、漏发/重复处理与责任人 |
| 消息会写 `SysMsgs` 并调用钉钉；另有企业微信消息路径 | [AnJianLY.cs:367](../../../../RSun.FaWu/fwxt.Web/fwxt.MgrSvr/AnJianLY.cs#L367)，[AnJianLY.cs:565](../../../../RSun.FaWu/fwxt.Web/fwxt.MgrSvr/AnJianLY.cs#L565)，[DelayMsg.cs:83](../../../../RSun.FaWu/fwxt.Web/fwxt.MgrSvr/DelayMsg.cs#L83) | 当前实际启用通道、接收人规则、消息送达和历史消息迁移要求 |
| 人员程序分页取外部人员，读 `SSO_USER`，再重建 `DN_USER` | [UserSync.cs:21](../../../../RSun.FaWu/fwxt.Web/fwxt.MgrSvr/UserSync.cs#L21)，行 178、226 | 主数据权威、组织数据同步链路、失效人员处理与新旧并行时写入职责 |
| 独立同步程序调用律所和甲方同步；律所以最近录入日期查增量 | [Data_Synchronization/Program.cs:49](../../../../RSun.FaWu/fwxt.TongBu/Data_Synchronization/Program.cs#L49)，行 55；[LvSuoTongBu.cs:125](../../../../RSun.FaWu/fwxt.TongBu/Data_Synchronization/LvSuoTongBu.cs#L125)，行 135–155 | 主数据上游、增量游标正确性、同步频率、错误恢复与历史数据规模 |

抽样审批路径是 SDK3 服务调用；仅有 Ultimus 组件引用不足以说明当前仍直连 Ultimus。外部文件库、报表页、通知组件存在也不足以说明其目前可用。保持现有平台需要确认正在运行的协议与资产，而不能只复制代码依赖列表。

## “完整业务”还需确认的业务清单

为了覆盖用户要求的完整业务功能，应由业务方确认以下清单，再将遗漏逐项补充调查。本节列证据缺口，不替业务方决定取舍或缩减首期。

1. **使用清单与责任人。** 每个主要业务域、子功能、角色和日常操作是否仍使用；菜单外入口、批处理、Excel 导入导出、人工台账及线上新功能是否存在。
2. **完整场景与规则。** 为每域提供从创建到结束的实际样例，包含修改、退回重提、撤销、移交、删除/恢复、共享与异常处理；明确字段校验、编号、金额、日期、阶段及通知规则。案件再审/结案执行、主诉/被诉查封、清欠退房、律师费用、绩效等尚需逐链路核实。
3. **角色与数据范围。** 提供现有有效角色/权限配置及代表性账号，确认集团、产业集团、城市公司、项目等范围和跨组织授权；区分查看、修改、审批、导出、分享及后台管理权限。
4. **平台与流程定义。** 提供现有登录、审批、组织、合同、明源、文件、报表、通知平台的运行入口和可用测试条件，确认流程版本、节点规则、在途实例与历史审批记录如何继续访问。
5. **历史资产目录。** 确认各业务表、关联 GUID/ID、附件本地与外部存储、分享链接、操作日志、审批历史、消息和报表的数量、时间范围、质量及保留期限。“保留历史数据”不能只统计主表。
6. **后台作业清单。** 导出实际 Windows 调度/部署配置和运行日志，确认人员/组织、律所、甲方、提醒与日历等任务及其他数据库作业；代码中的分支不代表每项都被调度。
7. **口径与基准样本。** 确认诉讼、清欠、合同、综合法律事务、绩效报表口径及样本结果。嵌入外部报表意味着只读 Web 源码可能无法得到完整计算规则。

以上核实完成后才能形成可供全面重建规格使用的功能覆盖表、权限矩阵和历史资产基线。本研究报告可作为其起点，不代替业务确认、测试环境演示或下一步接口调查。
