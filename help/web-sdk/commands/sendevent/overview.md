---
title: sendEvent
description: 将数据发送到Adobe Experience PlatformEdge Network。
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: 9ea7b678f5cfa19c7fd1e3ba6633cdeed4084b18
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# `sendEvent`

`sendEvent`命令是将数据发送到Adobe、检索个性化内容、身份和受众目标的主要方式。 使用[`xdm`](xdm.md)对象发送映射到Adobe Experience Platform架构的数据。 使用[`data`](data.md)对象发送非XDM数据。 您可以使用数据流映射器将此对象中的数据与架构字段对齐。

## 使用Web SDK标记扩展发送事件数据

在Adobe Experience Platform数据收集标记界面的规则中，发送事件数据是一项操作。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 规则]**，然后选择所需的规则。
1. 在[!UICONTROL 操作]下，选择现有操作或创建操作。
1. 将[!UICONTROL 扩展]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，并将[!UICONTROL 操作类型]设置为&#x200B;**[!UICONTROL 发送事件]**。
1. 设置所需字段，单击&#x200B;**[!UICONTROL 保留更改]**，然后运行发布工作流。

## 使用Web SDK JavaScript库发送事件数据

调用Web SDK的配置实例时运行`sendEvent`命令。 确保在调用`sendEvent`命令之前调用[`configure`](../configure/overview.md)命令。

```js
alloy("sendEvent", {
  "data": dataObject,
  "documentUnloading": false,
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "renderDecisions": true,
  "type": "commerce.purchases",
  "xdm": adobeDataLayer.getState(reference)
});
```

## 响应对象

如果您决定使用此命令[处理响应](../command-responses.md)，则响应对象中提供了以下属性：

* **`propositions`**：Edge Network返回的建议数组。 自动呈现的建议包括设置为`true`的标志`renderAttempted`。
* **`inferences`**：推理对象的数组，其中包含有关该用户的机器学习信息。
* **`destinations`**：Edge Network返回的目标对象数组。
