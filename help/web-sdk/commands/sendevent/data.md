---
title: 数据
description: 了解如何通过数据对象将非XDM数据发送到Adobe。
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# `data`

`data`对象允许您向与XDM架构不匹配的Adobe发送有效负载。 它在非XDM场景下非常有用，例如直接将数据发送到Adobe Analytics、Adobe Target或Adobe Audience Manager。 当数据到达数据流时，您可以使用[数据准备映射](/help/data-prep/ui/mapping.md)将XDM字段分配给`data`对象中的每个字段。

>[!IMPORTANT]
>
>此对象中的数据必须至少具有以下操作之一：
>
>* 数据流中的服务必须配置为从`data`对象中的给定属性检索数据。
>* 必须使用数据准备将给定属性映射到XDM字段。
>
>如果给定的属性未映射到XDM字段或未被配置的服务使用，则该数据将永久丢失。

## 通过Web SDK标记扩展使用`data`对象 {#tag-extension}

在标记规则操作的&#x200B;**[!UICONTROL Data]**&#x200B;字段中提供数据元素。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 规则]**，然后选择所需的规则。
1. 在[!UICONTROL 操作]下，选择现有操作或创建操作。
1. 将[!UICONTROL 扩展]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，并将[!UICONTROL 操作类型]设置为&#x200B;**[!UICONTROL 发送事件]**。
1. 在&#x200B;**[!UICONTROL 数据]**&#x200B;字段中提供包含所需对象的数据元素。
1. 单击&#x200B;**[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 通过Web SDK JavaScript库使用`data`对象 {#library}

在`sendEvent`命令的参数中将`data`对象设置为JSON对象的一部分。 对于计划在数据流中映射的数据，您可以根据需要构建此对象。 对于特定服务使用的数据，请确保对象层次结构与服务期望的层次结构匹配。 您可以在同一`sendEvent`命令中同时包含`data`对象和[`xdm`](xdm.md)对象。

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## 在Adobe Analytics中使用`data`对象 {#analytics}

您可以将`data`对象与Adobe Analytics结合使用，以将数据发送到没有XDM架构的报表包。 变量配置为使用与[!DNL AppMeasurement]变量相同的语法，从而简化了Web SDK的升级过程。 有关详细信息，请参阅Adobe Analytics实施指南中的[映射到Adobe Analytics的数据对象变量](https://experienceleague.adobe.com/zh-hans/docs/analytics/implementation/aep-edge/data-var-mapping)。
