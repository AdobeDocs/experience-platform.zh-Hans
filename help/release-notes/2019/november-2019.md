---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2019年11月18日
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 2%

---

# Adobe Experience Platform 发行说明

**发行日期：2019 年 11 月 18 日**

Adobe Experience Platform的新增功能：
* [[!DNL Real-time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

对现有功能的更新：
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-time Customer Data Platform] {#rtcdp}

实时客户数据平台(Real-time CDP)以Adobe Experience Platform为构建基础，可帮助公司将已知和未知的数据整合在一起，通过在整个客户旅程中的智能决策激活客户用户档案。 实时CDP将多个企业用户档案源组合在一起，以实时创建统一的数据，这些数据可用于在所有渠道和设备上提供一对一的个性化客户体验。

[!DNL Real-time Customer Data Platform] 包括用于数据治理、身份管理、高级细分和数据科学的工具，使您能够构建用户档案和定义受众，并在实施严格数据治理策略的同时获得丰富的洞察。

Adobe连接到一个大型合作伙伴生态系统，更不用说与Adobe Experience Cloud的本机集成了，因此您可以无缝激活这些受众，并在所有渠道（从现场或应用程序内个性化到电子邮件、付费媒体、呼叫中心、互联设备等）提供出色的客户体验。

利用实时CDP，您可以：

* 通过从整个企业内的流式收集客户数据，实现客户的单一视图。
* 对已知和未知的标识符进行可信治理和隐私控制，以负责任的方式管理用户档案。
* 借助以Adobe Sensei为后盾并为营销人员构建的AI和机器学习，生成可操作的洞察并扩展受众。
* 在所有渠道和目标中实时提供个性化体验。

有关详细信息，请参阅[实时客户数据平台文档](../../rtcdp/overview.md)。

**主要功能**

| 功能 | 描述 |
|---|---|
| 目标 | 预建与受Adobe[!DNL Real-time Customer Data Platform]支持的目标平台集成，以无缝方式将数据激活给这些合作伙伴。 有关详细信息，请参阅下面的[目标](#destinations)。 |
| 主页量度仪表板 | 实时客户数据平台（实时CDP）主页包括一个指标仪表板，其中显示了有关用户档案和细分的信息。 该主页还包含指向学习材料的链接。 请参见下面[实时客户数据平台量度](#real-time-customer-data-platform-metrics)的部分。 |
| 源 | 您可以从各种来源收集数据，如Adobe解决方案、基于云的存储、第三方软件和您的CRM。 请参阅下面的[源](#sources)部分以了解更多信息。 |

**[!DNL Real-time Customer Data Platform]指标**

“实时客户数据平台（实时CDP）”主页，在您登录到实时CDP时，会显示该仪表板，其中包括一个量度数据。

主页只是显示量度卡的位置之一。 实时CDP可在您的整个体验中提供量度卡。 这些量度会通知您系统中的数据、用户档案和细分受众。

如果登录到实时CDP时系统中没有数据，则不会显示主页上的仪表板。 在这种情况下，该主页将首次提供学习材料以用于用户体验。 在收集数据时，仪表板会自动更新以显示有关该数据的信息。

要了解更多信息，请参阅[实时客户数据平台量度概述](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是预建的与目标平台的集成，由Adobe的实时客户数据平台支持，以无缝方式向这些合作伙伴激活数据。有关详细信息，请阅读[目标概述](../../destinations/home.md)文章。

**可用目标**

在11月的发布中，Adobe的实时客户数据平台支持以下目标：

* 广告: [!DNL Google]
* 电子邮件营销：Adobe Campaign、[!DNL Salesforce Marketing Cloud]、[!DNL Responsys]、[!DNL Oracle Eloqua]

有关每个目标的信息，请参见[目标目录](../../destinations/catalog/overview.md)。

**已知限制**

* 在初始发行版中，不提供允许在[激活流](../../destinations/ui/activate-destinations.md#activate-data)(计划步骤)中进行自定义计划的控件。
* 当前无法编辑或删除目标配置。 要绕过此限制，您可以启用或禁用[目标详细信息页面](../../destinations/ui/destination-details-page.md)右上角的目标。
* 连接到目标或存储帐户时，当前没有帐户详细信息、路径或凭据的验证。 请确保输入正确的凭据并对拼写错误或打字错误进行多次检查。
* 在初始版本中没有进行凭据续订。 帐户过期或需要刷新后，您必须创建新的目标连接并重新映射之前映射的区段。

## 源 {#sources}

Adobe Experience Platform可以从外部源收集数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强该数据。 您可以从各种来源收集数据，如Adobe解决方案、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform] 提供RESTful API和交互式UI，让您可以轻松为各种数据提供者设置源连接。这些源连接允许您对存储系统和CRM服务进行身份验证，设置摄取运行的时间，并管理数据摄取吞吐量。

**主要功能**

| 功能 | 描述 |
| ---------- | ------------ |
| 源UI | 用于创建、查看和管理源连接的新用户界面。 |
| 改进了CRM连接器的工作流 | 用于创建和管理[!DNL Microsoft Dynamics]和[!DNL Salesforce]连接器的新的直观UI工作流。 |
| 对基于云的存储的连接器支持 | Connectors现在可以访问基于云的存储。 新源包括[!DNL Amazon S3]、[!DNL Azure Blob]和FTP/SFTP服务器。 |

**已知问题**

* 用于基于云的存储的源连接器不支持获取压缩文件。

有关源的详细信息，请参阅[源概述](../../sources/home.md)。

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace]通过构建和运行机器学习模型，使数据科学家能够跨Adobe应用程序和第三方系统无缝地从数据和内容生成洞察。 [!DNL Data Science Workspace] 与端对端数 [!DNL Platform] 据科学生命周期紧密集成并为其提供强大动力，包括探索和准备XDM数据，然后开发并实施模型以自动利用机器学习 [!DNL Real-time Customer Profile] 洞察丰富内容。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 使用[!DNL Platform] SDK访问数据 | [!DNL Python]中预建的菜谱和启动器笔记本现在使用[!DNL Platform] SDK访问数据。 |
| 沙箱支持 | 支持即将推出的沙箱功能（目前为测试版），包括将笔记本电脑和方法隔离到开发或生产沙箱的功能。 有关详细信息，请参阅[沙箱概述](../../sandboxes/home.md)。 |

有关详细信息，请参阅[数据科学工作区概述](../../data-science-workspace/home.md)。

## [!DNL Experience Data Model] (XDM)系统  {#xdm}

标准化和互操作性是[!DNL Experience Platform]背后的关键概念。 [!DNL Experience Data Model] (XDM)由Adobe驱动，旨在实现客户体验数据标准化并定义客户体验管理模式。

XDM是一个公开存档的规范，旨在提高数字体验的强大功能。 它为任何与Adobe Experience Platform上的服务通信的应用程序提供了通用结构和定义。 通过遵守XDM标准，所有客户体验数据都可以整合到以更快、更集成的方式提供洞察的常见表现形式中。 您可以从客户行动中获得宝贵的洞察，通过细分定义客户受众，并将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
| ---------- | ------------ |
| 通知模式 | 新模式，表示在数据获取过程中发送的通知数据。 |
| Adobe AdCloud DSP模式 | 已添加五个新模式来表示Adobe Advertising Cloud需求侧平台(DSP)元数据：版面、活动、包、广告商、帐户。 |
| “ExperienceEvent实施详细信息”模式字段组 | 新的ExperienceEvent字段组，可添加一个标准字段以存储有关用于收集事件的软件的信息。 |
| [!DNL Profile Privacy] 字段组 | 新的用户档案字段组，添加字段以接受[!DNL Real-time Customer Profile]的常规退出和销售/共享退出信号。 |
| `xdm:alternateDisplayInfo`的格式约束 | `xdm:alternateDisplayInfo`的“标题”和“说明”字段必须都是通过验证的字符串。 |
| 名称更改：XDM [!DNL Individual Profile] | “XDM [!DNL Profile]”类的“title”已更新为“XDM [!DNL Individual Profile]”。 类的正式`$id`未更改。 |

**已知问题**

* None.

要进一步了解如何使用[!DNL Schema Registry] API和[!DNL Schema Editor]用户界面使用XDM，请阅读[ XDM系统文档](../../xdm/home.md)。

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform使您能够在客户与您的品牌互动的任何地方或何时为其提供协调一致的相关体验。 通过[!DNL Real-time Customer Profile]，您可以看到每个客户的整体视图，该客户综合了来自多个渠道的数据，包括在线、离线、CRM和第三方数据。 [!DNL Profile] 允许您将不同的客户数据整合到一个统一的视图中，为每次客户互动提供一个可操作、有时间戳的帐户。

| 功能 | 描述 |
| -----------| ---------- |
| 对[!DNL Profile]查找的增强 | 用户现在能够使用引用描述符和相关实体查找用户档案。 |
| 清除给定数据集的数据 | 用户现在可以使用[!DNL Profile]系统作业API删除给定数据集或批处理的数据。 |
| Edge [!DNL Profile]查询增强 | 应用程序现在可以通过给定查询的任意标识来用户档案Edge [!DNL Profile]。 |
| 根据投影配置合并策略 | 应用程序现在可以针对每个投影配置合并策略，以生成由特定合并策略管理的视图数据。 |
| 计算属性 | 计算属性会根据其他值、计算和表达式自动计算字段值。 计算属性在用户档案级别上根据传入事件、传入事件和用户档案数据或传入事件、用户档案数据和历史事件对聚合值（如“总购买”、“生存期值”或“漏斗状态”）进行操作。 |

**错误修复**

* 简化了合并策略创建工作流中可用ID拼接策略的列表。

**已知问题**

* 没有。

有关[!DNL Real-time Customer Profile]的详细信息，包括使用[!DNL Profile]数据的教程和最佳实践，请阅读[实时客户用户档案概述](../../profile/home.md)。

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service]提供了用户界面和RESTful API，使您能够根据[!DNL Real-time Customer Profile]数据构建区段和生成受众。 这些区段在[!DNL Platform]上集中配置和维护，使任何Adobe应用程序都可轻松访问它们。

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准，定义特定的用户档案子集。细分可以基于记录数据（如人口统计信息）或表示客户与您品牌互动的时间序列事件。

| 功能 | 描述 |
| -----------| ---------- |
| 计划分段 | 用户现在可以通过UI和API为所有区段启用计划的区段评估。 启用后，所有区段将每天评估一次。 这不会影响按需细分功能，这些功能仍可以像以前一样继续工作。<br/><br/>注意：计划的分段功能不能用于包含五个以上合并策略的沙箱 [!DNL XDM Individual Profile]。 |
| 流细分 | 支持持续评估区段（流分段），当数据传入[!DNL Platform]时，可评估大多数区段规则。 此功能意味着区段成员资格将保持最新，无需运行计划的分段作业。 某些例外适用，如使用多实体关系的细分或具有丰富的负载。 |
| 段作为构件块 | 使用区段生成器用户界面创建区段时，用户现在可以将先前定义的区段用作其他区段的构建块。 <ul><li>参考当前受众会员资格：随着人们进出受众而更新。</li><li>复制逻辑：将选定的区段定义重复到新区段。</li></ul> |
| 视图区段成员资格(按ID命名空间) | 现在可通过ID命名空间（电子邮件、ECID和总计数）查看区段会员资格。 |
| RBAC支持 | 区段生成器现在支持基于角色的基本访问控制和权限。 |
| 增强了[!DNL Platform]和受众解决方案之间外部Adobe共享的支持 | 在受众数量较大或先验不知的情况下，用户现在可以导入外部（非[!DNL Experience Platform]）受众元数据。 此版本包括对已配置解决方案连接器的客户的[!DNL Audience Manager]元数据的访问。 此受众元数据可在区段生成器中使用，以创建新的[!DNL Experience Platform]区段。 <br/><br/> 此外，在中创建的 [!DNL Experience Platform] 细分现在可用于集成Adobe解决方案， [!DNL Audience Manager]包括 [!DNL Target]、和 [!DNL Ad Cloud]。 |

**错误修复**

* 修复了导致多实体分段在嵌套关系情况下返回零用户档案的问题。
* 修复了排除逻辑返回误导结果的问题。
* 改进了多实体文件夹的可读性。 现在，它们显示XDM类的易记名称。
* 修复了出现同一XDM文件夹的多个副本的间歇性问题。
* 现在生成消息以通知用户，如果所选合并策略不可用区段估计。

**已知问题**

* 没有。

要了解有关[!DNL Segmentation Service]的更多信息，请阅读[分段服务概述](../../segmentation/home.md)。
