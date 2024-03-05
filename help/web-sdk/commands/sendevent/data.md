---
title: 数据
description: 了解如何将非XDM数据发送到Adobe。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# 数据

此 `data` 属性允许您将数据发送到与XDM架构不匹配的Adobe。 它在非XDM场景下很有用，例如更新 [Adobe Target配置文件](/help/web-sdk/personalization/adobe-target/target-overview.md). 当数据到达Adobe时，您可以使用数据流映射工具将XDM字段分配给中的每个字段。 `data` 属性。

>[!IMPORTANT]
>
>此属性中的数据必须至少具有以下操作之一：
>
>* 必须将数据流中的服务配置为从中的特定属性检索数据 `data` 对象
>* 每个属性都必须映射到XDM字段
>
>如果给定字段未映射到XDM字段或未由配置的服务使用，则该数据将永久丢失。

## 通过Web SDK标记扩展使用data属性

在中提供数据元素 **[!UICONTROL 数据]** 标记规则操作中的字段。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 规则]**，然后选择所需的规则。
1. 下 [!UICONTROL 操作]，选择现有操作或创建操作。
1. 设置 [!UICONTROL 扩展名] 下拉字段至 **[!UICONTROL Adobe Experience Platform Web SDK]**，并设置 [!UICONTROL 操作类型] 到 **[!UICONTROL 发送事件]**.
1. 提供包含中所需对象的数据元素 **[!UICONTROL 数据]** 字段。
1. 单击 **[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 使用Web SDK JavaScript库的data属性

设置 `data` 属性作为JSON对象的一部分，在 `sendEvent` 命令。 对于计划在数据流中映射的数据，您可以根据需要构建此属性。 对于特定服务使用的数据，请确保对象层次结构与服务期望的层次结构匹配。 您可以同时包含 `data` 对象和 [`xdm`](xdm.md) 同一对象中的 `sendEvent` 命令。

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```
