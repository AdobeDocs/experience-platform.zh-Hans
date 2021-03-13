---
title: Adobe Experience Platform Web SDK扩展中的操作类型
description: 了解Adobe Experience Platform Launch中Adobe Experience Platform Web SDK扩展提供的不同操作类型。
solution: Experience Platform
feature: Web SDK
translation-type: tm+mt
source-git-commit: 9ce6dd5a290b55da04f4ae185cab96c120777775
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 4%

---


# 操作类型

为[Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html)配置[Adobe Experience Platform Web SDK扩展](web-sdk-extension.md)后，请配置您的操作类型。

本页介绍了可用的操作类型。

## 发送事件

向Adobe [!DNL Experience Platform]发送事件，以便Adobe Experience Platform可以收集您发送的数据并对该信息执行操作。 选择一个实例（如果您有多个实例）。 您要发送的任何数据都可以在&#x200B;**[!UICONTROL XDM数据]**&#x200B;字段中发送。 使用符合XDM模式结构的JSON对象。 可以在您的页面上创建此对象，也可以通过&#x200B;**[!UICONTROL 自定义代码]** **[!UICONTROL 数据元素]**&#x200B;创建此对象。

“发送事件”操作类型中还有一些其他字段，根据您的实施情况，这些字段可能也很有用。 请注意，这些字段都是可选的。

- **类型：** 此字段允许您指定将在XDM模式中录制的事件类型。有关默认事件类型的详细信息，请参阅[文档](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api)。
- **合并ID:** 如果要为事件指 [定](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/merging-event-data.html?lang=en#fundamentals) 合并ID，则可以在此字段中执行此操作。请注意，下游解决方案目前无法合并您的事件数据。
- **数据集ID:** 如果您需要将数据发送到您在边缘配置中指定的数据集以外的数据集，则可以在此处指定该数据集ID。
- **文档将卸载：** 如果要确保即使用户从页面导航到其他位置，事件也能到达服务器，请选中“文档将 **[!UICONTROL 卸载”]** 复选框。这允许事件访问服务器，但忽略响应。
- **渲染可视个性化决** 策：如果要在页面上渲染个性化内容，请选中“渲染可视 **[!UICONTROL 个性化决]** 策”复选框。如有必要，您还可以指定决策范围。 有关呈现个性化内容的更多信息，请参阅[个性化文档](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content)。

## 设置同意

在您收到用户的同意后，必须使用“设置同意”操作类型将此同意通知Adobe Experience Platform Web SDK。 目前，支持两种类型的标准：“Adobe”和“IAB TCF”。请参阅[支持客户同意首选项](../consent/supporting-consent.md)。 使用Adobe 2.0版时，仅支持数据元素值。 您需要创建一个解析到同意对象的数据元素。

在此操作中，您还会获得一个可选字段，用于包含身份映射，以便在收到同意后可以同步身份。 同步在同意配置为“待定”或“出现”时很有用，因为同意呼叫可能是第一个要触发的呼叫。

## 重置事件合并 ID

如果要在页面上重置事件合并ID，则可以通过此操作重置。 要重置您的ID，请选择要重置的合并ID，并根据需要触发操作。

## 下一步

设置操作后，[配置数据元素类型](data-element-types.md)。
