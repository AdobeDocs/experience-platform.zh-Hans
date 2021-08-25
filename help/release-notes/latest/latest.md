---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform的最新发行说明。
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: b1dca51264582788ccbde005b063c57e2f3edc8f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 8%

---


# Adobe Experience Platform 发行说明

**发行日期：2021 年 25 月 8 日**

Adobe Experience Platform 现有功能的更新包括：

- [目标](#destinations)
- [可观察性洞察](#observability)
- [Real-time Customer Profile](#profile)
- [源](#sources)

## 目标 {#destinations}

目标是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| [改进了目标的可用性](../../destinations/ui/activation-overview.md) | 目标的可用性改进使营销人员能够将区段无缝地激活到现有目标。 |

有关目标的更多常规信息，请参阅[目标概述](../../destinations/home.md)。

## 可观察性洞察 {#observability}

可观察性分析允许您通过使用统计量度和事件通知来监视平台活动。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 警报 | 您现在可以订阅与平台上运行的工作流相关的重要警报。 订阅特定警报规则后，当发生重要的生命周期事件（例如成功数据摄取）或存在需要您注意的问题（例如摄取流失败或区段作业花费比预期的时间长）时，您将收到UI内通知和电子邮件。 有关更多信息，请参阅[警报概述](../../observability/alerts/overview.md)。 |

有关该服务的更多信息，请参阅[可观测性分析概述](../../observability/home.md) 。

## 实时客户资料 {#profile}

Adobe Experience Platform使您能够为客户在何处或何时与您的品牌进行交互，从而提供协调、一致的相关体验。 通过实时客户资料，您可以查看每个客户的整体视图，该视图将来自多个渠道的数据（包括在线、离线、CRM和第三方数据）进行整合。 利用用户档案，可将客户数据整合到统一视图中，为每次客户互动提供一个加盖时间戳的可操作帐户。

| 功能 | 描述 |
| ------- | ----------- |
| 按合并策略或标识浏览用户档案 | 现在，在Experience Platform中浏览用户档案时，您可以按合并策略浏览，以根据选定的合并策略预览20个示例用户档案。 您还可以按身份浏览，以便使用身份命名空间和相关身份值搜索特定的配置文件。 有关更多信息，请参阅[Real-time Customer Profile UI指南](../../profile/ui/user-guide.md)。 |

要了解有关实时客户资料的更多信息，包括有关使用资料数据的教程和最佳实践，请首先阅读[实时客户资料概述](../../profile/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

| 功能 | 描述 |
| ------- | ----------- |
| 本地文件上传源连接器 | 文件摄取类别已重命名为本地系统，允许您使用本地文件上传连接器将本地文件直接导入到平台。 通过此连接器摄取的数据可通过监控仪表板进行监控。 有关更多信息，请参阅[本地文件上载源概述](../../sources/connectors/local-system/local-file-upload.md) 。 |

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
