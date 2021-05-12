---
title: Adobe Experience Platform Web SDK扩展中的操作类型
description: 了解Adobe Experience Platform Launch中Adobe Experience Platform Web SDK扩展提供的不同操作类型。
solution: Experience Platform
feature: Web SDK
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 7e87f5b29d388b34681217e392c3f1ae8f2b67ee
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 8%

---

# 操作类型

为[Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html)配置[Adobe Experience Platform Web SDK扩展](web-sdk-extension.md)后，请配置您的操作类型。

本页介绍了可用的操作类型。

## 发送事件

向Adobe [!DNL Experience Platform]发送事件，以便Adobe Experience Platform可以收集您发送的数据并对该信息执行操作。 选择一个实例（如果您有多个实例）。 您要发送的任何数据均可通过 **[!UICONTROL XDM Data]** 字段发送。使用符合XDM模式结构的JSON对象。 此对象可以在页面上创建，也可以通过 **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]** 创建。

“发送事件”操作类型中还有一些其他字段，根据您的实施情况，这些字段可能也很有用。 请注意，这些字段都是可选的。

- **类型：** 此字段允许您指定将在XDM模式中录制的事件类型。有关默认事件类型的详细信息，请参阅[文档](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api)。
- **合并ID:** 如果要为事件指 [定](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/merging-event-data.html?lang=en#fundamentals) 合并ID，则可以在此字段中执行此操作。请注意，下游解决方案目前无法合并您的事件数据。
- **数据集ID:** 如果您需要将数据发送到数据流中指定的数据集以外的数据集，则可以在此处指定该数据集ID。
- **文档将卸载：** 如果要确保即使用户从页面导航到其他位置，事件也能到达服务器，请选中此复 **[!UICONTROL Document will unload]** 选框。这允许事件访问服务器，但忽略响应。
- **呈现可视的个性化** 决策：如果要在页面上呈现个性化内容，请选中此复 **[!UICONTROL Render visual personalization decisions]** 选框。如有必要，您还可以指定决策范围。 有关呈现个性化内容的更多信息，请参阅[个性化文档](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content)。

## 设置同意

在您收到用户的同意后，必须使用“设置同意”操作类型将此同意通知Adobe Experience Platform Web SDK。 目前，支持两种类型的标准：“Adobe”和“IAB TCF”。请参阅[支持客户同意首选项](../consent/supporting-consent.md)。 使用Adobe 2.0版时，仅支持数据元素值。 您需要创建一个解析到同意对象的数据元素。

在此操作中，您还会获得一个可选字段，用于包含身份映射，以便在收到同意后可以同步身份。 同步在同意配置为“待定”或“出现”时很有用，因为同意呼叫可能是第一个要触发的呼叫。

## 重置事件合并 ID

如果要在页面上重置事件合并ID，则可以通过此操作重置。 要重置您的ID，请选择要重置的合并ID，并根据需要触发操作。

## 下一步

设置操作后，[配置数据元素类型](data-element-types.md)。
