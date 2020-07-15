---
title: Adobe Experience Platform 发行说明
description: Experience Platform的最新发行说明
doc-type: release notes
last-update: July 15, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 1e420d26f89150999f356f9cf5af94d434076c2b
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 7%

---


# Adobe Experience Platform 发行说明

**发行日期：2020 年 7 月 15 日**

对Adobe Experience Platform中现有功能的更新：

<!-- - [Data Governance](#governance) -->
- [实时客户资料](#profile)
- [分段服务](#segmentation)
- [源](#sources)

<!-- ## [!DNL Data Governance] {#governance}

Adobe Experience Platform Data Governance is a series of strategies and technologies used to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

**New features**

| Feature    | Description  |
| -----------| ---------- |
| Automatic policy enforcement in [!DNL Real-time Customer Data Platform] | Data usage policies are now automatically enforced in [!DNL Real-time CDP] when violating actions occur, including activating segments to destinations. When a policy violation is triggered, users get real-time visibility into usage restrictions within the activation workflow, indicating what data they cannot use and why.<br><br>See the section on [enforcing data usage compliance](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance) within the overview on [!DNL Data Governance] in [!DNL Real-time CDP] for more information. |
| Adobe Audience Manager integration | Any segments that are shared with [!DNL Audience Manager] from [!DNL Platform] inherit any applied data usage labels as [!DNL Data Export Controls], and vice versa. See the [!DNL Audience Manager] documentation for specific [mappings between usage labels and Data Export Controls](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep). |
| Custom data usage labels | You can now create custom data usage labels using the Policy Service API or in the UI. See the [labels overview](../../data-governance/labels/overview.md) for more information. |

See the [Data Governance overview](../../data-governance/home.md) for more information on the service.

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform enables you to drive coordinated, consistent, and relevant experiences for your customers no matter where or when they interact with your brand. With [!DNL Real-time Customer Profile], you can see a holistic view of each individual customer that combines data from multiple channels, including online, offline, CRM, and third party data. [!DNL Profile] allows you to consolidate your disparate customer data into a unified view offering an actionable, timestamped account of every customer interaction.

**New features**

| Feature | Description |
| ------- | ----------- |
| Data usage policy enforcement | In [!DNL Real-time Customer Data Platform], data usage policy violations are automatically surfaced when a violating action in the [!UICONTROL Profile] workspace is attempted. See the [release notes for Data Governance](#governance) for more information on automatic policy enforcement. | 

-->

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform分段服务提供用户界面和RESTful API，允许您根据数据构建细分和生成 [!DNL Real-time Customer Profile] 受众。 这些细分集中进行配置和维护， [!DNL Platform]使任何Adobe应用程序都能轻松访问它们。

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准，定义特定的用户档案子集。 细分可以基于记录数据（如人口统计信息）或表示客户与您品牌互动的时间序列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 流细分 | 现在，当数据进入时，流分段可以被限定为用户进入区段，从 [!DNL Platform]而显着缩短了区段限定时间。 流式分段还可以缓解手动运行分段作业的需求。 |

<!-- | Data usage policy enforcement | In [!DNL Real-time Customer Data Platform], data usage policy violations are automatically surfaced when a violating action in the [!UICONTROL Segments] workspace is attempted. See the [release notes for Data Governance](#governance) for more information on automatic policy enforcement. | -->

有关的详细信 [!DNL Segmentation Service]息，请参阅分 [段概述](../../segmentation/home.md)

## 源 {#sources}

Adobe Experience Platform可以从外部源收集数据，同时允许您使用服务构建、标记和增强该 [!DNL Platform] 数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)收集数据。

Experience Platform提供RESTful API和交互式UI，使您能轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 用于删除数据流的API和UI支持 | 现在，可通过API或使用UI删除出错或变得不必要的数据流。 |
| 对一次性摄取的API和UI支持 | 现在，可以通过API或使用UI执行数据流的一次性摄取，其中仅提供开始日期，不计划将来的摄取。 |

要进一步了解源，请参阅 [源概述](../../sources/home.md)。
