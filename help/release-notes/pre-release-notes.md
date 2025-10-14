---
title: Experience Platform预发行说明
description: Adobe Experience Platform最新发行说明预览。
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 9cf809f8fd6e424b4dcd800c3d554e4eb0e337dc
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 33%

---

# Adobe Experience Platform预发行说明

>[!IMPORTANT]
>
>本文档旨在作为当月发行说明的&#x200B;**预览**。 版本项目可能会发生更改，并且可能会在最终版本中添加或删除。

>[!TIP]
>
>有关其他 Adobe Experience Platform 应用程序的发行说明，请参阅以下文档：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/releases/pre-release-notes)
>- [联合受众构成](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hans/docs/real-time-cdp-collaboration/using/latest)

**发行日期：2025年10月**

Adobe Experience Platform 中新功能和现有功能的更新：

- [警报](#alerts)
- [目标](#destinations)
- [Segmentation Service](#segmentation-service)
- [源](#sources)

## 警报 {#alerts}

Experience Platform 允许您订阅各种 Experience Platform 活动的基于事件的警报。您可以通过 Experience Platform 用户界面中的[!UICONTROL 警报]选项卡订阅不同的警报规则，并可以选择在用户界面内或通过电子邮件通知接收警报消息。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 目标失败率警报 | 已添加目标的新警报： **目标失败率超过阈值**。 此警报在数据激活期间失败的记录数超过允许的阈值时通知您，使您能够快速响应激活问题。 |

{style="table-layout:auto"}

有关警报的更多信息，请阅读 [[!DNL Observability Insights] 概述](../observability/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预建的与目标平台的集成，可实现从 Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例。

**新增或更新目标**

| 目标 | 描述 |
| --- | --- |
| [!DNL AdForm] | 使用此目标可根据Adobe Real-Time CDP ID (ECID)和[!DNL AdForm]的ID Fusion将Experience Cloud受众发送到[!DNL AdForm]以进行激活。 [!DNL AdForm]的ID Fusion是一种ID解析服务，它允许您根据Experience Cloud ID (ECID)激活第一方受众。 |
| `Amazon Ads` | 我们添加了其他个人标识符支持，如`firstName`、`lastName`、`street`、`city`、`state`、`zip`和`country`。 将这些字段映射为目标标识可以提高受众匹配率。 |

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持[!DNL AES256]目标中的[!DNL Amazon S3]服务器端加密 | [!DNL Amazon S3]目标现在支持[!DNL AES256]服务器端加密，可为导出的数据提供增强的安全性。 您可以在设置或更新[!DNL Amazon S3]目标连接时配置此加密方法，确保使用行业标准[!DNL AES256]加密算法静态加密数据。 有关更多信息，请阅读该 [[!DNL Amazon] 文档](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingEncryption.html)。 |
| [多个支持受众级别监视的新目标](../dataflows/ui/monitor-destinations.md#audience-level-view) | 以下目标现在支持受众级别的监控： <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>[!DNL Salesforce Marketing Cloud]帐户参与度</li><li>[!DNL The Trade Desk]</li></ul> |
| 数据集导出护栏修复 | 已修复数据集导出护栏。 以前，某些包含时间戳列但基于XDM体验事件架构&#x200B;_而非_&#x200B;的数据集被错误地视为体验事件数据集，因此将导出限制为365天的回溯时段。 记录的365天回顾护栏现在仅适用于Experience Events数据集。 使用XDM体验事件架构以外的任何架构的数据集现在受100亿记录护栏的控制。 一些客户可能会看到数据集的导出数量增加，这错误地落到了365天的回看窗口下面。 这使您能够为具有较长回溯时段的预测工作流导出数据集。 有关详细信息，请阅读[数据集导出护栏](../destinations/guardrails.md#dataset-exports)。 |
| 增强了企业目标的受众级别报表 | 改进了企业目标的受众级别报表逻辑。 在此版本之后，客户将看到更准确的受众报表编号，其中仅包含与所选目标相关的受众。 这种监控调整可确保报表仅包含映射到数据流的受众，从而更清楚地了解实际的数据激活。 这不会影响正在激活的数据量 — 它纯粹是为了提高报告准确性而提供的监视增强功能。 |

有关更多信息，请阅读[目标概述](../destinations/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。受众可以基于记录型数据（如人口统计信息）或时间序列事件（代表客户与品牌的互动行为）进行构建。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 流式分段监控 | 流式客户细分的实时监控在沙盒、数据集和受众级别提供了评估率、延迟和数据质量量度的透明度。 该功能支持主动预警和可操作的洞察，以帮助数据工程师识别容量违规和摄取问题。监测指标包括评估率、P95摄取延迟以及接收、评估、失败和跳过的记录。 逐个数据集查看和逐个受众查看功能可全面查看符合条件或被取消资格的净新用户档案。 |

有关详细信息，请参阅 [[!DNL Segmentation Service]  概述](../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新源或已更新的源**

| 来源 | 描述 |
| --- | --- |
| 忠诚度数据的[!BADGE Beta]{type=Informative} [!DNL Talon.one]源 | 使用[!DNL Talon.One]源将批次和忠诚度数据流式传输到Experience Platform。 该连接器支持流式传输用户档案数据、交易数据和忠诚度数据，包括获得的点数、兑换的点数、过期的点数和层级数据。 |

**已更新源**

| 来源 | 描述 |
| --- | --- |
| [!DNL Google Ads]源的正式可用性（仅限API） | [!DNL Google Ads]源的API版本现在已正式发布。 API文档已更新，以反映最新版本现在为`v21`，并且Experience Platform支持所有版本v19及更高版本。 UI版本仍为测试版，仅支持一次性摄取。 要使用增量数据摄取，请使用API路由。 |
| [!DNL Azure Event Hubs]虚拟网络支持 | Adobe现在明确支持到Azure事件中心的虚拟网络连接，从而支持通过专用网络而不是公共网络传输数据。 客户可以允许列表Experience Platform VNet通过Azure专用主干私密路由事件中心流量，为数据摄取工作流提供增强的安全性和合规性。 |

有关更多信息，请阅读[来源概述](../sources/home.md)。
