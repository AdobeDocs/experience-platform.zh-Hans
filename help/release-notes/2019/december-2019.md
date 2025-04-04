---
title: Adobe Experience Platform发行说明2019年12月
description: Adobe Experience Platform 2019年12月版发行说明。
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 15%

---

# Adobe Experience Platform 发行说明

**发行日期： 2019年12月11日**

Adobe Experience Platform 中现有功能的更新：

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service提供了一个用户界面和RESTful API，允许您根据[!DNL Real-Time Customer Profile]数据构建区段并生成受众。 这些区段是在[!DNL Experience Platform]上集中配置和维护的，因此任何Adobe应用程序都可以轻松访问它们。

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| [!DNL Segment Builder]中的“合并的受众”选项卡 | [!DNL Segment Builder]中的[!UICONTROL 区段]和[!UICONTROL 受众]选项卡已合并为单个[!UICONTROL 受众]选项卡。 利用此选项卡，可浏览和搜索现有受众，然后将其拖放到规则生成器画布中以创建新的区段定义。 引用受众可以向新区段定义添加以下规则逻辑集之一：将受众成员资格作为规则，添加用于定义引用受众的完整规则逻辑集。 |
| 合并策略选择器的新位置 | [!DNL Segment Builder]中合并策略选择器的位置已更改。 要为区段定义选择合并策略，请选择&#x200B;**[!UICONTROL 字段]**&#x200B;选项卡上的齿轮图标，然后使用&#x200B;**[!UICONTROL 合并策略]**&#x200B;下拉菜单选择要使用的合并策略。 |

**已知问题**

* None

有关详细信息，请参阅[分段服务概述](../../segmentation/home.md)。

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service]提供了以下能力：以编程方式智能地从给定个人的一组可用选项中选择“下一个最佳体验”，将它们交付到任何渠道或应用程序，以及执行报表和分析。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 排名函数 | 现在，用户档案的优惠顺序是通过排名函数派生的，而不是通过所有用户档案的固定优惠集派生的。 |

**已知问题**

* 无。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强该数据。 您可以从各种源摄取数据，如Adobe解决方案、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform]提供了一个RESTful API和一个交互式UI，可让您轻松为各种数据提供程序设置源连接。 通过这些源连接，可对存储系统和CRM服务进行身份验证，设置摄取运行的时间，并管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ---------- | ------------ |
| 流连接 | 流式摄取允许您实时将数据从客户端和服务器端设备发送到[!DNL Experience Platform]。 此版本包括新的流连接用户界面。 |
| [!DNL Google Cloud Store]的连接器支持 | 支持从[!DNL Google Cloud Store]收集数据。 |

**已知问题**

* 无。

有关源的更多信息，请参阅[源概述](../../sources/home.md)。

## [!DNL Experience Data Model] (XDM)系统 {#xdm}

标准化和互操作性是[!DNL Experience Platform]背后的关键概念。 由Adobe驱动的[!DNL Experience Data Model] (XDM)致力于标准化客户体验数据并定义用于客户体验管理的架构。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为任何应用程序提供通用结构和定义，以便与Adobe Experience Platform上的服务进行通信。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 改进了架构验证 | 新检查可确保引用按预期解析为其他字段。 向定义为对象数组的字段添加了其他检查，以确保对象已完全定义。 改进了错误消息，以帮助识别和修复问题。 |

**错误修复**

* 与访问控制和沙盒相关的维护和改进。
* 在[!DNL Schema Registry] API中支持`/descriptors`终结点的`eTag`。

**已知问题**

* None

要了解有关使用[!DNL Schema Registry] API和[!DNL Schema Editor]用户界面使用XDM的更多信息，请阅读[XDM系统文档](../../xdm/home.md)。
