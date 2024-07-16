---
title: Adobe Experience Platform Web SDK扩展中的操作类型
description: 了解Adobe Experience Platform Web SDK标记扩展提供的各种操作类型。
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: fb9f7757d77b221c733bbed5124fa576a6b02ed2
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 1%

---


# 操作类型

配置[Adobe Experience Platform Web SDK标记扩展](web-sdk-extension-configuration.md)后，必须配置操作类型。

本页介绍[Adobe Experience Platform Web SDK标记扩展](web-sdk-extension-configuration.md)支持的操作类型。


## 应用响应 {#apply-response}

当您要根据Edge Network的响应执行各种操作时，请使用&#x200B;**[!UICONTROL 应用响应]**&#x200B;操作类型。 此操作类型通常用于混合部署，其中服务器对Edge Network进行初始调用，然后此操作类型从该调用中获取响应并在浏览器中初始化Web SDK。

使用此操作类型可能会缩短混合个性化用例的客户端加载时间。

![显示“应用响应”操作类型的Experience Platform用户界面图像。](assets/apply-response.png)

此操作类型支持以下配置选项：

* **[!UICONTROL 实例]**：选择您正在使用的Web SDK实例。
* **[!UICONTROL 响应标头]**：选择数据元素，该数据元素将返回包含从Edge Network服务器调用返回的标头键和值的对象。
* **[!UICONTROL 响应正文]**：选择数据元素，该数据元素将返回包含Edge Network响应所提供的JSON有效负载的对象。
* **[!UICONTROL 呈现可视化个性化决策]**：启用此选项可自动呈现Edge Network提供的个性化内容并预隐藏内容以防止闪烁。

## 发送事件 {#send-event}

向Adobe[!DNL Experience Platform]发送一个事件，以便Adobe Experience Platform可以收集您发送的数据并对该信息执行相应的操作。 选择一个实例（如果有多个实例）。 您要发送的任何数据均可通过&#x200B;**[!UICONTROL XDM数据]**&#x200B;字段发送。 使用符合XDM架构的JSON对象。 此对象可以在您的页面上创建，也可以通过&#x200B;**[!UICONTROL 自定义代码]** **[!UICONTROL 数据元素]**&#x200B;创建。

根据您的实施， Send Event操作类型中还有一些其他字段也可能很有用。 请注意，这些字段都是可选的。

* **类型：**&#x200B;此字段允许您指定将记录在XDM架构中的事件类型。 有关详细信息，请参阅`sendEvent`命令中的[`type`](/help/web-sdk/commands/sendevent/type.md)。
* **数据：**&#x200B;使用此字段可以发送与XDM架构不匹配的数据。 如果您尝试更新Adobe Target配置文件或发送Target Recommendations属性，则此字段非常有用。 有关详细信息，请参阅`sendEvent`命令中的[`data`](/help/web-sdk/commands/sendevent/data.md)。<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
* **数据集ID：**&#x200B;如果您需要将数据发送到您在数据流中指定的数据集以外的其他数据集，可以在此处指定该数据集ID。
* **文档将卸载：**&#x200B;如果您希望确保事件到达服务器，即使用户离开页面也一样，请选中&#x200B;**[!UICONTROL 文档将卸载]**&#x200B;复选框。 这允许事件访问服务器，但响应将被忽略。
* **呈现可视化个性化决策：**&#x200B;如果要在页面上呈现个性化内容，请选中&#x200B;**[!UICONTROL 呈现可视化个性化决策]**&#x200B;复选框。 如有必要，您还可以指定决策范围和/或曲面。 有关呈现个性化内容的更多信息，请参阅[个性化文档](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content)。

## 设置同意 {#set-consent}

收到用户的同意后，必须使用“设置同意”操作类型将此同意告知Adobe Experience Platform Web SDK。 目前，支持两种类型的标准：“Adobe”和“IAB TCF”。请参阅[支持客户同意首选项](../../../../web-sdk/commands/setconsent.md)。 使用Adobe版本2.0时，仅支持数据元素值。 您将需要创建一个解析为同意对象的数据元素。

在此操作中，还会向您提供一个可选字段，用于包含标识映射，以便在收到同意后可以同步标识。 将同意配置为“Pending”或“Out”时，同步很有用，因为同意调用可能是第一个要触发的调用。

