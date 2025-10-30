---
title: Adobe Experience Platform 发行说明（2019 年 11 月）
description: Adobe Experience Platform 2019 年 11 月发行说明。
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1889'
ht-degree: 8%

---

# Adobe Experience Platform 发行说明

**发行日期： 2019年11月18日**

Adobe Experience Platform 的新功能：

* [[!DNL Real-Time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

现有功能更新：

* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-Time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Real-Time Customer Data Platform (Real-Time CDP)构建于Adobe Experience Platform之上，可帮助企业汇总已知和未知数据，通过客户历程中的智能决策激活客户配置文件。 Real-Time CDP将多个企业数据源整合在一起，实时创建统一的用户档案，用于跨所有渠道和设备提供一对一的个性化客户体验。

[!DNL Real-Time Customer Data Platform]包括用于数据管理、身份管理、高级分段和数据科学的工具，以便您可以构建用户档案和定义受众，并获得丰富的见解，同时能够强制执行严格的数据管理策略。

Adobe可连接到由众多合作伙伴组成的大型生态系统，更不用说与Adobe Experience Cloud的本机集成了，因此您可以无缝激活这些受众，并通过所有渠道提供卓越的客户体验，从现场或应用程序内个性化到电子邮件、付费媒体、呼叫中心、互联设备等。

借助Real-Time CDP，您可以：

* 通过流式收集整个企业的客户数据，实现客户的单一视图。
* 使用已知和未知标识符的可信治理和隐私控制负责任地管理用户档案。
* 使用由Adobe Sensei提供支持并为营销人员构建的AI和机器学习生成可操作的见解并扩展受众。
* 在所有渠道和目标上实时提供个性化体验。

有关详细信息，请参阅[Real-Time Customer Data Platform文档](../../rtcdp/overview.md)。

**主要功能**

| 功能 | 描述 |
|---|---|
| 目标 | 预先构建的与Adobe的[!DNL Real-Time Customer Data Platform]所支持的目标平台的集成，这些平台可无缝地向这些合作伙伴激活数据。 有关详细信息，请参阅下面的[目标](#destinations)。 |
| 主页量度仪表板 | Real-Time Customer Data Platform (Real-Time CDP)主页包含一个量度仪表板，用于显示有关配置文件和区段的信息。 主页还包含指向学习材料的链接。 请参阅下面有关[Real-Time Customer Data Platform指标](#real-time-customer-data-platform-metrics)的部分。 |
| 源 | 您可以从各种源摄取数据，如Adobe解决方案、基于云的存储、第三方软件和您的CRM。 请参阅下面的[源](#sources)部分以了解更多信息。 |

**[!DNL Real-Time Customer Data Platform]个量度**

Real-Time Customer Data Platform (Real-Time CDP)主页（包括一个量度功能板）会在您登录到Real-Time CDP时显示。

主页只是显示量度卡片的位置之一。 Real-Time CDP会在您的整个体验中提供量度卡片。 这些量度会告知您系统中的数据、个人资料和区段受众。

如果您在登录到Real-Time CDP时系统中没有数据，则不会显示主页上的仪表板。 在这种情况下，主页会为首次用户体验提供学习材料。 在收集数据时，功能板会自动更新以显示有关该数据的信息。

要了解更多信息，请参阅[Real-Time Customer Data Platform指标概述](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations]是预先构建的与目标平台的集成，目标平台受Adobe的Real-Time Customer Data Platform支持，可无缝地向这些合作伙伴激活数据。 有关详细信息，请阅读[目标概述](../../destinations/home.md)一文。

**可用目标**

在11月版中，Adobe的Real-Time Customer Data Platform支持以下目标：

* Advertising： [!DNL Google]
* 电子邮件营销： Adobe Campaign，[!DNL Salesforce Marketing Cloud]，[!DNL Responsys]，[!DNL Oracle Eloqua]

有关每个目标的信息，请参阅[目标目录](../../destinations/catalog/overview.md)。

**已知限制**

* 在初始版本中，激活流程（“计划”步骤）中允许自定义激活计划的控件不可用。
* 当前无法编辑或删除目标配置。 要解决此限制，您可以在[目标详细信息页面](../../destinations/ui/destination-details-page.md)的右上角启用或禁用该目标。
* 连接到目标或存储帐户时，当前没有验证帐户详细信息、路径或凭据。 确保输入正确的凭据并仔细检查拼写错误或拼写错误。
* 初始版本未实施凭据续订。 帐户过期或需要刷新后，必须创建新的目标连接并重新映射以前映射的区段。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强该数据。 您可以从各种源摄取数据，如Adobe解决方案、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform]提供了一个RESTful API和一个交互式UI，可让您轻松为各种数据提供程序设置源连接。 通过这些源连接，可对存储系统和CRM服务进行身份验证，设置摄取运行的时间，并管理数据摄取吞吐量。

**主要功能**

| 功能 | 描述 |
| ---------- | ------------ |
| 源UI | 用于创建、查看和管理源连接的新用户界面。 |
| CRM连接器工作流程已改版 | 用于创建和管理[!DNL Microsoft Dynamics]和[!DNL Salesforce]连接器的新的直观UI工作流。 |
| 基于云的存储的连接器支持 | 连接器现在可以访问基于云的存储。 新源包括[!DNL Amazon S3]、[!DNL Azure Blob]和FTP/SFTP服务器。 |

**已知问题**

* 用于基于云的存储的Source连接器不支持压缩文件的摄取。

有关源的更多信息，请参阅[源概述](../../sources/home.md)。

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace]通过构建和运行机器学习模型，使数据科学家能够从Adobe应用程序和第三方系统中的数据和内容无缝地生成见解。 [!DNL Data Science Workspace]与[!DNL Experience Platform]紧密集成，支持端到端数据科学生命周期，包括探索和准备XDM数据，然后开发和操作模型，以使用机器学习分析自动丰富[!DNL Real-Time Customer Profile]。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 使用[!DNL Experience Platform] SDK访问数据 | [!DNL Python]中预建的配方和启动器笔记本现在使用[!DNL Experience Platform] SDK访问数据。 |
| 沙盒支持 | 支持即将推出的沙盒功能（目前为测试版），包括能够将笔记本和配方隔离到开发或生产沙盒中。 有关更多信息，请参阅[沙盒概述](../../sandboxes/home.md)。 |

有关详细信息，请参阅[数据科学Workspace概述](../../data-science-workspace/home.md)。

## [!DNL Experience Data Model] (XDM)系统 {#xdm}

标准化和互操作性是[!DNL Experience Platform]背后的关键概念。 由Adobe驱动的[!DNL Experience Data Model] (XDM)致力于标准化客户体验数据并定义用于客户体验管理的架构。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为任何应用程序提供通用结构和定义，以便与Adobe Experience Platform上的服务进行通信。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能**

| 功能 | 描述 |
| ---------- | ------------ |
| 通知模式 | 新架构，表示在数据摄取过程中发送的通知数据。 |
| Adobe AdCloud DSP架构 | 添加了五个新架构，分别表示位置、促销活动、包、广告商、帐户，这些架构代表Adobe Advertising Cloud需求方平台(DSP)元数据。 |
| ExperienceEvent实施详细信息架构字段组 | 新的ExperienceEvent字段组，用于添加标准字段以存储有关用于收集事件的软件的信息。 |
| [!DNL Profile Privacy]字段组 | 新的配置文件字段组添加了字段以接受[!DNL Real-Time Customer Profile]的常规退出和销售/共享选择退出信号。 |
| `xdm:alternateDisplayInfo`的格式约束 | `xdm:alternateDisplayInfo`的“标题”和“描述”字段都必须为字符串才能通过验证。 |
| 名称更改： XDM [!DNL Individual Profile] | “XDM [!DNL Profile]”类的“标题”已更新为“XDM [!DNL Individual Profile]”。 类的正式`$id`未更改。 |

**已知问题**

* 无。

要了解有关使用[!DNL Schema Registry] API和[!DNL Schema Editor]用户界面使用XDM的更多信息，请阅读[XDM系统文档](../../xdm/home.md)。

## [!DNL Real-Time Customer Profile] {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。通过[!DNL Real-Time Customer Profile]，您可以查看合并来自多个渠道（包括在线、离线、CRM和第三方数据）的数据的每个单个客户的整体视图。 [!DNL Profile]允许您将不同的客户数据整合到一个统一视图中，并提供每个客户交互的带时间戳的可操作帐户。

| 功能 | 描述 |
| -----------| ---------- |
| 对[!DNL Profile]查找的增强 | 用户现在可以使用引用描述符和相关实体查找用户档案。 |
| 清理给定数据集的数据 | 用户现在可以使用[!DNL Profile]系统作业API删除给定数据集或批次的数据。 |
| Edge [!DNL Profile]查询增强功能 | 应用程序现在可以按给定配置文件的任意标识查询Edge [!DNL Profile]。 |
| 为每个投影配置合并策略 | 应用程序现在可以按投影配置合并策略，以生成受特定合并策略控制的数据视图。 |
| 计算属性 | 计算属性会根据其他值、计算和表达式自动计算字段的值。 计算属性在配置文件级别运行，以根据传入事件、传入事件和配置文件数据或传入事件、配置文件数据和历史事件来聚合值，如“总购买”、“生命周期值”或“funnel状态”。 |

**错误修复**

* 合并策略创建工作流中可用ID拼接策略的简化列表。

**已知问题**

* 无。

有关[!DNL Real-Time Customer Profile]的更多信息，包括有关使用[!DNL Profile]数据的教程和最佳实践，请阅读[实时客户资料概述](../../profile/home.md)。

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service]提供了一个用户界面和RESTful API，允许您根据[!DNL Real-Time Customer Profile]数据构建区段并生成受众。 这些区段是在[!DNL Experience Platform]上集中配置和维护的，因此任何Adobe应用程序都可以轻松访问它们。

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

| 功能 | 描述 |
| -----------| ---------- |
| 计划分段 | 用户现在可以通过UI和API为所有区段启用计划的区段评估。 启用后，所有区段每天都将评估一次。 这不会影响按需分段功能，这些功能将像以前一样继续工作。<br/><br/>注意：计划分段功能不能在具有超过5个[!DNL XDM Individual Profile]合并策略的沙盒中使用。 |
| 流式客户细分 | 支持连续评估区段（流式分段），允许在数据传入[!DNL Experience Platform]时评估大多数区段规则。 此功能意味着区段成员资格将是最新的，无需运行计划的分段作业。 某些例外情况适用，例如使用多实体关系或具有扩充有效负荷的区段。 |
| 将区段作为构建块 | 使用区段生成器UI创建区段时，用户现在可以将之前定义的区段用作其他区段的构建块。 <ul><li>引用当前受众成员资格：随着人员进出受众进行更新。</li><li>复制逻辑：获取选定的区段定义并将其复制到新区段中。</li></ul> |
| 按ID命名空间查看区段成员资格 | 现在可以按ID命名空间（电子邮件、ECID和总数）查看区段成员资格。 |
| RBAC支持 | 现在，区段生成器支持基于角色的基本访问控制和权限。 |
| 增强了[!DNL Experience Platform]与Adobe解决方案之间的外部受众共享支持 | 在受众数量较大或先验未知的情况下，用户现在可以引入外部（非[!DNL Experience Platform]）受众元数据。 此版本包括访问已设置解决方案连接器的客户的[!DNL Audience Manager]元数据。 此受众元数据可在区段生成器中用于创建新的[!DNL Experience Platform]区段。 <br/><br/>此外，在[!DNL Experience Platform]中创建的区段现在可用于集成的Adobe解决方案，包括[!DNL Audience Manager]、[!DNL Target]和[!DNL Ad Cloud]。 |

**错误修复**

* 修复了在嵌套关系的情况下导致多实体分段返回零配置文件的问题。
* 修复了排除逻辑返回误导性结果的问题。
* 提高了多实体文件夹的可读性。 它们现在显示XDM类的友好名称。
* 修复了出现同一XDM文件夹的多个副本的间歇性问题。
* 现在生成消息以通知用户区段估计是否不可用于所选的合并策略。

**已知问题**

* 无。

若要了解有关[!DNL Segmentation Service]的更多信息，请阅读[分段服务概述](../../segmentation/home.md)。
