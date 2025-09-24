---
title: Adobe Experience Platform 发行说明（2025 年 8 月）
description: Adobe Experience Platform 的 2025 年 8 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: ac180f045dd3cc7e8ad9de702a3672630d668ee5
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 40%

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

**发行日期： 2025年9月23日**

Adobe Experience Platform 中新功能和现有功能的更新：

- [Agent Orchestrator](#agent-orchestrator)
- [警报](#alerts)
- [目标](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [实时客户轮廓](#profile)
- [Segmentation Service](#segmentation-service)
- [源](#sources)

## Agent Orchestrator {#agent-orchestrator}

Adobe Experience Platform Agent Orchestrator是Adobe Experience Platform中的新代理层。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| Agent Orchestrator | Adobe Experience Platform Agent Orchestrator是Adobe Experience Platform中的新代理层。 Experience Platform Agent Orchestrator旨在利用平台丰富的数据和客户知识，为专门构建的Adobe Experience Platform Agent专家提供智能和推理功能，使他们能够快速大规模地执行复杂的决策和问题解决任务，所有这些都由人为监督。 当您在像AI Assistant这样的对话界面中通过自然语言提出问题或请求帮助时，Agent Orchestrator会自动调用专业代理以获得正确的答案。 Agent Orchestrator会记住您的对话历史记录，使您能够自然地发展以前的问题，而无需重复上下文，并结合来自多个代理的洞察，为您提供清晰、统一的响应。 有关详细信息，请阅读[Agent Orchestrator文档](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)。 |
| Audience Agent | 通过Audience Agent，您可以查看关于受众的分析，包括检测受众规模的显着变化、检测重复的受众、探索受众库，以及检索受众规模。 有关详细信息，请阅读[Audience Agent文档](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/audience)。 |

有关详细信息，请阅读[Agent Orchestrator文档](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/home)。

## 警报 {#alerts}

Experience Platform 允许您订阅各种 Experience Platform 活动的基于事件的警报。您可以通过 Experience Platform 用户界面中的[!UICONTROL 警报]选项卡订阅不同的警报规则，并可以选择在用户界面内或通过电子邮件通知接收警报消息。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 流配置文件摄取警报 | 现在，您可以订阅两个新的警报，以便在数据流级别进行流式摄取： <ul><li>超过了流摄取失败率</li><li>超过了流摄取的跳过率</li></ul> 当超过默认阈值或您定义的自定义阈值时，平台内警报或电子邮件警报将通知您。 有关详细信息，请参阅[配置文件警报](../../observability/alerts/rules.md#profile)指南。 |

{style="table-layout:auto"}

有关警报的更多信息，请阅读[[!DNL Observability Insights] 概述](../../observability/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预建的与目标平台的集成，可实现从 Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例。

**新增或更新目标**

| 目标 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [[!DNL Snowflake Batch]](../../destinations/catalog/cloud-storage/snowflake-batch.md)连接器 | 新[!DNL Snowflake Batch]连接器现已可用，为特定用例提供流连接器的替代方法。 |
| 支持[[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)加密 | 现在，您可以附加RSA格式公钥来加密导出的文件，从而为您提供与其他云存储目标相同的敏感信息安全级别。 |
| [[!DNL Pinterest]](../../destinations/catalog/advertising/pinterest.md)目标的身份验证到期详细信息 | 现在，您可以直接在 Experience Platform 界面中查看关于 [!DNL Pinterest] 目标的身份验证到期的信息，您可以查看您的身份验证何时到期，在因其而导致您的数据流中断之前将其更新。您可以从&#x200B;**[[!UICONTROL 帐户]](../../destinations/ui/destinations-workspace.md#accounts)**&#x200B;或&#x200B;**[[!UICONTROL 浏览]](../../destinations/ui/destinations-workspace.md#browse)**&#x200B;选项卡中的&#x200B;**[!UICONTROL 帐户到期日期]**&#x200B;列监控您的令牌到期日期。 |

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| Experience Platform UI中增强的目标管理功能 | 使用[[!UICONTROL 浏览]](../../destinations/ui/destinations-workspace.md#browse)和[[!UICONTROL 帐户]](../../destinations/ui/destinations-workspace.md#accounts)选项卡中的新排序功能改进目标管理工作流。 现在，您还可以在帐户身份验证即将过期时看到一个视觉标志。<br> ![](../../destinations/assets/ui/workspace/expired-accounts.png){width="100" zoomable="yes"} |
| 持久列宽设置 | 现在，当导航离开页面并返回页面时，列宽设置会保留。 例如，如果在[[!UICONTROL 浏览]](../../destinations/ui/destinations-workspace.md#browse)选项卡中调整列宽，则当您离开并返回该选项卡时，自定义列宽将保持不变。 |

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## 体验数据模型 (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Experience Platform 的数据提供常用的结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 基于模型的架构 | 使用基于模型的架构简化您的数据建模。现在，您可以通过全面的操作示例和指导更轻松地创建架构。此功能目前可供Campaign Orchestration许可证持有人使用，并将在正式发布时扩展到Data Distiller客户，从而使数据建模更易于访问且更有效。 该功能包括对时间序列数据和变更数据捕获功能的支持。 |
| Data Mirror | 使用基于模型的架构，将行级更改从云数据仓库(例如Snowflake、Databricks、BigQuery)摄取到Adobe Experience Platform中。 Data Mirror通过直接将现有数据库结构镜像到数据湖，消除了上游ETL并保留关系、版本控制和删除。 支持具有更改数据捕获功能的时间系列和记录事件模式行为。 此功能目前可供Campaign Orchestration许可证持有人使用，并将在这一有限版本中扩展，包括Customer Journey Analytics客户。 有关更多详细信息，请参阅[Data Mirror文档](../../xdm/data-mirror/overview.md)。 请联系您的Adobe代表以获取访问权限。 |

有关详细信息，请参阅 [XDM 概述](../../xdm/home.md)。

## 实时客户轮廓 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。利用实时客户轮廓，您可以看到每个客户的整体视图，其中结合来自多个渠道的数据，包括在线、离线、CRM 和第三方数据。轮廓允许您将客户数据整合到一个统一视图中，并为每一次客户交互提供可操作的、有时间戳的描述。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 配置文件查看器增强功能 | 2025年9月版本包括以下对Profile查看器的增强功能。 <ul><li>**组合视图**：属性、事件和分析已组合到单个视图中。</li><li>**AI生成的分析**：配置文件详细信息页面现在显示AI生成的分析，让您知道从配置文件生成的详细信息。 这些见解可能包括倾向分数和趋势分析等信息。</li><li>**样式更新**：个人资料详细信息页面已更新为可见内容。</li><li>**浏览**：您现在可以通过交互式基于卡片的轮播来浏览配置文件，该轮播具有搜索和自定义功能。</li></ul> |

有关详细信息，请阅读[实时客户资料概述](../../profile/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。受众可以基于记录型数据（如人口统计信息）或时间序列事件（代表客户与品牌的互动行为）进行构建。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 具有体验事件弃用的帐户受众 | B2B架构升级后，不再支持具有体验事件的帐户受众。 请改用新的“区段划分”方法：通过体验事件创建人员受众，然后在创建帐户受众时引用该人员受众。 这为创建B2B受众提供了更灵活和可维护的方法。 |

**重要更新**

| 更新 | 描述 |
| ------- | ----------- |
| 受众评估自动刷新还原 | 已还原受众估计的自动刷新增强功能。 将继续在区段生成器中生成受众预计值，但已删除自动刷新功能。 |
| 外部受众 | 从9月30日开始，将通过区段生成器中的统一搜索检索外部受众。 如果您使用区段匹配，则可以在区段生成器中启用旧版体验。 |

有关详细信息，请参阅 [[!DNL Segmentation Service]  概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 正式发布的新源 | 以下源现已正式发布：多个源连接器已从Beta更新为GA： <ul><li>[Acxiom数据摄取](../../sources/connectors/data-partners/acxiom-data-ingestion.md)</li><li>[Acxiom目标客户数据摄取](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md)</li><li>[Merkury Enterprise](../../sources/connectors/data-partners/merkury.md)</li><li>[SAP Commerce](../../sources/connectors/ecommerce/sap-commerce.md)</li></ul>。这些源现在完全受支持，并可供生产使用。 |
| [!DNL Snowflake]密钥对身份验证支持 | 增强了Snowflake连接的安全性，支持密钥对身份验证。 基本身份验证（用户名/密码）将于2025年11月被弃用，因此建议客户迁移到密钥对身份验证以提高安全性。 有关更多信息，请阅读该[[!DNL Snowflake] 文档](../../sources/connectors/databases/snowflake.md)。 |
| 在源中正式提供专用链接支持 | 您现在可以为选定的源组使用&#x200B;**专用链接**。 使用此功能可以创建一个可以与来源连接的私有端点。使用私有端点，您可以设置绕过公共互联网的连接和数据流，从而为您的敏感数据提供更强的安全性和网络隔离。对专用链接的支持可从以下来源获得： <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li></ul>。有关详细信息，请参阅在API[中创建专用链接](../../sources/tutorials/api/private-link.md)以及在UI[中创建专用链接](../../sources/tutorials/ui/private-link.md)的指南。 |

有关更多信息，请阅读[来源概述](../../sources/home.md)。

<!--
| [!BADGE Beta]{type=Informative} [!DNL Capillary Streaming Events] | Use the [[!DNL Capillary Streaming Events] source](../../sources/connectors/loyalty/capillary.md) to stream loyalty data from your [!DNL Capillary] account to Experience Platform. |
-->