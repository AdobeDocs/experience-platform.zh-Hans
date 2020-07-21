---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2019年12月11日
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 5%

---


# Adobe Experience Platform 发行说明

**发布日期： 2019年12月11日**

对Adobe Experience Platform中现有功能的更新：

* [!DNL Segmentation Service](#segmentation)
* [!DNL Decisioning Service](#decisioning)
* [!DNL Sources](#sources)
* [!DNL Experience Data Model (XDM) System](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform分段服务提供用户界面和RESTful API，允许您根据数据构建细分和生成 [!DNL Real-time Customer Profile] 受众。 这些细分集中进行配置和维护， [!DNL Platform]使任何Adobe应用程序都能轻松访问它们。

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准，定义特定的用户档案子集。 细分可以基于记录数据（如人口统计信息）或表示客户与您品牌互动的时间序列事件。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| “合并受众”选项卡 [!DNL Segment Builder] | Segments [!UICONTROL _和&#x200B;_][!UICONTROL _受众_] （区段） [!DNL Segment Builder] 选项卡已合并为单 [!UICONTROL _个受众&#x200B;_]选项卡。 此选项卡允许您浏览和搜索现有受众，然后将其拖放到规则构建器画布中以创建新的区段定义。 引用受众可以向新区段定义添加以下规则集之一： 受众成员资格作为规则，定义引用受众的完整规则逻辑集。 |
| 合并策略选择器的新位置 | 合并策略选择器在中的位 [!DNL Segment Builder] 置已更改。 要为段定义选择合并策略，请单击“字段”选项卡上的齿轮 [!UICONTROL _图标&#x200B;_]，然后使用“合并策略__ ”下拉菜单选择要使用的合并策略。 |

**已知问题**

* None

有关详细信息，请参阅 [分段服务概述](../../segmentation/home.md)。

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] 能够以编程方式智能地为特定个人从一组可用选项中选择“下一个最佳体验”，将其交付给任何渠道或应用程序，并执行报告和分析。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 排名函数 | 用户档案的优惠顺序现在通过排序函数而不是所有用户档案的固定优惠集来导出。 |

**已知问题**

* 无。

有关服 [务的完整介绍](../../decisioning-service/home.md) ，请参阅决策服务概述。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源收集数据，同时允许您使用服务构建、标记和增强该 [!DNL Platform] 数据。 您可以从各种来源(如Adobe解决方案、基于云的存储、第三方软件和您的CRM系统)收集数据。

[!DNL Experience Platform] 提供REST风格的API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您验证存储系统和CRM服务，设置摄取运行的时间，并管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ---------- | ------------ |
| 流连接 | 流摄取使您能够将数据从客户端和服务器端设备 [!DNL Experience Platform] 实时发送到。 版本包括新的流连接用户界面。 |
| 连接器支持 [!DNL Google Cloud Store] | 支持从收集数据 [!DNL Google Cloud Store]。 |

**已知问题**

* 无。

有关源的详细信息，请参阅 [源概述](../../sources/home.md)。

## [!DNL Experience Data Model] (XDM)系统 {#xdm}

标准化和互操作性是背后的关键概念 [!DNL Experience Platform]。 [!DNL Experience Data Model] (XDM)由Adobe推动，旨在实现客户体验数据标准化并为客户体验管理定义模式。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为在Adobe Experience Platform上与服务通信的任何应用程序提供了通用结构和定义。 通过遵守XDM标准，所有客户体验数据都可以整合到一个通用表现形式中，以更快、更集成的方式提供洞察。 您可以从客户行动中获得宝贵的洞察，通过细分定义客户受众，并将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 改进的模式验证 | 新的检查可确保引用解析为其他字段（如预期）。 为定义为对象数组的字段添加了其他检查，以确保对象已完全定义。 改进了错误消息，以帮助识别和修复问题。 |

**错误修复**

* 与访问控制和沙箱相关的维护和改进。
* 支持 `eTag` API `/descriptors` 中的端点 [!DNL Schema Registry] 。

**已知问题**

* None

要进一步了解如何使用API和 [!DNL Schema Registry] 用户 [!DNL Schema Editor] 界面使用XDM，请阅 [读XDM系统文档](../../xdm/home.md)。