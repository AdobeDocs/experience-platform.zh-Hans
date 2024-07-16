---
title: applyResponse
description: 使用来自Edge Network的响应初始化Web SDK。
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: 74725546163f0807d3188aff5b5ffda9b8d6350b
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# `applyResponse`

`applyResponse`命令允许您根据Edge Network的响应执行各种操作。 它通常用于混合部署，其中服务器会对Edge Network进行初始调用。 此命令从该调用中获取响应并在浏览器中初始化Web SDK。

## 使用Web SDK标记扩展应用响应

应用响应可作为Adobe Experience Platform数据收集标记界面中规则的一项操作来执行。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 规则]**，然后选择所需的规则。
1. 在[!UICONTROL 操作]下，选择现有操作或创建操作。
1. 将[!UICONTROL 扩展]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，并将[!UICONTROL 操作类型]设置为&#x200B;**[!UICONTROL 应用响应]**。
1. 在右侧设置所需字段。
1. 单击&#x200B;**[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 使用Web SDK JavaScript库应用响应

调用Web SDK的配置实例时运行`applyResponse`命令。 包含配置选项的对象支持以下字段：

* **`renderDecisions`**：一个布尔值，强制Web SDK呈现任何符合自动呈现条件的个性化内容。 与[`sendEvent`](sendevent/overview.md)命令中的[`renderDecisions`](sendevent/renderdecisions.md)相同。
* **`responseHeaders`**：字符串标头名称到字符串标头值的映射。
* **`responseBody`**：必需。 来自对Edge Network的服务器调用的JSON响应主体。
* **`personalization.sendDisplayEvent`**： `sendEvent`命令中与[`personalization.sendDisplayEvent`](sendevent/personalization.md)运行方式相同的布尔值。

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

* **`propositions`**：Edge Network返回的建议数组。 自动呈现的建议包括设置为`true`的标志`renderAttempted`。
* **`inferences`**：推理对象的数组，其中包含有关该用户的机器学习信息。
* **`destinations`**：Edge Network返回的目标对象数组。
