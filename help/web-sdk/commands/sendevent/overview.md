---
title: sendEvent
description: 将数据发送到Adobe Experience Platform Edge Network。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# `sendEvent`

此 `sendEvent` 命令是将数据发送到Adobe以检索个性化内容、身份和受众目标的主要方式。 使用 [`xdm`](xdm.md) 对象，用于发送映射到Adobe Experience Platform架构的数据。 使用 [`data`](data.md) 对象以发送非XDM数据。 您可以使用数据流映射器将此对象中的数据与架构字段对齐。

## 使用Web SDK标记扩展发送事件数据

在Adobe Experience Platform数据收集标记界面的规则中，发送事件数据是一项操作。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 规则]**，然后选择所需的规则。
1. 下 [!UICONTROL 操作]，选择现有操作或创建操作。
1. 设置 [!UICONTROL 扩展名] 下拉字段至 **[!UICONTROL Adobe Experience Platform Web SDK]**，并设置 [!UICONTROL 操作类型] 到 **[!UICONTROL 发送事件]**.
1. 设置所需字段，然后单击 **[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 使用Web SDK JavaScript库发送事件数据

运行 `sendEvent` 命令。 确保您致电 [`configure`](../configure/overview.md) 命令之前调用 `sendEvent` 命令。

```js
alloy("sendEvent", {
  "data": dataObject,
  "documentUnloading": true,
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "renderDecisions": true,
  "type": "commerce.purchases",
  "xdm": adobeDataLayer.getState(reference)
});
```

## 响应对象

如果您决定 [处理响应](../command-responses.md) 使用此命令，响应对象中提供了以下属性：

* **`propositions`**：Edge Network返回的一组建议。 自动呈现的建议包含标志 `renderAttempted` 设置为 `true`.
* **`inferences`**：推理对象数组，其中包含有关此用户的机器学习信息。
* **`destinations`**：边缘网络返回的目标对象数组。
