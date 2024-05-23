---
title: renderDecisions
description: 呈现符合自动呈现条件的个性化内容。
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# `renderDecisions`

此 `renderDecisions` 属性允许您强制Web SDK呈现任何符合自动呈现条件的个性化内容。

## 使用Web SDK标记扩展呈现个性化内容

选择 **[!UICONTROL 呈现可视化个性化决策]** 标记规则操作中的复选框。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 规则]**，然后选择所需的规则。
1. 下 [!UICONTROL 操作]，选择现有操作或创建操作。
1. 设置 [!UICONTROL 扩展名] 下拉字段至 **[!UICONTROL Adobe Experience Platform Web SDK]**，并设置 [!UICONTROL 操作类型] 到 **[!UICONTROL 发送事件]**.
1. 向下滚动到 [!UICONTROL 个性化] 部分，然后选择 **[!UICONTROL 呈现可视化个性化决策]** 复选框。
1. 单击 **[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 使用Web SDK JavaScript库呈现个性化内容

设置 `renderDecisions` 布尔值 `sendEvent` 命令。 如果忽略，则此属性默认为 `false`. 将此属性设置为 `true` （如果要自动渲染个性化内容）。

>[!IMPORTANT]
>
>此 `renderDecisions` 属性与 [`documentUnloading`](documentunloading.md) 属性。 您不应将两个属性都设置为 `true` 同时。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
