---
title: Adobe Experience Platform 发行说明
description: Experience Platform的最新发行说明
doc-type: release notes
last-update: July 15, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: e864073c27ba20ce32c962c469aed52608f199ac
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 4%

---


# Adobe Experience Platform 发行说明

**发行日期：2020 年 7 月 15 日**

对Adobe Experience Platform中现有功能的更新：

- [数据管理](#governance)
- [实时客户资料](#profile)
- [分段服务](#segmentation)
- [源](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform数据治理是用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策的一系列战略和技术。 它在各个层次中都起 [!DNL Experience Platform] 着关键作用，包括编目、数据谱系、数据使用标签、数据访问策略和访问控制营销行动的数据。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 在 [!DNL Real-time Customer Data Platform] | 现在，当发生违反操作(包括将区段激 [!DNL Real-time CDP] 活到目标)时，会自动实施数据使用策略。 触发策略违规时，用户可以实时查看激活工作流中的使用限制，从而指明他们无法使用哪些数据以及原因。<br><br>有关详细信息，请参 [阅中的概述](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance) ，参阅“强制实 [!DNL Data Governance] 施数据使用 [!DNL Real-time CDP] 合规性”一节。 |
| Adobe Audience Manager集成 | 与之共享的任何区段 [!DNL Audience Manager] 将继 [!DNL Platform] 承任何已应用的数据使用标签， [!DNL Data Export Controls]反之亦然。 有关使用 [!DNL Audience Manager] 标签和数据 [导出控件之间的特定映射，请参阅文档](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)。 |
| 自定义数据使用标签 | 您现在可以使用策略服务API或在UI中创建自定义数据使用标签。 有关更多 [信息，请参](../../data-governance/labels/overview.md) 阅标签概述。 |

有关该 [服务的更多信息](../../data-governance/home.md) ，请参阅数据管理概述。

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform使您能够为客户提供协调、一致和相关的体验，无论客户在何处或何时与您的品牌互动。 您 [!DNL Real-time Customer Profile]可以看到每个客户的整体视图，该渠道组合了多个的数据，包括在线、离线、CRM和第三方数据。 [!DNL Profile] 允许您将不同的客户数据整合到统一的视图中，为每次客户互动提供一个具有可操作性、时间戳记的帐户。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据使用策略实施 | 在中 [!DNL Real-time Customer Data Platform]，当尝试用户档案工作区中的违规操作时，会自动 [!UICONTROL 显示] 数据使用策略违规。 有关自动 [策略实施的更多信息](#governance) ，请参阅数据管理发行说明。 |

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform分段服务提供用户界面和RESTful API，允许您根据数据构建细分和生成 [!DNL Real-time Customer Profile] 受众。 这些细分集中进行配置和维护， [!DNL Platform]使任何Adobe应用程序都能轻松访问它们。

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准，定义特定的用户档案子集。 细分可以基于记录数据（如人口统计信息）或表示客户与您品牌互动的时间序列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 流细分 | 现在，当数据进入时，流分段可以被限定为用户进入区段，从 [!DNL Platform]而显着缩短了区段限定时间。 流式分段还可以缓解手动运行分段作业的需求。 |
| 数据使用策略实施 | 在中 [!DNL Real-time Customer Data Platform]，当尝试在“区段”工作区中执行违规操作时，数据使用策略 [!UICONTROL 违规会] 自动出现。 有关自动 [策略实施的更多信息](#governance) ，请参阅数据管理发行说明。 |

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
