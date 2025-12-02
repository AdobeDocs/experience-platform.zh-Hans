---
title: 数据
description: 了解如何通过数据对象将非XDM数据发送到Adobe。
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# `data`

`data`对象允许您向Adobe发送与XDM架构不匹配的有效负载。 它在非XDM场景下非常有用，例如直接将数据发送到Adobe Analytics、Adobe Target或Adobe Audience Manager。 当数据到达数据流时，您可以使用[数据准备映射](/help/data-prep/ui/mapping.md)将XDM字段分配给`data`对象中的每个字段。 如果Adobe已将某个产品配置为检测`data`对象中的字段，则可以将该数据按原样发送到数据流。

>[!IMPORTANT]
>
>此对象中的数据必须至少具有以下操作之一：
>
>* 数据流中的服务必须配置为从`data`对象中的给定属性检索数据。
>* 必须使用数据准备将给定属性映射到XDM字段。
>
>如果给定的属性未映射到XDM字段或未被配置的服务使用，则该数据将永久丢失。

在`data`命令的参数中将`sendEvent`对象设置为JSON对象的一部分。 对于计划在数据流中映射的数据，您可以根据需要构建此对象。 对于特定服务使用的数据，请确保对象层次结构与服务期望的层次结构匹配。 您可以在同一`data`命令中同时包含[`xdm`](xdm.md)对象和`sendEvent`对象。

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## 在Adobe Analytics中使用`data`对象 {#analytics}

您可以将`data`对象与Adobe Analytics结合使用，以将数据发送到没有XDM架构的报表包。 将变量配置为使用与AppMeasurement变量相同的语法，从而简化升级到Web SDK的过程。 有关详细信息，请参阅Adobe Analytics实施指南中的[映射到Adobe Analytics的数据对象变量](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping)。

## 通过Web SDK标记扩展使用`data`对象

使用Web SDK标记扩展时，`data`对象可用作[变量数据元素](/help/tags/extensions/client/web-sdk/data-element-types.md#variable)。
