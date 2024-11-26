---
title: Adobe Experience Platform发行说明2024年11月
description: Adobe Experience Platform 2024年11月版发行说明。
source-git-commit: d87747c2181f4ae378e1341c3c190cc6fa57d4b0
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 29%

---

# Adobe Experience Platform 发行说明

>[!TIP]
>
>新的[AI助手产品文档登陆页面](../../ai-assistant/landing.md)现已可用。 使用此页作为所有与AI Assistant相关的资源的中心。

**发行日期： 2024年11月26日**

Adobe Experience Platform 中现有功能和文档的更新：

- [AI 助手](#ai-assistant)
- [目标](#destinations)
- [查询服务](#query-service)
- [沙盒](#sandboxes)
- [文档更新](#documentation-updates)
   - [交互式 Experience Platform API 文档](#interactive-experience-platform-api-documentation)
   - [Experience League上的新目录](#new-table-of-contents-on-experience-league)
   - [新的AI助手登陆页面](#new-ai-assistant-landing-page)

## AI 助手 {#ai-assistant}

Adobe Experience Platform 中的 AI 助手是一种对话体验，您可以使用它来加速 Adobe 应用程序中的工作流程。您可以使用 AI 助手更好地了解产品知识、解决问题或搜索信息并找到运营洞察。AI 助手支持 Experience Platform、Real-time Customer Data Platform、Adobe Journey Optimizer 和 Customer Journey Analytics。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| [!BADGE Alpha]{type=Informative}监视重大变化并预测受众增长 | 使用AI Assistant监控重大变化，并为您的受众和数据集大小提供增长预测。 然后，您可以使用此信息确保受众数据的完整性，并提供前瞻性预测以支持以数据为依据的决策。 有关详细信息，请阅读有关[监控重大更改和预测受众增长](../../ai-assistant/new-features/audience-forecasting.md)的指南。 |
| [!BADGE Alpha]{type=Informative}自然语言估计 | 利用AI Assistant的自然语言估计功能，根据简单的对话问题估计受众规模并预测受众倾向。 有关详细信息，请阅读有关[在AI助手中使用自然语言估计](../../ai-assistant/new-features/natural-language.md)的指南。 |

{style="table-layout:auto"}

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新目标**{#new-updated-destinations}

| 目标 | 描述 |
| --- | --- |
| [Magnite实时流式传输](/help/destinations/catalog/advertising/magnite-streaming.md) | 在Magnite流平台中导出受众以供激活、定位或禁止。 请注意，要将受众正确导出到Magnite，您必须同时使用实时目标和批处理目标。 |
| [菱形流批处理](/help/destinations/catalog/advertising/magnite-batch.md) | 在Magnite流平台中导出受众以供激活、定位或禁止。 请注意，要将受众正确导出到Magnite，您必须同时使用实时目标和批处理目标。 |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| --- | --- |
| [在Edge上实时查找配置文件属性](/help/destinations/ui/activate-edge-profile-lookup.md) | 了解如何使用自定义Personalization目标和Edge NetworkAPI实时查找边缘配置文件属性以交付个性化体验或告知下游应用程序决策规则。 |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## 查询服务 {#query-service}

使用标准SQL和查询服务在Adobe Experience Platform Data Lake中查询数据。 无缝地组合数据集并从查询结果中生成新数据集以支持报告、启用数据科学工作流程或促进将数据摄取到实时客户个人资料中。 例如，您可以将客户交易数据与行为数据合并，以识别针对性营销活动的高价值受众。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 日期Distiller授权API | 管理和强制实施查询服务沙盒基于IP的访问限制，以增强数据安全性并确保遵守组织策略。 请参阅[Data Distiller Authorization API指南](../../query-service/auth-api/overview.md)，以了解其主要特性和功能的详细信息，或参阅[OpenAPI文档](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/)，以了解包括端点详细信息、参数列表、请求/响应示例和测试功能的全面信息。 |

有关[!DNL Query Service]的详细信息，请参阅[[!DNL Query Service] 概述](../../query-service/home.md)。

## 沙盒 {#sandboxes}

Adobe Experience Platform 旨在丰富全球范围内的数字体验应用。企业通常会同时运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署要求，同时确保运营合规性。为了满足这一需求，Experience Platform 提供了可将单个 Platform 实例划分为多个单独的虚拟环境的沙盒，以帮助开发和改进数字体验应用程序。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 使用沙盒工具API共享包 | 使用沙盒工具API使用两个新的API端点[`/handshake`](../../sandboxes/sandbox-tooling-api/packages.md#org-linking)和[`/transfers`](../../sandboxes/sandbox-tooling-api/packages.md#transfer-packages)处理组织之间的包共享，例如请求审批、包可见性和导入包。 |

有关沙盒的更多信息，请阅读[沙盒概述](../../sandboxes/home.md)。

## 文档更新 {#documentation-updates}

### 交互式 Experience Platform API 文档 {#interactive-api-documentation}

[Experience PlatformAPI文档](https://developer.adobe.com/experience-platform-apis/)现在完全交互式，允许您直接在API参考文档页面上验证和浏览API。 您现在可以转到所需的API引用文档页面，创建或获取API身份验证凭据，将它们粘贴到&#x200B;**[!UICONTROL 尝试]**&#x200B;块中，然后执行调用。 全部放在一个页面上。 [阅读有关功能的更多信息](/help/landing/api-authentication.md#get-credentials-functionality)。

### Experience League上的新目录 {#new-table-of-contents-on-experience-league}

Experience League文档页面上的目录已得到改进，为读者提供了更好的体验，包括关键词过滤器（用于发现所需的确切页面）、展开所有页面的功能等。<br> ![新的目录体验，包括关键词筛选器和展开所有页面的功能。](../2024/assets/november/new-toc-experience.gif "新的目录体验，包括关键词筛选器和展开所有页面的能力。"){width="250" align="center" zoomable="yes"}

### 新的AI助手登陆页面 {#new-ai-assistant-landing-page}

使用新的[AI助手产品文档](../../ai-assistant/landing.md)页面作为所有AI助手项目的中心。 请参阅产品文档，获取有关AI助手的视频教程、技术文档、用例以及指向博客帖子的链接。