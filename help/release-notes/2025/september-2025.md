---
title: Adobe Experience Platform 发行说明（2025 年 9 月）
description: Adobe Experience Platform 2025 年 9 月发行说明。
exl-id: 9c5ab487-22b8-4590-b4ea-abec0f377703
source-git-commit: d2694170e2860bd32783ad3f1860b0397e847289
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 98%

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

**发行日期：2025 年 9 月 23 日**

Adobe Experience Platform 中新功能和现有功能的更新：

- [Agent Orchestrator](#agent-orchestrator)
- [警报](#alerts)
- [目标](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [实时客户轮廓](#profile)
- [Segmentation Service](#segmentation-service)
- [源](#sources)

## Agent Orchestrator {#agent-orchestrator}

Adobe Experience Platform Agent Orchestrator 是 Adobe Experience Platform 中新的代理式层。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| Agent Orchestrator | Adobe Experience Platform Agent Orchestrator 是 Adobe Experience Platform 中新的代理式层。Experience Platform Agent Orchestrator 旨在利用平台的丰富数据和客户知识，为专门构建的专业 Adobe Experience Platform 代理赋予智能和推理功能，使后者在人为监督下大规模地快速执行复杂的决策和问题解决任务。当您在 AI 助手这类对话界面中用自然语言提出问题或请求帮助时，Agent Orchestrator 会自动调用专门的代理来为您提供正确的回答。Agent Orchestrator 会记住您的对话历史，使您能够自然地延续以前的问题，无需重复上下文，它还会结合来自多个代理的洞察，为您提供清晰、统一的回答。有关更多信息，请阅读 [Agent Orchestrator 文档](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)。 |
| Audience 代理 | 通过 Audience 代理，您可以获得关于受众的洞察，包括发现显著的受众规模变化、发现重复的受众、浏览您的受众库存以及检索受众规模。有关更多信息，请阅读 [Audience 代理文档](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-ai/experience-cloud-ai/agents/audience)。 |

有关更多信息，请阅读 [Agent Orchestrator 文档](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-ai/experience-cloud-ai/home)。

## 警报 {#alerts}

Experience Platform 允许您订阅各种 Experience Platform 活动的基于事件的警报。您可以通过 Experience Platform 用户界面中的[!UICONTROL 警报]选项卡订阅不同的警报规则，并可以选择在用户界面内或通过电子邮件通知接收警报消息。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 流式摄取轮廓警报 | 现在，您可以订阅数据流级别流式摄取的两个新警报： <ul><li>超出了流式摄取失败率</li><li>超出了流式摄取跳过率</li></ul> 如果实际值超过了默认阈值或您设定的自定义阈值时，就会通过平台内警报或电子邮件警报通知您。更多信息请阅读[轮廓警报](../../observability/alerts/rules.md#profile)指南。 |

{style="table-layout:auto"}

有关警报的更多信息，请阅读 [[!DNL Observability Insights] 概述](../../observability/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预建的与目标平台的集成，可实现从 Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例。

**新增或更新目标**

| 目标 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [[!DNL Snowflake Batch]](../../destinations/catalog/cloud-storage/snowflake-batch.md)连接器 | 现在提供一种新的 [!DNL Snowflake Batch] 连接器，可为特定用例提供一种流传输连接器的替代方法。 |
| 支持 [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) 加密 | 现在，您可以附加 RSA 格式的公钥来加密导出的文件，这为您的敏感信息提供了与其他云存储目标所提供的相同安全等级。 |
| [[!DNL Pinterest]](../../destinations/catalog/advertising/pinterest.md) 目标的身份验证有效期限详细信息 | 现在，您可以直接在 Experience Platform 界面中查看关于 [!DNL Pinterest] 目标的身份验证到期的信息，您可以查看您的身份验证何时到期，在因其而导致您的数据流中断之前将其更新。您可以从&#x200B;**[[!UICONTROL 帐户]](../../destinations/ui/destinations-workspace.md#accounts)**&#x200B;或&#x200B;**[[!UICONTROL 浏览]](../../destinations/ui/destinations-workspace.md#browse)**&#x200B;选项卡中的&#x200B;**[!UICONTROL 帐户到期日期]**&#x200B;列监控您的令牌到期日期。 |

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| 增强了 Experience Platform UI 中的目标管理功能 | 通过[[!UICONTROL 浏览]](../../destinations/ui/destinations-workspace.md#browse)和[[!UICONTROL 帐户]](../../destinations/ui/destinations-workspace.md#accounts)选项卡中新增的排序功能改进您的目标管理工作流。现在，您还可以在帐户身份验证即将过期时看到一个指示器。<br> ![](../../destinations/assets/ui/workspace/expired-accounts.png){width="100" zoomable="yes"} |
| 永久性列宽设置 | 现在，当您离开一个页面之后又重新返回该页面时，列宽设置会保留。例如，如果您在[[!UICONTROL 浏览]](../../destinations/ui/destinations-workspace.md#browse)选项卡中调整了列宽，当您离开此选项卡之后又再返回时，您自定义的列宽将保持不变。 |

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## 体验数据模型 (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Experience Platform 的数据提供常用的结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 基于模型的架构 | 使用基于模型的架构简化您的数据建模。现在，您可以通过全面的操作示例和指导更轻松地创建架构。此功能目前可供营销活动编排许可证持有者使用，未来将扩展到 GA 的数据蒸馏器客户，使数据建模更易于访问、更高效。此功能包括对时间序列数据和变更数据捕获功能的支持。 |

有关详细信息，请参阅 [XDM 概述](../../xdm/home.md)。

<!--

| Data Mirror | Ingest row-level changes from cloud data warehouses (e.g., Snowflake, Databricks, BigQuery) into Adobe Experience Platform using model-based schemas. Data Mirror eliminates upstream ETL and preserves relationships, versioning, and deletions by mirroring existing database structures directly into the data lake. Time-series and record event schema behavior with change data capture capabilities are all supported. This feature is currently available for Campaign Orchestration license holders and will expand through this limited release, also including Customer Journey Analytics customers. See the [Data Mirror documentation](../../xdm/data-mirror/overview.md) for more details. Contact your Adobe representative for access. |
-->

## 实时客户轮廓 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。利用实时客户轮廓，您可以看到每个客户的整体视图，其中结合来自多个渠道的数据，包括在线、离线、CRM 和第三方数据。轮廓允许您将客户数据整合到一个统一视图中，并为每一次客户交互提供可操作的、有时间戳的描述。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| [!BADGE Alpha]{type=Informative}此功能当前位于Alpha中。 轮廓查看器增强功能 | 2025 年 9 月发行的版本包括以下关于轮廓查看器的增强功能。 <ul><li>**组合视图**：将属性、事件和洞察组合到同一个视图中。</li><li>**AI 生成的洞察**：轮廓详细信息页面现在显示 AI 生成的洞察，让您了解从轮廓生成的详细信息。这些洞察可能包括倾向性得分和趋势分析等信息。</li><li>**样式更新**：轮廓详细信息页面更新了外观。</li><li>**浏览**：您现在可以通过一个具有搜索和自定义功能的基于信息卡的交互式轮播组件来浏览轮廓。</li></ul> |

更多信息请阅读[实时客户轮廓概述](../../profile/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。受众可以基于记录型数据（如人口统计信息）或时间序列事件（代表客户与品牌的互动行为）进行构建。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 弃用带有体验事件的帐户受众 | B2B 架构升级后，不再支持带有体验事件的帐户受众。请改用新的区段嵌套方法：创建一个带有体验事件的“人员”受众，然后在创建“帐户”受众时引用这个“人员”受众。这为创建 B2B 受众提供了一种更灵活的可维护的方法。 |

**重要更新**

| 更新 | 描述 |
| ------- | ----------- |
| 受众估计值自动刷新回退 | 受众估计值的自动刷新增强功能已回退。受众估计值将继续在区段生成器中生成，自动刷新功能已移除。 |
| 外部受众 | 从 9 月 30 日开始，将通过区段生成器中的统一搜索功能检索外部受众。如果您使用区段匹配，就可以启用区段生成器中的旧版体验。 |

有关详细信息，请参阅 [[!DNL Segmentation Service]  概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 正式发布中的新来源 | 正式发布中现在包含以下来源：多个源连接器已从 Beta 版更新为正式发布： <ul><li>[Acxiom 数据摄取](../../sources/connectors/data-partners/acxiom-data-ingestion.md)</li><li>[Acxiom 潜在客户数据摄取](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md)</li><li>[Merkury Enterprise](../../sources/connectors/data-partners/merkury.md)</li><li>[SAP Commerce](../../sources/connectors/ecommerce/sap-commerce.md)</li></ul>。这些来源现在完全受支持，可供生产使用。 |
| 支持 [!DNL Snowflake] 密钥对身份验证 | 增强了 Snowflake 连接的安全性，支持密钥对身份验证。2025 年 11 月将弃用基本身份验证（用户名/密码），因此建议客户迁移到密钥对身份验证，以提高安全性。有关更多信息，请阅读该 [[!DNL Snowflake] 文档](../../sources/connectors/databases/snowflake.md)。 |
| [!BADGE Beta]{type=Informative} [!DNL Capillary Streaming Events] | 使用此 [[!DNL Capillary Streaming Events] 来源](../../sources/connectors/loyalty/capillary.md)将忠诚度数据从您的 [!DNL Capillary] 帐户流式传输到 Experience Platform。 |
| [!BADGE Beta]{type=Informative} [!DNL Relay Connector] | 使用[[!DNL Relay Connector]](../../sources/tutorials/ui/create/marketing-automation/relay-connector.md)将[!DNL Relay Network]集成中的事件数据流式传输到Experience Platform中。 |
| 正式提供来源中的专用链接支持 | 您现在可以为一组选定的来源使用&#x200B;**专用链接**。使用此功能可以创建一个可以与来源连接的私有端点。使用私有端点，您可以设置绕过公共互联网的连接和数据流，从而为您的敏感数据提供更强的安全性和网络隔离。以下来源提供对专用链接的支持： <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li></ul>。有关详细信息，请参阅 [API](../../sources/tutorials/api/private-link.md) 和 [UI](../../sources/tutorials/ui/private-link.md) 中的专用链接创建指南。 |

有关更多信息，请阅读[来源概述](../../sources/home.md)。