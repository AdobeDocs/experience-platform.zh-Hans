---
title: Adobe Experience Platform 发行说明（2025 年 10 月）
description: Adobe Experience Platform 的 2025 年 10 月发行说明。
source-git-commit: 199acd8d3bdbb0e89fc1ab881bff4d94063b7f78
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 24%

---

# Adobe Experience Platform 发行说明

>[!TIP]
>
>有关其他 Adobe Experience Platform 应用程序的发行说明，请参阅以下文档：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/releases/pre-release-notes)
>- [联合受众构成](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hans/docs/real-time-cdp-collaboration/using/latest)

**发行日期： 2025年10月22日**

Adobe Experience Platform 中新功能和现有功能的更新：

- [警报](#alerts)
- [目标](#destinations)
- [源](#sources)

## 警报 {#alerts}

Experience Platform 允许您订阅各种 Experience Platform 活动的基于事件的警报。您可以通过Experience Platform用户界面的[!UICONTROL Alerts]选项卡订阅各种警报规则，并且可以选择在UI中或通过电子邮件通知接收警报消息。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 目标失败率警报 | 已添加目标的新警报： **目标失败率超过阈值**。 此警报在数据激活期间失败的记录数超过允许的阈值时通知您，使您能够快速响应激活问题。 有关详细信息，请阅读有关[标准警报规则](../../observability/alerts/rules.md)的文档。 |

{style="table-layout:auto"}

有关警报的更多信息，请阅读 [[!DNL Observability Insights] 概述](../../observability/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预建的与目标平台的集成，可实现从 Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例。

**新增或更新目标**

| 目标 | 描述 |
| --- | --- |
| [!DNL Adform] | 使用此目标可根据Adobe Real-Time CDP ID (ECID)和[!DNL Adform]的ID Fusion将Experience Cloud受众发送到[!DNL Adform]以进行激活。 [!DNL Adform]的ID Fusion是一种ID解析服务，它允许您根据Experience Cloud ID (ECID)激活第一方受众。 有关详细信息，请阅读[[!DNL Adform] 文档](../../destinations/catalog/advertising/adform.md) |
| [!DNL Amazon Ads] | 添加了其他个人标识符支持。 这包括`firstName`、`lastName`、`street`、`city`、`state`、`zip`和`country`等字段。 将这些字段映射为目标标识可以提高受众匹配率。 有关详细信息，请阅读[[!DNL Amazon Ads] 文档](../../destinations/catalog/advertising/amazon-ads.md)。 |

{style="table-layout:auto"}

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持[!DNL AES256]目标中的[!DNL Amazon S3]服务器端加密 | [!DNL Amazon S3]目标现在支持[!DNL AES256]服务器端加密，可为导出的数据提供增强的安全性。 您可以在设置或更新[!DNL Amazon S3]目标连接时配置此加密方法，确保使用行业标准[!DNL AES256]加密算法静态加密数据。 有关更多信息，请阅读该 [[!DNL Amazon] 文档](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingEncryption.html)。 |
| [多个支持受众级别监视的新目标](../../dataflows/ui/monitor-destinations.md#audience-level-view) | 以下目标现在支持受众级别的监控： <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>[!DNL Salesforce Marketing Cloud]帐户参与度</li><li>[!DNL The Trade Desk]</li></ul> |
| 数据集导出护栏修复 | 已修复数据集导出护栏。 以前，某些包含时间戳列但基于XDM体验事件架构&#x200B;_而非_&#x200B;的数据集被错误地视为体验事件数据集，因此将导出限制为365天的回溯时段。 记录的365天回顾护栏现在仅适用于Experience Events数据集。 使用XDM体验事件架构以外的任何架构的数据集现在受100亿记录护栏的控制。 一些客户可能会看到数据集的导出数量增加，这错误地落到了365天的回看窗口下面。 这使您能够为具有较长回溯时段的预测工作流导出数据集。 有关详细信息，请阅读[数据集导出护栏](../../destinations/guardrails.md#dataset-exports)。 |
| 增强了企业目标的受众级别报表 | 在此版本之后，客户将看到更准确的受众报表编号，其中仅包含与所选目标相关的受众。 这种监控调整可确保报表仅包含映射到数据流的受众，从而更清楚地了解实际的数据激活。 这不会影响正在激活的数据量 — 它纯粹是为了提高报告准确性而提供的监视增强功能。 |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

<!--
| [!DNL Snowflake Batch] (Limited availability) | Create a live [!DNL Snowflake] data share to receive daily audience updates directly as shared tables into your account. This integration is currently available for customer organizations provisioned in the VA7 region. |
| [!DNL Snowflake Streaming] (Limited availability) | Create a live [!DNL Snowflake] data share to receive streaming audience updates directly as shared tables into your account. This integration is currently available for customer organizations provisioned in the VA7 region. |
-->

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| Adobe Analytics源的数据集创建更改 | 在Adobe Analytics和Experience Platform之间创建数据流的过程中，会通过目录服务创建一个数据集。 此数据集用作要着陆的数据的容器。 目前，此过程涉及的数据源ID是从Analytics报表包提取、发送到目录服务，然后与新创建的数据集相关联。 更改后，提供数据源ID的选项在数据集创建期间将不再可用。 因此，Analytics源创建的新数据集在目录服务中将不再具有与其关联的数据源ID。 此更改仅适用于元数据，不会以任何方式更改数据集中的数据存储。 但是，请务必知道，目录服务提供的数据源ID在为Adobe Analytics新建的数据集中将不再可用。 有关Adobe Analytics源连接器的更多信息，请阅读[Adobe Analytics源文档](../../sources/connectors/adobe-applications/analytics.md)。 |
| [!DNL Google Ads]源的正式可用性（仅限API） | [源的 [!DNL Google Ads]](../../sources/tutorials/api/create/advertising/ads.md)API版本现在已正式发布。 API文档已更新，以反映最新版本现在为`v21`，并且Experience Platform支持所有版本v19及更高版本。 [UI版本](../../sources/tutorials/ui/create/advertising/ads.md)仍保留在Beta版中，仅支持一次性引入。 要使用增量数据摄取，请使用API路由。 |
| [!DNL Azure Event Hubs]虚拟网络支持 | Adobe现在明确支持到[[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md)的虚拟网络连接，支持通过专用网络而不是公共网络进行数据传输。 客户可以允许列表Experience Platform VNet通过Azure专用主干私密路由事件中心流量，为数据摄取工作流提供增强的安全性和合规性。 |

{style="table-layout:auto"}

有关更多信息，请阅读[来源概述](../../sources/home.md)。

<!--
| Source | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.one] sources for loyalty data | Use the [[!DNL Talon.One] sources](../../sources/connectors/loyalty/talon-one.md) to ingest batch and streaming loyalty data into Experience Platform. The connector supports streaming of profile data, transaction data, and loyalty data including points earned, points redeemed, points expired, and tier data. For more information, read the [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) and [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) documentation. |
-->