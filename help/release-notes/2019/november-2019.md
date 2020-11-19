---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2019年11月18日
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '1878'
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

实时客户数据平台(Real-time CDP)以Adobe Experience Platform为构建基础，可帮助公司将已知和未知的数据整合在一起，在客户旅程中通过智能决策激活客户用户档案。 实时CDP结合了多个企业用户档案源，以实时创建统一的渠道，这些数据可用于在所有和设备上提供一对一的个性化客户体验。

[!DNL Real-time Customer Data Platform] 包括用于数据治理、身份管理、高级细分和数据科学的工具，使您能够构建用户档案并定义受众，并在能够实施严格数据治理策略的同时获得丰富的洞察。

Adobe连接到一个大型的合作伙伴生态系统，更不用说与Adobe Experience Cloud的本机集成，因此您可以无缝激活这些受众并在所有渠道提供出色的客户体验，从现场或应用程序内个性化到电子邮件、付费媒体、呼叫中心、互联设备等。

利用实时CDP，您可以：

* 通过从整个企业内流式收集客户数据，实现客户的单一视图。
* 对已知和未知标识符进行可信管理和隐私控制，以负责任的方式管理用户档案。
* 借助以Adobe Sensei为后盾、专为营销人员打造的人工智能和机器学习，生成切实可行的洞察并扩展受众。
* 在所有渠道和目的地实时提供个性化体验。

有关详细信息，请 [参阅实时客户数据平台文档](../../rtcdp/overview.md)。

**主要功能**

