---
title: Adobe Experience Platform Web SDK扩展中的操作类型
description: 了解Adobe Experience Platform Web SDK标记扩展提供的不同操作类型。
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 2%

---


# 操作类型

配置 [Adobe Experience Platform Web SDK标记扩展](web-sdk-extension-configuration.md)，则必须配置操作类型。

本页介绍了 [Adobe Experience Platform Web SDK标记扩展](web-sdk-extension-configuration.md).

## 发送事件 {#send-event}

向Adobe发送事件 [!DNL Experience Platform] 以便Adobe Experience Platform能够收集您发送的数据并对该信息采取行动。 选择一个实例（如果您有多个实例）。 您要发送的任何数据均可在 **[!UICONTROL XDM数据]** 字段。 使用符合XDM架构的JSON对象。 此对象可以在页面上创建，也可以通过 **[!UICONTROL 自定义代码]** **[!UICONTROL 数据元素]**.

“发送事件”操作类型中还有其他一些字段，根据您的实施，这些字段也会很有用。 请注意，这些字段都是可选的。

- **类型：** 利用此字段，可指定将在XDM架构中记录的事件类型。 请参阅 [文档](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) 以了解有关默认事件类型的详细信息。
- **数据：** 使用此字段可发送与XDM架构不匹配的数据。 如果您尝试更新Adobe Target配置文件或发送Target Recommendations属性，则此字段非常有用。 有关示例，请参阅 [文档](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=zh-Hans).<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **数据集ID:** 如果您需要将数据发送到数据流中指定的数据集以外的数据集，则可以在此处指定该数据集ID。
- **文档将卸载：** 如果要确保即使用户离开页面，事件也会到达服务器，请检查 **[!UICONTROL 文档将卸载]** 复选框。 这允许事件到达服务器，但会忽略响应。
- **呈现可视化个性化决策：** 如果要在页面上呈现个性化内容，请检查 **[!UICONTROL 呈现可视化个性化决策]** 复选框。 您还可以根据需要指定决策范围和/或曲面。 请参阅 [个性化文档](../personalization/rendering-personalization-content.md#automatically-rendering-content) 以了解有关呈现个性化内容的更多信息。

## 设置同意 {#set-consent}

在您收到用户的同意后，必须使用“设置同意”操作类型将此同意传达到Adobe Experience Platform Web SDK。 目前，支持两种类型的标准：“Adobe”和“IAB TCF”。请参阅 [支持客户同意首选项](../consent/supporting-consent.md). 使用Adobe版本2.0时，仅支持数据元素值。 您需要创建一个可解析为同意对象的数据元素。

在此操作中，您还会获得一个可选字段，用于包含身份映射，以便在收到同意后可以同步身份。 同步在同意配置为“待定”或“输出”时很有用，因为同意调用可能是首次调用触发时。

## 重置事件合并ID {#reset-event-merge-id}

如果要在页面上重置事件合并ID，可以通过此操作来重置。 要重置您的ID，请选择要重置的合并ID，然后根据需要触发操作。

## （测试版）更新变量 {#update-variable}

>[!IMPORTANT]
>
>这目前是测试版功能，可能会发生更改。 将来版本可能包含中断更改。

使用此操作可修改事件导致的XDM对象。 此操作旨在构建一个对象，该对象稍后可从 **[!UICONTROL 发送事件]** 操作，以记录事件XDM对象。

要使用此操作类型，您必须定义 [变量](data-element-types.md#variable) 数据元素。 选择要修改的变量数据元素后，会显示一个编辑器，它类似于 [XDM对象](data-element-types.md#xdm-object) 数据元素。

![](./assets/update-variable.png)

用于编辑器的XDM架构是在 [!UICONTROL 变量] 数据元素。 您可以通过单击左侧树中的一个属性，然后修改右侧的值来设置对象的一个或多个属性。例如，在下面的屏幕截图中， prodectedBy属性将设置为数据元素“由数据元素生成”。

![](./assets/update-variable-set-property.png)

与XDM对象数据元素中的编辑器相比，更新变量操作中的编辑器存在一些差异。 首先，更新变量操作的根级别项目标记为“xdm”。 如果单击此项目，则可以指定用于设置整个对象的数据元素。 其次，更新变量操作包含用于清除xdm对象中数据的复选框。 单击左侧的其中一个属性，然后选中右侧的复选框以清除值。 这将在变量上设置任何值之前清除当前值。

## 后续步骤 {#next-steps}

阅读本文后，您应该对如何配置操作有了更好的了解。 接下来，阅读有关如何 [配置数据元素类型](data-element-types.md).
