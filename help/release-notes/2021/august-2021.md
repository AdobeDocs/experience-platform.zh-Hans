---
title: Adobe Experience Platform发行说明2021年8月
description: Adobe Experience Platform 2021年8月版发行说明。
doc-type: release notes
last-update: August 25, 2021
author: ens28527
exl-id: 0513b9dc-b16c-43b3-8e17-4be4499308d4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 8 月 25 日**

Adobe Experience Platform 现有功能的更新包括：

- [目标](#destinations)
- [可观察性洞察](#observability)
- [实时客户资料](#profile)
- [源](#sources)

## 目标 {#destinations}

目标是与目标平台预建的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用目标为跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例激活已知和未知数据。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | “飞艇属性”目标（以前为测试版）现已正式推出。 |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | 飞艇标记目标（以前为测试版）现已正式推出。 |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | Braze目标（以前为测试版）现已正式推出。 |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | 通过Pinterest客户列表目标，您可以从客户列表、访问过您的网站的人或已在Pinterest上与您的内容交互的人创建受众。 |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | 在Twitter中定位现有关注者和客户，并通过激活在Adobe Experience Platform中构建的受众来创建相关的再营销活动。 |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX是一个汇总Verizon Media/Yahoo基础架构，它托管着各种组件，使Verizon Media/Yahoo能够与其外部合作伙伴以安全、自动和可伸缩的方式交换数据。 |

**新增功能**

| 功能 | 描述 |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Adobe Experience Platform Destination SDK是一套配置API，允许您为Experience Platform配置目标集成模式，以根据所选的数据和身份验证格式向端点交付受众和配置文件数据。 配置存储在Experience Platform中，可通过API检索以进行其他更新。 |
| [对目标的可用性改进](../../destinations/ui/activation-overview.md) | 对目标的可用性改进使营销人员能够无缝地激活现有目标的区段。 |

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 可观察性洞察 {#observability}

可观察性分析允许您通过使用统计指标和事件通知来监控Platform活动。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 警报 | 您现在可以订阅与Platform上运行的工作流相关的重要警报。 在订阅特定的警报规则后，您将在发生重要生命周期事件（例如成功的数据摄取）或存在需要您关注的问题（例如摄取流失败或区段作业耗时超过预期）时，收到UI内通知和电子邮件。 欲了解更多信息，请参见 [警报概述](../../observability/alerts/overview.md). |

请参阅 [可观察性分析概述](../../observability/home.md) 以了解有关该服务的更多信息。

## 实时客户资料 {#profile}

通过Adobe Experience Platform，无论客户在何处或何时与您的品牌互动，您都可以为其推动协调、一致且相关的体验。 利用实时客户档案，您可以查看合并了来自多个渠道（包括在线、离线、CRM和第三方数据）的数据的每个单个客户的整体视图。 用户档案允许您将客户数据整合到一个统一的视图中，并提供每个客户互动的可操作、带时间戳的帐户。

| 功能 | 描述 |
| ------- | ----------- |
| 按合并策略或标识浏览配置文件 | 在Experience Platform中浏览配置文件时，您现在可以按合并策略浏览，以根据选定的合并策略预览20个示例配置文件。 您还可以按身份浏览，以使用身份命名空间和相关身份值搜索特定配置文件。 欲了解更多信息，请参见 [Real-Time Customer Profile用户界面指南](../../profile/ui/user-guide.md). |

要了解有关Real-time Customer Profile的更多信息，包括有关使用用户档案数据的教程和最佳实践，请从阅读 [Real-time Customer Profile概述](../../profile/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

| 功能 | 描述 |
| ------- | ----------- |
| 本地文件上传源连接器 | 文件摄取类别已重命名为本地系统，允许您使用本地文件上传连接器将本地文件直接带入Platform。 通过此连接器摄取的数据可以通过监控功能板进行监控。 请参阅 [本地文件上传源概述](../../sources/connectors/local-system/local-file-upload.md) 了解更多信息。 |

要了解有关源的更多信息，请参阅 [源概述](../../sources/home.md).
