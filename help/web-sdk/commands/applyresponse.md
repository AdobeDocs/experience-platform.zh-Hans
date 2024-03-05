---
title: applyResponse
description: 使用来自Edge Network的响应初始化Web SDK。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# `applyResponse`

此 `applyResponse` 命令允许您根据来自Edge Network的响应执行各种操作。 它通常用于混合部署，其中服务器会对Edge Network进行初始调用。 此命令从该调用中获取响应并在浏览器中初始化Web SDK。

## 使用Web SDK标记扩展应用响应

应用响应可作为Adobe Experience Platform数据收集标记界面中规则的一项操作来执行。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 规则]**，然后选择所需的规则。
1. 下 [!UICONTROL 操作]，选择现有操作或创建操作。
1. 设置 [!UICONTROL 扩展名] 下拉字段至 **[!UICONTROL Adobe Experience Platform Web SDK]**，并设置 [!UICONTROL 操作类型] 到 **[!UICONTROL 应用响应]**.
1. 在右侧设置所需字段。
1. 单击 **[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 使用Web SDK JavaScript库应用响应

运行 `applyResponse` 命令。 包含配置选项的对象支持以下字段：

* **`renderDecisions`**：一个布尔值，强制Web SDK呈现任何符合自动呈现条件的个性化内容。 与 [`renderDecisions`](sendevent/renderdecisions.md) 在 [`sendEvent`](sendevent/overview.md) 命令。
* **`responseHeaders`**：字符串标头名称到字符串标头值的映射。
* **`responseBody`**：必填。 从服务器调用到Edge Network的JSON响应主体。
* **`personalization.sendDisplayEvent`**：一个布尔值，它的操作与 [`personalization.sendDisplayEvent`](sendevent/personalization.md) 在 `sendEvent` 命令。

```js
allow("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## 响应对象

如果您决定 [处理响应](command-responses.md) 使用此命令，响应对象中提供了以下属性：

* **`propositions`**：Edge Network返回的一组建议。 自动呈现的建议包含标志 `renderAttempted` 设置为 `true`.
* **`inferences`**：推理对象数组，其中包含有关此用户的机器学习信息。
* **`destinations`**：边缘网络返回的目标对象数组。
