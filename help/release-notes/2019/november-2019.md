---
title: Adobe Experience Platform发行说明2019年11月
description: 2019年11月版Adobe Experience Platform发行说明。
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 2%

---

# Adobe Experience Platform 发行说明

**发行日期：2019 年 11 月 18 日**

Adobe Experience Platform的新增功能：
* [[!DNL Real-Time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

现有功能的更新：
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-Time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Real-time Customer Data Platform(Real-Time CDP)构建于Adobe Experience Platform之上，可帮助公司将已知和未知数据汇集在一起，通过智能决策激活客户档案，并贯穿整个客户历程。 Real-Time CDP整合了多个企业数据源以实时创建统一的配置文件，可用于跨所有渠道和设备提供一对一的个性化客户体验。

[!DNL Real-Time Customer Data Platform] 包括数据管理、身份管理、高级分段和数据科学工具，以便您能够构建用户档案并定义受众，以及在实施严格的数据管理策略的同时获得丰富的洞察信息。

Adobe可连接到大型合作伙伴生态系统，更不用说与Adobe Experience Cloud的本机集成，这样您就可以无缝激活这些受众，并跨所有渠道提供出色的客户体验，从现场或应用程序内个性化到电子邮件、付费媒体、呼叫中心、连接设备等。

通过Real-Time CDP，您可以：

* 通过从整个企业流式收集客户数据，实现客户的单一视图。
* 对已知和未知标识符使用可信的管理和隐私控制负责地管理用户档案。
* 借助由Adobe Sensei提供支持并为营销人员构建的AI和机器学习功能，生成可操作的洞察并扩展受众。
* 跨所有渠道和目标实时提供个性化体验。

有关更多信息，请参阅 [Real-time Customer Data Platform文档](../../rtcdp/overview.md).

**主要功能**

| 功能 | 描述 |
|---|---|
| 目标 | 预先构建的与受Adobe支持的目标平台的集成 [!DNL Real-Time Customer Data Platform] 可无缝地向这些合作伙伴激活数据。 请参阅 [目标](#destinations) 下面以了解更多信息。 |
| 主页量度功能板 | Real-time Customer Data Platform(Real-Time CDP)主页包含一个量度功能板，用于显示有关用户档案和区段的信息。 主页还包含指向学习材料的链接。 请参阅 [Real-time Customer Data Platform量度](#real-time-customer-data-platform-metrics) 下。 |
| 源 | 您可以从各种来源摄取数据，如Adobe解决方案、基于云的存储、第三方软件和您的CRM。 请参阅 [源](#sources) 部分以了解更多信息。 |

**[!DNL Real-Time Customer Data Platform]量度**

登录Real-time Customer Data Platform(Real-Time CDP)时，会显示该主页（其中包含量度功能板）。

主页只是显示量度卡的位置之一。 Real-Time CDP会在您的整个体验中提供量度卡。 这些量度可告知您系统中的数据、用户档案和区段受众。

如果您登录Real-Time CDP时系统中没有数据，则主页上的功能板不会显示。 在这种情况下，主页会首次提供用户体验的学习材料。 收集数据时，功能板会自动更新以显示有关该数据的信息。

要了解更多信息，请参阅 [Real-time Customer Data Platform量度概述](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是与由Adobe Real-time Customer Data Platform支持的目标平台的预建集成，可无缝地向这些合作伙伴激活数据。 有关更多信息，请阅读 [目标概述](../../destinations/home.md) 文章。

**可用目标**

在11月版中，Adobe的Real-time Customer Data Platform支持以下目标：

* 广告: [!DNL Google]
* 电子邮件营销：Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

请参阅 [目标目录](../../destinations/catalog/overview.md) 以了解有关每个目标的信息。

**已知限制**

* 在初始版本中，不提供允许在激活流程（计划步骤）中执行自定义激活计划的控件。
* 当前无法编辑或删除目标配置。 要绕过此限制，您可以在 [目标详细信息页面](../../destinations/ui/destination-details-page.md).
* 连接到目标或存储帐户时，当前没有验证帐户详细信息、路径或凭据。 确保输入正确的凭据并对拼写错误或拼写错误进行复查。
* 在初始版本中，没有进行凭据续订。 帐户过期或需要刷新后，必须创建新的目标连接并重新映射之前映射的区段。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用 [!DNL Platform] 服务。 您可以从各种来源摄取数据，如Adobe解决方案、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform] 提供了RESTful API和交互式UI，让您能够轻松为各种数据提供程序设置源连接。 这些源连接允许您对存储系统和CRM服务进行身份验证，设置摄取运行的时间，并管理数据摄取吞吐量。

**主要功能**

| 功能 | 描述 |
| ---------- | ------------ |
| 源UI | 用于创建、查看和管理源连接的新用户界面。 |
| 改进了CRM连接器的工作流 | 用于创建和管理的全新直观UI工作流 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce] 连接器。 |
| 对基于云的存储的连接器支持 | 连接器现在可以访问基于云的存储。 新来源包括 [!DNL Amazon S3], [!DNL Azure Blob]和FTP/SFTP服务器。 |

**已知问题**

* 基于云的存储的源连接器不支持摄取压缩文件。

有关源的详细信息，请参阅 [源概述](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] 通过构建和运行机器学习模型，使数据科学家能够跨Adobe应用程序和第三方系统从数据和内容无缝地生成洞察。 [!DNL Data Science Workspace] 与 [!DNL Platform] 并支持端到端数据科学的生命周期，包括探索和准备XDM数据，随后开发和实施模型以自动丰富 [!DNL Real-Time Customer Profile] 和机器学习分析。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 使用 [!DNL Platform] SDK | 中预建的脚本和启动器笔记本 [!DNL Python] 现在使用 [!DNL Platform] 用于访问数据的SDK。 |
| 支持沙箱 | 支持即将推出的沙盒功能（目前为测试版），包括将笔记本电脑和方法隔离到开发或生产沙箱中的功能。 请参阅 [沙箱概述](../../sandboxes/home.md) 以了解更多信息。 |

有关更多信息，请参阅 [数据科学工作区概述](../../data-science-workspace/home.md).

## [!DNL Experience Data Model] (XDM)系统 {#xdm}

标准化和互操作性是其背后的关键概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)在Adobe的驱动下，努力标准化客户体验数据并定义客户体验管理架构。

XDM是一项公开记录的规范，旨在提高数字体验的强大功能。 它为任何与Adobe Experience Platform上的服务通信的应用程序提供了通用结构和定义。 通过遵循XDM标准，所有客户体验数据都可以整合到通用呈现形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
| ---------- | ------------ |
| 通知架构 | 表示在数据摄取过程中发送的通知数据的新架构。 |
| AdobeAdCloud DSP架构 | 添加了五个新架构来表示Adobe Advertising Cloud需求方平台(DSP)元数据：版面、促销活动、包、广告商、帐户。 |
| ExperienceEvent实施详细信息架构字段组 | 新增了ExperienceEvent字段组，用于添加标准字段以存储有关用于收集事件的软件的信息。 |
| [!DNL Profile Privacy] 字段组 | 新增了用户档案字段组，用于添加字段以接受的常规退出和销售/共享选择退出信号 [!DNL Real-Time Customer Profile]. |
| 格式约束 `xdm:alternateDisplayInfo` | 的“标题”和“描述”字段 `xdm:alternateDisplayInfo` 必须两者都是字符串才能通过验证。 |
| 名称更改：XDM [!DNL Individual Profile] | XDM的“标题” [!DNL Profile]“ ”类已更新为“ XDM” [!DNL Individual Profile]&quot; 正式 `$id` 班级没有变。 |

**已知问题**

* None.

要了解有关使用XDM的更多信息，请使用 [!DNL Schema Registry] API和 [!DNL Schema Editor] 用户界面，请阅读 [XDM系统文档](../../xdm/home.md).

## [!DNL Real-Time Customer Profile] {#profile}

Adobe Experience Platform使您能够为客户在何处或何时与您的品牌进行交互，从而提供协调、一致的相关体验。 使用 [!DNL Real-Time Customer Profile]，您可以看到每个客户的整体视图，该视图将来自多个渠道的数据（包括在线、离线、CRM和第三方数据）进行合并。 [!DNL Profile] 允许您将不同的客户数据整合到统一视图中，为每次客户互动提供一个可操作且带有时间戳的帐户。

| 功能 | 描述 |
| -----------| ---------- |
| 增强了 [!DNL Profile] 对照 | 用户现在能够使用引用描述符和相关实体查找用户档案。 |
| 清理给定数据集的数据 | 用户现在可以使用 [!DNL Profile] 系统作业API。 |
| Edge [!DNL Profile] 查询增强功能 | 应用程序现在可以查询边缘 [!DNL Profile] 任何给定用户档案的身份。 |
| 为每个投影配置合并策略 | 现在，应用程序可以针对每个投影配置合并策略，以便生成由特定合并策略管理的数据视图。 |
| 计算属性 | 计算属性会根据其他值、计算和表达式自动计算字段的值。 计算属性在配置文件级别上运行，以根据传入事件、传入事件和配置文件数据或传入事件、配置文件数据和历史事件聚合“总购买”、“生命周期值”或“漏斗状态”等值。 |

**错误修复**

* 合并策略创建工作流中可用ID拼合策略的简化列表。

**已知问题**

* None.

有关 [!DNL Real-Time Customer Profile]，包括使用的教程和最佳实践 [!DNL Profile] 数据，请阅读 [实时客户资料概述](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] 提供了用户界面和RESTful API，允许您从中构建区段并生成受众 [!DNL Real-Time Customer Profile] 数据。 这些区段在上集中配置和维护 [!DNL Platform]，以便任何Adobe应用程序都可轻松访问。

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准来定义特定的用户档案子集。 区段可以基于记录数据（如人口统计信息）或表示客户与您的品牌交互的时间序列事件。

| 功能 | 描述 |
| -----------| ---------- |
| 计划分段 | 用户现在可以通过UI和API为所有区段启用计划区段评估。 启用后，所有区段将每天评估一次。 这不会影响按需分段功能，这些功能可继续像以前一样使用。<br/><br/>注意：计划分段功能不能用在具有五个以上合并策略的沙箱中， [!DNL XDM Individual Profile]. |
| 流分段 | 支持持续评估区段（流式分段），在数据传入时，可以评估大多数区段规则 [!DNL Platform]. 此功能意味着区段成员资格将保持为最新状态，而无需运行计划的分段作业。 某些例外适用，例如使用多实体关系或具有扩充负载的区段。 |
| 区段作为构建基块 | 现在，使用区段生成器UI创建区段时，用户可以将之前定义的区段用作其他区段的构建基块。 <ul><li>引用当前受众成员资格：当人员进出受众时进行更新。</li><li>复制逻辑：获取选定的区段定义，并将其复制到新区段中。</li></ul> |
| 按ID命名空间查看区段成员资格 | 现在，可以通过ID命名空间（电子邮件、ECID和总计数）查看区段成员资格。 |
| RBAC支持 | 区段生成器现在支持基本的基于角色的访问控制和权限。 |
| 增强了对外部受众在之间共享的支持 [!DNL Platform] 和Adobe解决方案 | 用户现在可以引入外部(非[!DNL Experience Platform])受众元数据。 此版本包括 [!DNL Audience Manager] 元数据。 此受众元数据可在区段生成器中使用，以创建新 [!DNL Experience Platform] 区段。 <br/><br/> 此外，在 [!DNL Experience Platform] 现在可用于集成Adobe解决方案，包括 [!DNL Audience Manager], [!DNL Target]和 [!DNL Ad Cloud]. |

**错误修复**

* 修复了导致多实体分段在嵌套关系情况下返回零用户档案的问题。
* 修复了排除逻辑返回误导性结果的问题。
* 提高了多实体文件夹的可读性。 现在，它们显示XDM类的易记名称。
* 修复了显示同一XDM文件夹的多个副本的间歇性问题。
* 现在产生消息以在区段估计对所选合并策略不可用时通知用户。

**已知问题**

* None.

详细了解 [!DNL Segmentation Service]，请阅读 [Segmentation Service概述](../../segmentation/home.md).
