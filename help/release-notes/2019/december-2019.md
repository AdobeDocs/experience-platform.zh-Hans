---
title: Adobe Experience Platform发行说明2019年12月
description: 2019年12月版Adobe Experience Platform发行说明。
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发行日期：2019年12月11日**

Adobe Experience Platform 现有功能的更新包括：

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service提供了用户界面和RESTful API，允许您从 [!DNL Real-time Customer Profile] 数据。 这些区段在上集中配置和维护 [!DNL Platform]，以便任何Adobe应用程序都可轻松访问。

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准来定义特定的用户档案子集。 区段可以基于记录数据（如人口统计信息）或表示客户与您的品牌交互的时间序列事件。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 中的“合并的受众”选项卡 [!DNL Segment Builder] | 的 [!UICONTROL 区段] 和 [!UICONTROL 受众] 选项卡 [!DNL Segment Builder] 合并为一个 [!UICONTROL 受众] 选项卡。 利用此选项卡，可浏览和搜索现有受众，然后将现有受众拖放到规则生成器画布中，以创建新的区段定义。 引用受众可以向新区段定义中添加以下一组规则逻辑之一：作为规则，受众成员资格是定义引用受众的完整规则逻辑集。 |
| 合并策略选择器的新位置 | 合并策略选择器在 [!DNL Segment Builder] 已更改。 要为区段定义选择合并策略，请在 **[!UICONTROL 字段]** 选项卡，然后使用 **[!UICONTROL 合并策略]** 下拉菜单，选择要使用的合并策略。 |

**已知问题**

* None

有关详细信息，请参阅 [Segmentation Service概述](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] 提供了以编程方式智能地从给定个人的一组可用选项中选择“下一个最佳体验”、将其交付到任何渠道或应用程序，以及执行报告和分析的功能。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 排名函数 | 用户档案的选件顺序现在通过排名函数派生，而不是通过所有用户档案的一组固定选件来派生。 |

**已知问题**

* None.

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用 [!DNL Platform] 服务。 您可以从各种来源摄取数据，如Adobe解决方案、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform] 提供了RESTful API和交互式UI，让您能够轻松为各种数据提供程序设置源连接。 这些源连接允许您对存储系统和CRM服务进行身份验证，设置摄取运行的时间，并管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ---------- | ------------ |
| 流连接 | 流式摄取让您能够将数据从客户端和服务器端设备发送到 [!DNL Experience Platform] 实时。 此版本包括新的流连接用户界面。 |
| 连接器支持 [!DNL Google Cloud Store] | 支持从中收集数据 [!DNL Google Cloud Store]. |

**已知问题**

* 无。

有关源的详细信息，请参阅 [源概述](../../sources/home.md).

## [!DNL Experience Data Model] (XDM)系统 {#xdm}

标准化和互操作性是其背后的关键概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)在Adobe的驱动下，努力标准化客户体验数据并定义客户体验管理架构。

XDM是一项公开记录的规范，旨在提高数字体验的强大功能。 它为任何与Adobe Experience Platform上的服务通信的应用程序提供了通用结构和定义。 通过遵循XDM标准，所有客户体验数据都可以整合到通用呈现形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 改进了架构验证 | 新增了检查，以确保引用可按预期解析到其他字段中。 为定义为对象数组的字段添加了额外的检查，以确保对象已完全定义。 改进了错误消息，以帮助识别和修复问题。 |

**错误修复**

* 与访问控制和沙箱相关的维护和改进。
* 支持 `eTag` 对于 `/descriptors` 的端点 [!DNL Schema Registry] API。

**已知问题**

* 无

要了解有关使用XDM的更多信息，请使用 [!DNL Schema Registry] API和 [!DNL Schema Editor] 用户界面，请阅读 [XDM系统文档](../../xdm/home.md).
