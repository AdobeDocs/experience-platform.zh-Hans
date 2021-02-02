---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2019年12月11日
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 7%

---


# Adobe Experience Platform 发行说明

**发布日期：2019年12月11日**

Adobe Experience Platform 现有功能的更新包括：

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform分段服务提供用户界面和RESTful API，允许您根据[!DNL Real-time Customer Profile]数据构建细分和生成受众。 这些区段集中配置并维护在[!DNL Platform]上，使任何Adobe应用程序都能轻松访问它们。

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准，定义特定的用户档案子集。细分可以基于记录数据（如人口统计信息）或表示客户与您品牌互动的时间序列事件。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| [!DNL Segment Builder]中的“合并受众”选项卡 | [!DNL Segment Builder]中的[!UICONTROL 区段]和[!UICONTROL 受众]选项卡已合并为单个[!UICONTROL 受众]选项卡。 此选项卡允许您浏览和搜索现有受众，然后将其拖放到规则构建器画布中以创建新的区段定义。 引用受众可以向新区段定义添加以下规则集之一：受众成员资格作为规则，定义引用受众的完整规则逻辑集。 |
| 合并策略选择器的新位置 | [!DNL Segment Builder]中合并策略选择器的位置已更改。 要为段定义选择合并策略，请在&#x200B;**[!UICONTROL 字段]**&#x200B;选项卡上选择齿轮图标，然后使用&#x200B;**[!UICONTROL 合并策略]**&#x200B;下拉菜单选择要使用的合并策略。 |

**已知问题**

* None

有关详细信息，请参阅[分段服务概述](../../segmentation/home.md)。

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform[!DNL Decisioning Service]提供以编程方式智能地从给定个人的一组可用选项中选择“下一个最佳体验”、将其交付给任何渠道或应用程序、执行报告和分析的能力。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 排名函数 | 用户档案的优惠顺序现在通过排序函数而不是所有用户档案的固定优惠集来导出。 |

**已知问题**

* None.

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源收集数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强该数据。 您可以从各种来源(如Adobe解决方案、基于云的存储、第三方软件和您的CRM系统)收集数据。

[!DNL Experience Platform] 提供REST风格的API和交互式UI，让您可以轻松为各种数据提供者设置源连接。这些源连接允许您验证存储系统和CRM服务，设置摄取运行的时间，并管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ---------- | ------------ |
| 流连接 | 流摄取使您能够实时将数据从客户端和服务器端设备发送到[!DNL Experience Platform]。 版本包括新的流连接用户界面。 |
| [!DNL Google Cloud Store]的连接器支持 | 支持从[!DNL Google Cloud Store]收集数据。 |

**已知问题**

* 没有。

有关源的详细信息，请参阅[源概述](../../sources/home.md)。

## [!DNL Experience Data Model] (XDM)系统  {#xdm}

标准化和互操作性是[!DNL Experience Platform]的主要概念。 [!DNL Experience Data Model] (XDM)由Adobe驱动，旨在实现客户体验数据标准化并定义客户体验管理模式。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为任何与Adobe Experience Platform上的服务通信的应用程序提供了通用结构和定义。 通过遵守XDM标准，所有客户体验数据都可以整合到一个通用表现形式中，以更快、更集成的方式提供洞察。 您可以从客户行动中获得宝贵的洞察，通过细分定义客户受众，并将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 改进的模式验证 | 新的检查可确保引用解析为其他字段（如预期）。 为定义为对象数组的字段添加了其他检查，以确保对象已完全定义。 改进了错误消息，以帮助识别和修复问题。 |

**错误修复**

* 与访问控制和沙箱相关的维护和改进。
* 支持[!DNL Schema Registry] API中的`/descriptors`端点`eTag`。

**已知问题**

* 无

要进一步了解如何使用[!DNL Schema Registry] API和[!DNL Schema Editor]用户界面使用XDM，请阅读[ XDM系统文档](../../xdm/home.md)。