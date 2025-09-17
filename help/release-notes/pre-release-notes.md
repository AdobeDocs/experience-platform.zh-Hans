---
title: Experience Platform预发行说明
description: Adobe Experience Platform最新发行说明预览。
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: c592d007932835f5263d7f78b2e8155790313840
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 45%

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

**发行日期：2025年9月**

Adobe Experience Platform 中新功能和现有功能的更新：

- [AI 助手](#ai-assistant)
- [警报](#alerts)
- [目标](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [查询服务](#query-service)
- [实时客户轮廓](#profile)
- [Segmentation Service](#segmentation-service)
- [源](#sources)

## AI 助手 {#ai-assistant}

Adobe Experience Platform AI Assistant是一种对话式体验，可用于跨Adobe Experience Cloud应用程序加速和优化工作流。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| Agent Orchestrator | Adobe Experience Platform Agent Orchestrator是支持AI Assistant的智能层。 当您提出问题或请求帮助时，Agent Orchestrator会自动致电专业代理，以便为您提供正确的答案。 Agent Orchestrator会记住您的对话历史记录，使您能够自然地发展以前的问题，而无需重复上下文，并结合来自多个代理的洞察，为您提供清晰、统一的响应。 |
| Audience Agent | 通过Audience Agent，您可以查看关于受众的分析，包括检测受众规模的显着变化、检测重复的受众、探索受众库，以及检索受众规模。 |

有关更多信息，请阅读 [AI 助手概述](../ai-assistant/home.md)。

## 警报 {#alerts}

Experience Platform 允许您订阅各种 Experience Platform 活动的基于事件的警报。您可以通过 Experience Platform 用户界面中的[!UICONTROL 警报]选项卡订阅不同的警报规则，并可以选择在用户界面内或通过电子邮件通知接收警报消息。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 流配置文件摄取警报 | 现在，您可以订阅两个新的警报，以便在数据流级别进行流式摄取： <ul><li>超过了流摄取失败率</li><li>超过了流摄取的跳过率</li></ul> 当超过默认阈值或您定义的自定义阈值时，平台内警报或电子邮件警报将通知您。 有关详细信息，请参阅[配置文件警报](../observability/alerts/rules.md#profile)指南。 |

{style="table-layout:auto"}

有关警报的更多信息，请阅读[[!DNL Observability Insights] 概述](../observability/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预建的与目标平台的集成，可实现从 Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例。

**新增或更新目标**

| 目标 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Snowflake Batch]连接器 | 新[!DNL Snowflake Batch]连接器现已可用，为特定用例提供流连接器的替代方法。 |
| [!DNL Adform] 目标 | [!DNL Adform]是计划媒体购买和销售解决方案的领先提供商。 通过将Adform连接到Adobe Experience Platform，您可以根据Experience Cloud ID (ECID)通过Adform激活第一方受众。 |
| 支持[!DNL Data Landing Zone]加密 | 现在，您可以附加RSA格式公钥来加密导出的文件，从而为您提供与其他云存储目标相同的敏感信息安全级别。 |
| [!DNL Pinterest]目标的身份验证到期详细信息 | 现在，您可以直接在 Experience Platform 界面中查看关于 [!DNL Pinterest] 目标的身份验证到期的信息，您可以查看您的身份验证何时到期，在因其而导致您的数据流中断之前将其更新。您可以从&#x200B;**[[!UICONTROL 帐户]](../destinations/ui/destinations-workspace.md#accounts)**&#x200B;或&#x200B;**[[!UICONTROL 浏览]](../destinations/ui/destinations-workspace.md#browse)**&#x200B;选项卡中的&#x200B;**[!UICONTROL 帐户到期日期]**&#x200B;列监控您的令牌到期日期。 |

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| Experience Platform UI中增强的目标管理功能 | 使用[[!UICONTROL 浏览]](../destinations/ui/destinations-workspace.md#browse)和[[!UICONTROL 帐户]](../destinations/ui/destinations-workspace.md#accounts)选项卡中的新排序功能改进目标管理工作流。 现在，您还可以在帐户身份验证即将过期时看到一个视觉标志。 |

有关更多信息，请阅读[目标概述](../destinations/home.md)。

## 体验数据模型 (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Experience Platform 的数据提供常用的结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 基于模型的架构 | 使用基于模型的架构简化您的数据建模。现在，您可以通过全面的操作示例和指导更轻松地创建架构。此功能目前可供Campaign Orchestration许可证持有人使用，并将在正式发布时扩展到Data Distiller客户，从而使数据建模更易于访问且更有效。 该功能包括对时间序列数据和变更数据捕获功能的支持。 |

有关详细信息，请参阅 [XDM 概述](../xdm/home.md)。

## 实时客户轮廓 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。利用实时客户轮廓，您可以看到每个客户的整体视图，其中结合来自多个渠道的数据，包括在线、离线、CRM 和第三方数据。轮廓允许您将客户数据整合到一个统一视图中，并为每一次客户交互提供可操作的、有时间戳的描述。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 配置文件查看器增强功能 | 2025年9月版本包括以下对Profile查看器的增强功能。 <ul><li>**组合视图**：属性、事件和分析已组合到单个视图中。</li><li>**AI生成的分析**：配置文件详细信息页面现在显示AI生成的分析，让您知道从配置文件生成的详细信息。 这些见解可能包括倾向分数和趋势分析等信息。</li><li>**样式更新**：个人资料详细信息页面已更新为可见内容。</li><li>**浏览**：您现在可以通过交互式基于卡片的轮播来浏览配置文件，该轮播具有搜索和自定义功能。</li></ul> |

有关详细信息，请阅读[实时客户资料概述](../profile/home.md)。

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

有关详细信息，请参阅 [[!DNL Segmentation Service]  概述](../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 正式发布的新源 | 以下源现已正式发布：多个源连接器已从Beta更新为GA： <ul><li>[Acxiom数据摄取](../sources/connectors/data-partners/acxiom-data-ingestion.md)</li><li>[Acxiom目标客户数据摄取](../sources/connectors/data-partners/acxiom-prospecting-data-import.md)</li><li>[Merkury Enterprise](../sources/connectors/data-partners/merkury.md)</li><li>[SAP Commerce](../sources/connectors/ecommerce/sap-commerce.md)</li></ul>。这些源现在完全受支持，并可供生产使用。 |
| [!DNL Snowflake]密钥对身份验证支持 | 增强了Snowflake连接的安全性，支持密钥对身份验证。 基本身份验证（用户名/密码）将于2025年11月被弃用，因此建议客户迁移到密钥对身份验证以提高安全性。 |

有关更多信息，请阅读[来源概述](../sources/home.md)。