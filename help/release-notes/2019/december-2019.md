---
title: Adobe Experience Platform发行说明2019年12月
description: Adobe Experience Platform 2019年12月版发行说明。
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发行日期： 2019年12月11日**

Adobe Experience Platform 现有功能的更新包括：

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service提供了一个用户界面和RESTful API，允许您从构建区段和生成受众。 [!DNL Real-Time Customer Profile] 数据。 这些区段集中配置并维护于 [!DNL Platform]，便于任何Adobe应用程序访问。

[!DNL Segmentation Service] 通过描述用于区分客户群内可销售人员组的标准，来定义用户档案的特定子集。 区段可以基于记录数据（例如人口统计信息）或表示客户与您的品牌互动的时间系列事件。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 中的“合并的受众”选项卡 [!DNL Segment Builder] | 此 [!UICONTROL 区段] 和 [!UICONTROL 受众] 选项卡位于 [!DNL Segment Builder] 已合并为一个 [!UICONTROL 受众] 选项卡。 利用此选项卡，可浏览和搜索现有受众，然后将其拖放到规则生成器画布中以创建新的区段定义。 引用受众可以向新区段定义添加以下规则逻辑集之一：受众成员资格作为规则，定义引用受众的完整规则逻辑集。 |
| 合并策略选择器的新位置 | 合并策略选择器在 [!DNL Segment Builder] 已更改。 要为区段定义选择合并策略，请选择 **[!UICONTROL 字段]** 选项卡，然后使用 **[!UICONTROL 合并策略]** 下拉菜单选择要使用的合并策略。 |

**已知问题**

* None

欲知更多信息，请参见 [分段服务概述](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] 提供以下能力：以编程方式智能地从给定个人的一组可用选项中选择“下一个最佳体验”，将其交付到任何渠道或应用程序，以及执行报告和分析。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 排名函数 | 现在，用户档案的优惠顺序是通过排名函数派生的，而不是通过所有用户档案中的固定优惠集派生的。 |

**已知问题**

* None.

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用来构建、标记和增强这些数据 [!DNL Platform] 服务。 您可以从各种来源(如Adobe解决方案、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

[!DNL Experience Platform] 提供了一个RESTful API和一个交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您对存储系统和CRM服务进行身份验证，设置引入运行的时间，并管理数据引入吞吐量。

**新增功能**

| 功能 | 描述 |
| ---------- | ------------ |
| 流连接 | 流式摄取允许您将数据从客户端和服务器端设备发送到 [!DNL Experience Platform] 实时。 此版本包括新的流连接用户界面。 |
| 连接器支持 [!DNL Google Cloud Store] | 支持从中收集数据 [!DNL Google Cloud Store]. |

**已知问题**

* None.

有关源的更多信息，请参见 [源概述](../../sources/home.md).

## [!DNL Experience Data Model] (XDM)系统 {#xdm}

标准化和互操作性是背后的关键概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)由Adobe驱动，致力于标准化客户体验数据并定义用于客户体验管理的架构。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为任何应用程序提供通用结构和定义，以便与Adobe Experience Platform上的服务进行通信。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 改进了架构验证 | 新检查可确保引用按预期解析为其他字段。 向定义为对象数组的字段添加了其他检查，以确保完全定义了对象。 改进了错误消息，以帮助识别和修复问题。 |

**错误修复**

* 与访问控制和沙盒相关的维护和改进。
* 支持 `eTag` 对于 `/descriptors` 中的端点 [!DNL Schema Registry] API。

**已知问题**

* None

要了解有关使用XDM的更多信息，请使用 [!DNL Schema Registry] API和 [!DNL Schema Editor] 用户界面，请阅读 [XDM系统文档](../../xdm/home.md).
