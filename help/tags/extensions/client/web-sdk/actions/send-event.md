---
title: 发送事件
description: 将数据发送到Adobe Experience Platform Edge Network。
exl-id: 4ac7750e-48ab-4eb6-873d-bb2556dbf788
source-git-commit: caaf5cad7276d6429fbbf35585fd4845de6ff60c
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# 发送事件

**[!UICONTROL Send event]**&#x200B;操作会将有效负载发送到Adobe Experience Platform Edge Network上的数据流。 它是数据收集和个性化的核心功能；几乎所有组织都将此操作用作其Web SDK实施的一部分。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Rules]**，然后选择所需的规则。
1. 在[!UICONTROL Actions]下，选择现有操作或创建操作。
1. 将[!UICONTROL Extension]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，然后将[!UICONTROL Action type]设置为&#x200B;**[!UICONTROL Send event]**。

## 常规字段

![Experience Platform Tags UI图像显示“发送事件”操作类型的实例设置。](../assets/instance-settings.png)

* **[!UICONTROL Instance]**：操作适用的SDK实例。 如果您的实施使用单个SDK实例，则会禁用此下拉菜单。
* **[!UICONTROL Use guided events]**：启用此选项可自动填写或隐藏某些字段以启用特定用例。 在为每种目的设置操作时，此设置有助于减少可用选项的干扰，并遵循Adobe的最佳实践[顶部/底部页面事件](/help/collection/use-cases/personalization/top-bottom-page-events.md)。 启用此复选框会触发显示以下单选按钮：
   * **[!UICONTROL Request personalization]**：获取最新的个性化决策，而不记录Adobe Analytics活动。 最常用的名称是在页面顶部。 选中后，此单选按钮将设置以下字段：
      * [!UICONTROL Type]已锁定到[!UICONTROL Decisioning Proposition Fetch]
      * [!UICONTROL Render visual personalization decisions]已锁定以启用
      * [!UICONTROL Automatically send a display event]已锁定为禁用
   * **[!UICONTROL Collect analytics]**：记录事件而不获取个性化决策。 最常在页面底部调用。 选中后，此单选按钮将设置以下字段：
      * [!UICONTROL Include rendered propositions]已锁定以启用

## 数据字段

![显示“发送事件”操作类型的数据元素设置的Experience Platform Tags UI图像。](../assets/data.png)

* **[!UICONTROL Type]**：事件类型。 您可以从预定义的一组值中进行选择，或定义自己的值。 有关详细信息，请参阅[的`eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype)接受值。 与此字段等效的JavaScript库为[`eventType`](/help/collection/js/commands/sendevent/eventtype.md)。
* **[!UICONTROL XDM]**：要发送到Adobe的XDM有效负载。 您可以在此字段中使用[XDM对象](../data-element-types.md#xdm-object)或[变量](../data-element-types.md#variable)。 如果您的规则填充了多个XDM对象，则可以使用[合并的对象](../../core/overview.md#merged-objects)来组合它们。
* **[!UICONTROL Data]**：要发送到Adobe的数据有效负载。 某些应用程序和服务不需要遵循XDM架构，例如Adobe Analytics或Adobe Target。 对此字段使用[变量](../data-element-types.md#variable)数据元素类型。
* **[!UICONTROL Include rendered propositions]**：启用此复选框可将此事件用作显示事件，包括未选中“自动发送显示事件”时呈现的建议。 `_experience.decisioning` XDM字段将填充有关已渲染个性化的信息。
* **[!UICONTROL Document will unload]**：启用此复选框可确保事件到达服务器，即使用户离开页面也一样。 此设置允许事件访问服务器，但来自Edge Network的响应将被忽略。
* **[!UICONTROL Merge ID]** _（已弃用）_：填充`eventMergeId` XDM字段。

## 个性化字段

![Experience Platform Tags UI图像显示“发送事件”操作类型的Personalization设置。](../assets/personalization-settings.png)

* **[!UICONTROL Scopes]**：要从个性化明确请求的作用域数组。 您可以手动输入范围，也可以提供数据元素。 手动输入范围时，每个字段表示一个范围。 选择&#x200B;**[!UICONTROL Add scope]**&#x200B;以向操作添加更多作用域。
* **[!UICONTROL Surfaces]**：要使用事件进行查询的表面数组。 有关详细信息，请参阅Adobe Journey Optimizer文档中的[创建Web体验](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=zh-Hans)。 手动输入曲面时，每个字段表示一个曲面。 选择&#x200B;**[!UICONTROL Add surface]**&#x200B;可向操作添加更多表面。
* **呈现可视化个性化决策：**&#x200B;一个复选框，启用后可让您在页面上呈现个性化内容。 有关详细信息，请参阅[自动呈现DOM操作](/help/collection/use-cases/personalization/render-auto-pers-content.md)。
* **[!UICONTROL Request default personalization]**：控制是否请求页面范围的范围和默认表面。 默认情况下，在页面加载的第一个`sendEvent`调用期间自动请求它。 与这些单选按钮等效的JavaScript库为[`requestDefaultPersonalization`](/help/collection/js/commands/sendevent/personalization.md)。 您可以从以下选项中进行选择：
   * **[!UICONTROL Automatic]**：默认行为。 仅在尚未请求时请求默认个性化。
   * **[!UICONTROL Enabled]**：显式请求页面范围和默认表面。 这将更新SPA视图缓存。
   * **[!UICONTROL Disabled]**：显式禁止请求页面范围和默认表面。
* **[!UICONTROL Decision context]**：在评估设备上决策的Adobe Journey Optimizer规则集时使用的键值映射。 您可以手动或通过数据元素提供决策上下文。

## Advertising字段

![Experience Platform标记UI显示“发送事件”操作的广告设置](../assets/send-event-advertising.png)

* **[!UICONTROL Request default advertising data]**：确定库何时或是否将广告信息添加到XDM有效负载。 您可以从以下选项中进行选择：
   * **[!UICONTROL Automatic]**：将事件发生时可用的任何广告数据添加到事件有效负载中。
   * **[!UICONTROL Wait]**：延迟发送事件，直到收到广告数据。
   * **[!UICONTROL Disabled]**：不要将广告数据添加到事件有效负载。 如果您的实施不使用Adobe Analytics或Customer Journey Analytics，请选择此选项。

## 数据流配置覆盖

此命令支持数据流配置覆盖，从而使您能够控制哪些应用程序和服务接收此数据。 当在单个命令和标记扩展配置设置中设置数据流配置覆盖时，单个命令优先。 有关详细信息，请参阅[数据流配置覆盖](../configure/configuration-overrides.md)。
