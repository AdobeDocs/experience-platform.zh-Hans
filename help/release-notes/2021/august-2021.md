---
title: Adobe Experience Platform 发行说明（2021 年 8 月）
description: Adobe Experience Platform 的 2021 年 8 月发行说明。
doc-type: release notes
last-update: August 25, 2021
author: ens28527
exl-id: 0513b9dc-b16c-43b3-8e17-4be4499308d4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 36%

---

# Adobe Experience Platform 发行说明

**发行日期： 2021年8月25日**

Adobe Experience Platform 中现有功能的更新：

- [目标](#destinations)
- [可观察性洞察](#observability)
- [实时客户轮廓](#profile)
- [源](#sources)

## 目标 {#destinations}

目标是预先构建的与目标平台的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | 飞艇属性目标（以前为测试版）现已公开发布。 |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | 飞艇标记目标以前为测试版，现已正式推出。 |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | Braze目标以前是Beta版，现已正式提供。 |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | 利用Pinterest客户列表目标，您可以从客户列表、访问过您网站的人或已在Pinterest上与您的内容互动的人创建受众。 |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | 在Twitter中定位现有的关注者和客户，并通过激活在Adobe Experience Platform中构建的受众来创建相关的再营销活动。 |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX是一个聚合的Verizon Media/Yahoo基础架构，它托管着各种组件，使Verizon Media/Yahoo能够以安全、自动化和可扩展的方式与外部合作伙伴交换数据。 |

**新增功能**

| 功能 | 描述 |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Adobe Experience Platform Destination SDK是一套配置API，可让您为Experience Platform配置目标集成模式，以根据所选数据和身份验证格式向您的端点交付受众和配置文件数据。 配置存储在Experience Platform中，可以通过API检索以获取其他更新。 |
| [目标的可用性改进](../../destinations/ui/activation-overview.md) | 对目标的可用性改进使营销人员可以无缝地激活现有目标的区段。 |

有关目标的更多一般信息，请参阅[目标概述](../../destinations/home.md)。

## 可观察性洞察 {#observability}

可观察性分析允许您通过使用统计指标和事件通知来监控Experience Platform活动。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 警报 | 现在，您可以订阅与Experience Platform上运行的工作流相关的重要提醒。 在订阅特定的警报规则后，当发生重要的生命周期事件（例如成功的数据摄取）或存在需要您关注的问题（例如摄取流失败或区段作业耗时超过预期）时，您将收到UI内通知和电子邮件。 有关详细信息，请参阅[警报概述](../../observability/alerts/overview.md)。 |

有关该服务的更多信息，请参阅[可观察性分析概述](../../observability/home.md)。

## 实时客户轮廓 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。利用实时客户轮廓，您可以看到每个客户的整体视图，其中结合来自多个渠道的数据，包括在线、离线、CRM 和第三方数据。轮廓允许您将客户数据整合到一个统一视图中，并为每一次客户交互提供可操作的、有时间戳的描述。

| 功能 | 描述 |
| ------- | ----------- |
| 按合并策略或身份浏览配置文件 | 在Experience Platform中浏览配置文件时，您现在可以按合并策略浏览，根据所选的合并策略预览20个示例配置文件。 您还可以按身份浏览，以使用身份命名空间和相关身份值搜索特定配置文件。 有关详细信息，请参阅[实时客户个人资料UI指南](../../profile/ui/user-guide.md)。 |

要详细了解实时客户轮廓，包括使用轮廓数据的教程和最佳实践，请首先阅读[实时客户轮廓概述](../../profile/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

| 功能 | 描述 |
| ------- | ----------- |
| 本地文件上传源连接器 | 文件摄取类别已重命名为本地系统，使您可以使用本地文件上传连接器直接将本地文件带入Experience Platform。 通过此连接器摄取的数据可以通过监控仪表板进行监控。 有关详细信息，请参阅[本地文件上载源概述](../../sources/connectors/local-system/local-file-upload.md)。 |

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