## 更新变量 {#update-variable}

使用此操作作为事件结果来修改XDM对象。 此操作旨在构建一个以后可以从&#x200B;**[!UICONTROL 发送事件]**&#x200B;操作引用的对象，以记录事件XDM对象。

要使用此操作类型，您必须定义一个[变量](data-element-types.md#variable)数据元素。 选择要修改的变量数据元素后，将显示一个编辑器，该编辑器类似于[XDM对象](data-element-types.md#xdm-object)数据元素的编辑器。

![](assets/update-variable.png)

用于编辑器的XDM架构是对[!UICONTROL 变量]数据元素选择的架构。 您可以设置对象的一个或多个属性，方法是单击左侧的树中的其中一个属性，然后修改右侧的值。例如，在下面的屏幕快照中，productedBy属性将设置为数据元素“Producted by data element”。

![](assets/update-variable-set-property.png)

更新变量操作中的编辑器与XDM对象数据元素中的编辑器之间存在一些差异。 首先，更新变量操作具有一个标记为“xdm”的根级别项。 如果单击此项目，则可以指定要用于设置整个对象的数据元素。 其次，更新变量操作包含复选框，用于清除xdm对象中的数据。 单击左侧的其中一个属性，然后选中右侧的复选框以清除值。 这将在设置变量上的任何值之前清除当前值。

## 发送媒体事件 {#send-media-event}

向Adobe Experience Platform和/或Adobe Analytics发送媒体事件。 当您跟踪网站上的媒体事件时，此操作很有用。 选择一个实例（如果有多个实例）。 该操作需要一个`playerId`，它表示跟踪的媒体会话的唯一标识符。 启动媒体会话时，它还需要&#x200B;**[!UICONTROL 体验质量]**&#x200B;和`playhead`数据元素。

![显示发送媒体事件屏幕的平台UI图像。](assets/send-media-event.png)

**[!UICONTROL 发送媒体事件]**&#x200B;操作类型支持以下属性：

* **[!UICONTROL 实例]**：正在使用的Web SDK实例。
* **[!UICONTROL 媒体事件类型]**：要跟踪的媒体事件的类型。
* **[!UICONTROL 播放器ID]**：媒体会话唯一标识符。
* **[!UICONTROL 播放头]**：媒体播放的当前位置（以秒为单位）。
* **[!UICONTROL 媒体会话详细信息]**：发送媒体开始事件时，应指定所需的媒体会话详细信息。
* **[!UICONTROL 章节详细信息]**：在此部分中，您可以在发送章节开始媒体事件时指定章节详细信息。
* **[!UICONTROL Advertising详细信息]**：发送`AdBreakStart`事件时，必须指定所需的广告详细信息。
* **[!UICONTROL Advertising pod详细信息]**：发送`AdStart`事件时有关广告面板的详细信息。
* **[!UICONTROL 错误详细信息]**：有关正在跟踪的播放错误的详细信息。
* **[!UICONTROL 状态更新详细信息]**：正在更新的播放器状态。
* **[!UICONTROL 自定义元数据]**：有关正在跟踪的媒体事件的自定义元数据。
* **[!UICONTROL 体验质量]**：正在跟踪的体验数据的媒体质量。

## 获取Media Analytics跟踪器 {#get-media-analytics-tracker}

此操作用于获取旧版Media Analytics API。 配置操作并提供对象名称时，旧版Media Analytics API将导出到该窗口对象。 如果未提供，它将像当前媒体JS库那样导出到`window.Media`。

![Platform UI图像显示“获取Media Analytics跟踪器”操作类型。](assets/get-media-analytics-tracker.png)

## 带标识的重定向 {#redirect-with-identity}

使用此操作类型可将当前页面的标识共享到其他域。 此操作设计用于&#x200B;**[!UICONTROL click]**&#x200B;事件类型和值比较条件。 有关如何使用此操作类型的详细信息，请参阅[使用Web SDK扩展将标识附加到URL](../../../../web-sdk/commands/appendidentitytourl.md#extension)。

## 后续步骤 {#next-steps}

阅读本文后，您应该对如何配置操作有了更好的了解。 接下来，阅读如何[配置您的数据元素类型](data-element-types.md)。
