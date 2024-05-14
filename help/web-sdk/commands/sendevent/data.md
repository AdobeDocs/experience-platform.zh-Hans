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

此 `data` 对象允许您将有效负载发送到与XDM架构不匹配的Adobe。 它在非XDM场景下非常有用，例如直接将数据发送到Adobe Analytics、Adobe Target或Adobe Audience Manager。 当数据到达数据流时，您可以使用 [数据准备映射](/help/data-prep/ui/mapping.md) 要将XDM字段分配给 `data` 对象。

>[!IMPORTANT]
>
>此对象中的数据必须至少具有以下操作之一：
>
>* 必须将数据流中的服务配置为从中的给定属性检索数据 `data` 对象。
>* 必须使用数据准备将给定属性映射到XDM字段。
>
>如果给定的属性未映射到XDM字段或未被配置的服务使用，则该数据将永久丢失。

## 使用 `data` 对象通过Web SDK标记扩展 {#tag-extension}

在中提供数据元素 **[!UICONTROL 数据]** 标记规则操作中的字段。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 规则]**，然后选择所需的规则。
1. 下 [!UICONTROL 操作]，选择现有操作或创建操作。
1. 设置 [!UICONTROL 扩展名] 下拉字段至 **[!UICONTROL Adobe Experience Platform Web SDK]**，并设置 [!UICONTROL 操作类型] 到 **[!UICONTROL 发送事件]**.
1. 提供包含中所需对象的数据元素 **[!UICONTROL 数据]** 字段。
1. 单击 **[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 使用 `data` 对象通过Web SDK JavaScript库 {#library}

设置 `data` 对象，作为参数中的JSON对象的一部分 `sendEvent` 命令。 对于计划在数据流中映射的数据，您可以根据需要构建此对象。 对于特定服务使用的数据，请确保对象层次结构与服务期望的层次结构匹配。 您可以同时包含 `data` 对象和 [`xdm`](xdm.md) 同一对象中的 `sendEvent` 命令。

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## 使用 `data` 使用Adobe Analytics的对象 {#analytics}

您可以使用 `data` Adobe Analytics对象将数据发送到没有XDM架构的报表包。 变量配置为使用与相同的语法 [!DNL AppMeasurement] 变量，从而简化对Web SDK的升级过程。 请参阅 [数据对象变量映射到Adobe Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics/implementation/aep-edge/data-var-mapping) 有关更多信息，请参阅Adobe Analytics实施指南。
