---
title: Personalization用例概述
description: 了解如何使用Adobe Experience Platform Web SDK实施个性化用例，包括用于呈现内容和跟踪显示的模式。
keywords: 个性化；sendEvent；renderDecisions；applyPropositions；decisionScopes；显示事件；闪烁；
exl-id: 6beccbfd-fddb-4e19-8a56-caba276e1643
source-git-commit: caaf5cad7276d6429fbbf35585fd4845de6ff60c
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Personalization用例概述

Adobe Experience Platform Web SDK允许对Web资产使用各种个性化用例。 它支持灵活的体系结构（客户端、服务器端和混合），因此您可以根据站点的需求请求决策和呈现内容。

## 呈现个性化内容

Web SDK可以检索个性化决策（也称为&#x200B;_建议_），并帮助您在页面上呈现这些决策。 渲染是异步的，因此请避免假定应用内容时的特定时间。

选择与您收到的建议项目匹配的模式：

1. **自动呈现DOM操作建议**：当建议包含的`dom-action`项具有Web SDK可自动应用的选择器和操作类型时使用。 请参阅[自动呈现DOM操作建议](render-auto-pers-content.md)。
1. **使用applyPropositions呈现不带选择器的HTML选件**：在接收HTML内容时使用，但必须提供通过元数据应用该选件的位置和方法（选择器+操作类型）。 查看[渲染不带选择器的HTML选件](render-html-offers.md)。
1. **手动呈现建议**：需要完全控制呈现逻辑时使用（例如，从JSON合成UI或应用自定义业务规则）。 请参阅[手动渲染建议](render-manual-propositions.md)。

>[!TIP]
>
>这些模式可以合并。 例如，您可以启用自动DOM操作渲染，同时还可以手动呈现特定决策范围中的内容。

## 常见伴随主题

大多数个性化实施都涉及以下常见主题：

* **防止闪烁**（可选）：在个性化过程中隐藏并显示容器。 请参阅[管理闪烁](manage-flicker.md)。
* **跟踪显示的内容**：记录呈现内容的显示事件。 请参阅[管理显示事件](display-events.md)。
* **页面顶部提取/页面底部量度**：提早请求决策，然后稍后包含测量。 请参阅[配置页面顶部和底部事件](top-bottom-page-events.md)。

## Web SDK示例

除了此文件夹中的文档页面之外，Adobe还维护着一个您可以引用的示例应用程序存储库。 有关其他个性化方案，请参阅GitHub上的[Web SDK示例](https://github.com/adobe/alloy-samples/)，包括：

* 客户端个性化
* 服务器端个性化
* 混合个性化
* 单页应用程序中的Personalization
