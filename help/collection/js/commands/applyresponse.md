---
title: applyResponse
description: 使用来自Edge Network的响应来初始化Web SDK。
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# `applyResponse`

`applyResponse`命令允许您根据Edge Network的响应执行各种操作。 它通常用于混合部署，其中服务器会对Edge Network进行初始调用。 此命令从该调用中获取响应并在浏览器中初始化Web SDK。

调用Web SDK的配置实例时运行`applyResponse`命令。 包含配置选项的对象支持以下字段：

* **`renderDecisions`**：一个布尔值，强制Web SDK呈现任何符合自动呈现条件的个性化内容。 与[`renderDecisions`](sendevent/renderdecisions.md)命令中的[`sendEvent`](sendevent/overview.md)相同。
* **`responseHeaders`**：字符串标头名称到字符串标头值的映射。
* **`responseBody`**：必需。 来自对Edge Network的服务器调用的JSON响应主体。
* **`personalization.sendDisplayEvent`**： [`personalization.sendDisplayEvent`](sendevent/personalization.md)命令中与`sendEvent`运行方式相同的布尔值。

```js
alloy("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## 响应对象

如果您决定使用此命令[处理响应](command-responses.md)，则响应对象中提供了以下属性：

* **`propositions`**： Edge Network返回的建议数组。 自动呈现的建议包括设置为`renderAttempted`的标志`true`。
* **`inferences`**：推理对象的数组，其中包含有关该用户的机器学习信息。
* **`destinations`**： Edge Network返回的目标对象数组。

## 使用Web SDK标记扩展应用响应

与此命令等效的Web SDK标记扩展是[**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md)操作。
