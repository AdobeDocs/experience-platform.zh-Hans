---
title: Adobe Experience Platform 发行说明（2024 年 11 月）
description: Adobe Experience Platform 2024 年 11 月发行说明。
exl-id: e3969f8b-70b2-40f8-bb9b-5be6e3d8f722
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 96%

---

# Adobe Experience Platform 发行说明

>[!TIP]
>
>新的 [AI 助手产品文档](../../ai-assistant/landing.md)现已推出。将此页面用作所有与 AI 助手相关资源的中心。

**发行日期：2024 年 11 月 26 日**

Adobe Experience Platform 中现有功能和文档的更新：

- [AI 助手](#ai-assistant)
- [目标](#destinations)
- [查询服务](#query-service)
- [沙盒](#sandboxes)
- [文档更新](#documentation-updates)
   - [交互式 Experience Platform API 文档](#interactive-experience-platform-api-documentation)
   - [Experience League 上的新目录](#new-table-of-contents-on-experience-league)
   - [新的 AI 助手登陆页面](#new-ai-assistant-landing-page)

## AI 助手 {#ai-assistant}

Adobe Experience Platform 中的 AI 助手是一种对话体验，您可以使用它来加速 Adobe 应用程序中的工作流程。您可以使用 AI 助手更好地了解产品知识、解决问题或搜索信息并找到运营洞察。AI 助手支持 Experience Platform、Real-time Customer Data Platform、Adobe Journey Optimizer 和 Customer Journey Analytics。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| [!BADGE Alpha]{type=Informative} 可监控重大变化并预测受众增长 | 使用 AI 助手监控重大变化，并为您的受众和数据集大小提供增长预测。然后，您可以使用这些信息来确保受众数据的完整性，并提供前瞻性预测，以支持基于数据的决策。若要了解更多信息，请阅读[监控重大变化和预测受众增长](../../ai-assistant/new-features/audience-forecasting.md)的指南。 |
| [!BADGE Alpha]{type=Informative} 自然语言评估 | 使用 AI 助手的自然语言评估功能根据简单的对话问题估计受众规模并预测受众倾向。如需了解更多信息，请阅读[使用 AI 助手进行自然语言评估](../../ai-assistant/new-features/natural-language.md)的指南。 |

{style="table-layout:auto"}

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新目标**{#new-updated-destinations}

| 目标 | 描述 |
| --- | --- |
| [Magnite Streaming 实时处理](/help/destinations/catalog/advertising/magnite-streaming.md) | 导出受众，以便在 Magnite Streaming 平台中进行激活、定位或抑制。请注意，为了确保受众能正确导出至 Magnite，您必须同时使用实时和批量目标。 |
| [Magnite Streaming 批量处理](/help/destinations/catalog/advertising/magnite-batch.md) | 导出受众，以便在 Magnite Streaming 平台中进行激活、定位或抑制。请注意，为了确保受众能正确导出至 Magnite，您必须同时使用实时和批量目标。 |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| --- | --- |
| [在边缘实时查找轮廓属性](/help/destinations/ui/activate-edge-profile-lookup.md) | 了解如何通过使用自定义个性化目标和 Edge Network API 实时查找边缘轮廓属性，以提供个性化体验，或通过下游应用程序通知决策规则。 |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## 查询服务 {#query-service}

使用查询服务，通过标准 SQL 在 Adobe Experience Platform 数据湖中查询数据。无缝组合数据集，并从查询结果中生成新数据集，以增强报告功能、启用数据科学工作流程，或促进向实时客户轮廓引入数据。例如，您可以将客户交易数据与行为数据合并，为有针对性的营销活动识别高价值受众。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 数据蒸馏器授权 API | 管理和实施基于 IP 的查询服务沙盒访问限制，以增强数据安全性，并确保遵守组织政策。请参阅[数据蒸馏器授权 API 指南](../../query-service/auth-api/overview.md)，了解有关其主要特性和功能的更多信息，或参阅 [OpenAPI 文档](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/)，获取包括端点详细信息、参数列表、请求/响应示例和测试功能在内的全面信息。 |

有关 [!DNL Query Service] 的详细信息，请查看 [[!DNL Query Service] 概述](../../query-service/home.md)。

## 沙盒 {#sandboxes}

Adobe Experience Platform 旨在丰富全球范围内的数字体验应用。企业通常会同时运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署要求，同时确保运营合规性。为了满足此需求，Experience Platform提供了可将单个Experience Platform实例划分为多个单独的虚拟环境的沙盒，以帮助开发和改进数字体验应用程序。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 沙盒工具 API 中的包共享 | 使用两个新的 API 端点 [`/handshake`](../../sandboxes/sandbox-tooling-api/packages.md#org-linking) 和 [`/transfers`](../../sandboxes/sandbox-tooling-api/packages.md#transfer-packages) 来处理跨组织包共享，例如请求审批、包可见性和导入包（使用沙盒工具 API）。 |

有关沙盒的更多信息，请阅读[沙盒概述](../../sandboxes/home.md)。

## 文档更新 {#documentation-updates}

### 交互式 Experience Platform API 文档 {#interactive-api-documentation}

[Experience Platform API 文档](https://developer.adobe.com/experience-platform-apis/)现已完全实现交互，允许您直接在 API 参考文档页面上进行身份验证和探索 API。您现在可以转到所需的 API 参考文档页面，创建或获取您的 API 身份验证凭据，将其粘贴到 **[!UICONTROL 尝试]**&#x200B;块中，然后执行调用。所有内容都在一个页面上。[参阅更多](/help/landing/api-authentication.md#get-credentials-functionality)关于该功能的信息。

### Experience League 上的新目录 {#new-table-of-contents-on-experience-league}

Experience League 文档页面上的目录已经得到改进，以为读者提供更好的体验，其中包括关键词过滤器，以便您轻松找到所需的页面，并且提供了展开所有页面的功能等。 <br> ![新的目录体验包括关键词过滤器和扩展所有页面的能力。](../2024/assets/november/new-toc-experience.gif "新的目录体验包括关键词过滤器和扩展所有页面的能力。"){width="250" align="center" zoomable="yes"}

### 新的 AI 助手登陆页面 {#new-ai-assistant-landing-page}

使用新的 [AI 助手产品文档](../../ai-assistant/landing.md)页面作为所有 AI 助手内容的中心。请参阅产品文档，获取有关 AI 助手的视频教程、技术文档、用例和博客文章链接。