| 功能 | 描述 |
|---|---|
| 目标 | 预建与受Adobe支持的目标平台集成， [!DNL Real-time Customer Data Platform] 以无缝方式向这些合作伙伴激活数据。 See [Destinations](#destinations) below for more information. |
| 主页指标仪表板 | 实时客户数据平台（实时CDP）主页包含一个指标仪表板，它显示有关用户档案和细分的信息。 该主页还包含指向学习材料的链接。 请参阅以下 [实时客户数据平台指标部分](#real-time-customer-data-platform-metrics) 。 |
| 源 | 您可以从各种来源(如Adobe解决方案、基于云的存储、第三方软件和您的CRM)收集数据。 请参阅 [以下](#sources) “源”部分以了解更多。 |

**[!DNL Real-time Customer Data Platform]指标**

实时客户数据平台(Real-time CDP)主页，在您登录到实时CDP时，会显示该仪表板，其中包括一个指标。

主页只是显示度量卡的位置之一。 实时CDP在您的整个体验中提供度量卡。 这些指标会通知您系统中的数据、用户档案和细分受众。

如果登录到实时CDP时系统中没有仪表板，则不会显示主页上的数据。 在这种情况下，主页首次为用户提供学习材料。 在收集数据时，仪表板会自动更新以显示有关该数据的信息。

要了解更多信息，请参 [阅实时客户数据平台指标概述](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是预建的与Adobe实时客户数据平台支持的目标平台集成，以无缝方式向这些合作伙伴激活数据。 有关详细信息，请阅读目 [标概述](../../rtcdp/destinations/destinations-overview.md) 文章。

**可用目标**

在11月的发布中，Adobe的实时客户数据平台支持以下目标：

* 广告: [!DNL Google]
* 电子邮件营销：Adobe Campaign [!DNL Salesforce Marketing Cloud], [!DNL Responsys][!DNL Oracle Eloqua]

有关每 [个目标](../../rtcdp/destinations/destinations-catalog.md) ，请参阅目标目录。

**已知限制**

* 在初始版本中，不提供允许在激活流 [(激活步](../../rtcdp/destinations/activate-destinations.md#activate-data) )中进行自定义计划计划的控件。
* 当前无法编辑或删除目标配置。 要绕过此限制，您可以启用或禁用目标详细信息页面右上角 [的目标](../../rtcdp/destinations/destination-details-page.md)。
* 连接到目标或存储帐户时，当前没有验证帐户详细信息、路径或凭据。 确保输入正确的凭据，并对拼写错误或打字错误进行多次检查。
* 在初始版本中没有进行凭据续订。 在帐户过期或需要刷新后，您必须创建新的目标连接并重新映射之前映射的区段。

## 源 {#sources}

Adobe Experience Platform可以从外部来源收集数据，同时允许您使用服务来构建、标记和增强该 [!DNL Platform] 数据。 您可以从各种来源(如Adobe解决方案、基于云的存储、第三方软件和您的CRM系统)收集数据。

[!DNL Experience Platform] 提供REST风格的API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您验证存储系统和CRM服务，设置摄取运行的时间，并管理数据摄取吞吐量。

**主要功能**

| 功能 | 描述 |
| ---------- | ------------ |
| 源UI | 用于创建、查看和管理源连接的新用户界面。 |
| 改进了CRM连接器的工作流 | 用于创建和管理连接器的全新直观 [!DNL Microsoft Dynamics] UI工 [!DNL Salesforce] 作流程。 |
| 对基于云的存储的连接器支持 | 连接器现在可以访问基于云的存储。 新来源 [!DNL Amazon S3]包括 [!DNL Azure Blob]FTP/SFTP服务器。 |

**已知问题**

* 基于云的存储的源连接器不支持获取压缩文件。

有关源的详细信息，请参阅 [源概述](../../sources/home.md)。

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] 通过构建和运行机器学习模型，使数据科学家能够跨Adobe应用程序和第三方系统无缝地从数据和内容生成洞察。 [!DNL Data Science Workspace] 与端对端数 [!DNL Platform] 据科学生命周期紧密集成，并为其提供强大动力，包括探索和准备XDM数据，然后开发和运行模型以自动丰富机器学习 [!DNL Real-time Customer Profile] 的洞察。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 使用SDK访问 [!DNL Platform] 数据 | 现在，中预建的菜谱和启动器笔 [!DNL Python] 记本电 [!DNL Platform] 脑使用SDK访问数据。 |
| 沙箱支持 | 支持即将推出的沙箱功能（目前为测试版），包括将笔记本和菜谱隔离到开发或生产沙箱的能力。 See the [sandboxes overview](../../sandboxes/home.md) for more information. |

有关详细信息，请参 [阅数据科学工作区概述](../../data-science-workspace/home.md)。

## [!DNL Experience Data Model] (XDM)系统 {#xdm}

标准化和互操作性是背后的关键概念 [!DNL Experience Platform]。 [!DNL Experience Data Model] (XDM)由Adobe驱动，旨在实现客户体验数据标准化并定义客户体验管理模式。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为任何与Adobe Experience Platform上的服务通信的应用程序提供了通用结构和定义。 通过遵守XDM标准，所有客户体验数据都可以整合到一个通用表现形式中，以更快、更集成的方式提供洞察。 您可以从客户行动中获得宝贵的洞察，通过细分定义客户受众，并将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
| ---------- | ------------ |
| 通知模式 | 表示数据获取过程中发送的通知数据的新模式。 |
| AdobeAdCloudDSP模式 | 新增了5个模式来代表Adobe Advertising Cloud需求侧平台(DSP)元数据：位置、活动、包装、广告商、帐户。 |
| ExperienceEvent实施详细信息混合 | 新增的ExperienceEvent混音，它添加一个标准字段以存储有关用于收集事件的软件的信息。 |
| [!DNL Profile Privacy] 混音 | 新的用户档案混音，可添加字段以接受一般退出和销售／共享选择退出信号 [!DNL Real-time Customer Profile]。 |
| 格式约束 `xdm:alternateDisplayInfo` | “标题”和“说明”字段必 `xdm:alternateDisplayInfo` 须都是字符串才能通过验证。 |
| 名称更改：XDM [!DNL Individual Profile] | “XDM”类的“ [!DNL Profile]标题”已更新为“XDM [!DNL Individual Profile]”。 班级 `$id` 的正式版本没有更改。 |

**已知问题**

* None.

要进一步了解如何使用API和 [!DNL Schema Registry] 用户 [!DNL Schema Editor] 界面使用XDM，请阅 [读XDM系统文档](../../xdm/home.md)。

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform使您能够为客户提供协调、一致和相关的体验，无论客户在何处或何时与您的品牌互动。 您 [!DNL Real-time Customer Profile]可以看到每个客户的整体视图，该渠道组合了多个的数据，包括在线、离线、CRM和第三方数据。 [!DNL Profile] 允许您将不同的客户数据整合到统一的视图中，为每次客户互动提供可操作、有时间戳的帐户。

| 功能 | 描述 |
| -----------| ---------- |
| 对查找的增 [!DNL Profile] 强 | 用户现在能够使用引用描述符和相关实体查找用户档案。 |
| 清除给定数据集的数据 | 用户现在可以使用系统作业API删除给定数据集或批 [!DNL Profile] 处理的数据。 |
| 边缘 [!DNL Profile] 查询增强 | 应用程序现在可 [!DNL Profile] 以按给定用户档案的任何标识查询Edge。 |
| 根据投影配置合并策略 | 应用程序现在可以根据投影配置合并策略，以生成由特定合并策略管理的视图。 |
| 计算属性 | 计算的属性会根据其他值、计算和表达式自动计算字段的值。 计算属性在用户档案级别上对聚合值（如“总购买”、“生命周期值”或“漏斗状态”）进行操作，这些值基于传入事件、传入事件和用户档案数据，或传入事件、用户档案数据和历史事件。 |

**错误修复**

* 简化了合并策略创建工作流中可用ID拼接策略的列表。

**已知问题**

* None.

有关更多信息( [!DNL Real-time Customer Profile]包括有关使用数据的教程和 [!DNL Profile] 最佳实践)，请阅 [读实时客户用户档案概述](../../profile/home.md)。

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] 提供用户界面和RESTful API，使您能够根据数据构建细分和生成 [!DNL Real-time Customer Profile] 受众。 这些细分集中配置并维护， [!DNL Platform]使任何Adobe应用程序都能轻松访问它们。

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准，定义特定的用户档案子集。 细分可以基于记录数据（如人口统计信息）或表示客户与您品牌互动的时间序列事件。

| 功能 | 描述 |
| -----------| ---------- |
| 计划分段 | 用户现在可以通过UI和API为所有区段启用计划的区段评估。 启用后，所有区段将每天评估一次。 这不会影响按需细分功能，这些功能仍可以像以前一样继续工作。<br/><br/>注意：计划分段功能不能用于具有五个以上合并策略的沙箱 [!DNL XDM Individual Profile]。 |
| 流细分 | 支持持续评估区段（流分段），当数据传入时，可以评估大多数区段规则 [!DNL Platform]。 此功能意味着区段成员资格将保持最新，无需运行计划的分段作业。 某些例外适用，如使用多实体关系的细分或具有丰富有效载荷的细分。 |
| 细分为构件块 | 使用区段生成器UI创建区段时，用户现在可以使用先前定义的区段作为其他区段的构建块。 <ul><li>参考当前受众会员资格：当人们进出受众时更新。</li><li>复制逻辑：将选定的区段定义并重复到新区段中。</li></ul> |
| 按ID视图的命名空间段成员资格 | 区段成员资格现在可以通过ID命名空间（电子邮件、ECID和总计数）进行查看。 |
| RBAC支持 | 区段生成器现在支持基于角色的基本访问控制和权限。 |
| 增强了对外部受众共享的支持，在解决方 [!DNL Platform] 案和Adobe解决方案之间 | 在受众数量较大或事先不知道的情[!DNL Experience Platform]况下，用户现在可以引入外部（非）受众元数据。 此版本包括对已配置 [!DNL Audience Manager] 解决方案连接器的客户的元数据的访问。 此受众元数据可在区段生成器中用于创建新 [!DNL Experience Platform] 区段。 <br/><br/> 此外，中创建的 [!DNL Experience Platform] 细分现在可用于集成Adobe解决方案， [!DNL Audience Manager]包括 [!DNL Target]、和 [!DNL Ad Cloud]。 |

**错误修复**

* 修复了在嵌套关系情况下导致多实体细分返回零用户档案的问题。
* 修复了排除逻辑返回误导结果的问题。
* 改进了多实体文件夹的可读性。 现在，它们显示XDM类的友好名称。
* 修复了显示同一XDM文件夹的多个副本的间歇性问题。
* 现在，产生消息以通知用户，如果所选合并策略不提供区段估计。

**已知问题**

* None.

要了解有关的更 [!DNL Segmentation Service]多信息，请阅读 [分段服务概述](../../segmentation/home.md)。