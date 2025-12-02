---
title: sendEvent
description: 将数据发送到Adobe Experience Platform Edge Network。
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# `sendEvent`

`sendEvent`命令是将数据发送到Adobe的主要方式。 其响应对象是检索个性化内容、身份和受众目标的主要方式。 使用[`xdm`](xdm.md)对象发送映射到Adobe Experience Platform架构的数据。 使用[`data`](data.md)对象发送非XDM数据。 将数据发送到Adobe时的有效负载的最大限制为64 KB。

调用Web SDK的配置实例时运行`sendEvent`命令。 确保在调用[`configure`](../configure/overview.md)命令之前调用`sendEvent`命令。

```js
alloy("sendEvent", {
  data: dataObject,
  documentUnloading: false,
  edgeConfigOverrides: { datastreamId: "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  personalization: { decisionScopes: ["hero-banner"]},
  renderDecisions: true,
  type: "commerce.purchases",
  xdm: adobeDataLayer.getState(reference)
});
```

## 响应对象

如果您决定使用此命令[处理响应](../command-responses.md)，则响应对象中提供了以下属性：

* **`propositions`**： Edge Network返回的建议数组。 自动呈现的建议包括设置为`renderAttempted`的标志`true`。
* **`inferences`**：推理对象的数组，其中包含有关该用户的机器学习信息。
* **`destinations`**： Edge Network返回的目标对象数组。

## 使用Web SDK标记扩展发送事件

此命令的Web SDK标记扩展等效项是[**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields)操作。
