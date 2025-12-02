---
title: 应用建议
description: 在单页应用程序中渲染建议而不增加量度。
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# 应用建议

**[!UICONTROL Apply propositions]**&#x200B;操作类型允许您在不增加量度的情况下在单页应用程序中呈现建议。 在使用单页应用程序时，如果页面的一部分被重新渲染，可能会覆盖已应用于页面的任何个性化设置，则此操作类型会很有用。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Rules]**，然后选择所需的规则。
1. 在[!UICONTROL Actions]下，选择现有操作或创建操作。
1. 将[!UICONTROL Extension]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，然后将[!UICONTROL Action type]设置为&#x200B;**[!UICONTROL Apply propositions]**。

![显示“应用建议”操作类型的Experience Platform Tags UI。](../assets/apply-propositions.png)

## 用例

您可以将此操作类型用于各种用例，例如：

1. **呈现mbox HTML选件**。 从&#x200B;**[!UICONTROL Send event]**&#x200B;操作通过范围或表面明确请求的主张不会自动呈现。 您可以使用&#x200B;**[!UICONTROL Apply propositions]**&#x200B;操作类型通过指定建议元数据来告知Web SDK在何处渲染它们。
2. **在单页应用程序上渲染视图的选件**。 在呈现视图更改事件时，如果分析数据尚未准备就绪，则可以使用&#x200B;**[!UICONTROL Apply propositions]**&#x200B;操作在页面顶部呈现视图建议。 有关更多详细信息，请参阅[页面事件的顶部和底部（第二个页面视图 — 选项2）](/help/collection/use-cases/personalization/top-bottom-page-events.md)。 要使用此项，请在表单中输入&#x200B;**[!UICONTROL View name]**。
3. **重新呈现建议**。 当网站使用React等框架重新呈现内容时，您可能需要重新应用个性化。 在这种情况下，您可以使用&#x200B;**[!UICONTROL Apply propositions]**&#x200B;操作类型来执行此操作。

此操作类型不会为渲染的建议发送显示事件。 它跟踪渲染的建议，以便将其包含在后续&#x200B;**[!UICONTROL Send event]**&#x200B;调用中。

## 可用字段

此操作类型支持以下字段：

* **[!UICONTROL Instance]**：操作适用的SDK实例。 如果您的实施使用单个SDK实例，则会禁用此下拉菜单。
* **[!UICONTROL Propositions]**：要重新渲染的建议对象的数组。
* **[!UICONTROL View name]**：要呈现的视图的名称。
* **[!UICONTROL Proposition metadata]**：确定如何应用HTML选件的对象。 您可以通过表单或数据元素提供此信息。 它包含以下属性：
   * **[!UICONTROL Scope]**
   * **[!UICONTROL Selector]**
   * **[!UICONTROL Action type]**
