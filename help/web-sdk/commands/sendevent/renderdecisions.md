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

`renderDecisions`属性允许您强制Web SDK呈现任何适于自动呈现的个性化内容。

## 使用Web SDK标记扩展呈现个性化内容

选中标记规则操作中的&#x200B;**[!UICONTROL 呈现可视化个性化决策]**&#x200B;复选框。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 规则]**，然后选择所需的规则。
1. 在[!UICONTROL 操作]下，选择现有操作或创建操作。
1. 将[!UICONTROL 扩展]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，并将[!UICONTROL 操作类型]设置为&#x200B;**[!UICONTROL 发送事件]**。
1. 向下滚动到[!UICONTROL Personalization]部分，然后选择&#x200B;**[!UICONTROL 呈现可视化个性化决策]**&#x200B;复选框。
1. 单击&#x200B;**[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 使用Web SDK JavaScript库呈现个性化内容

运行`sendEvent`命令时设置`renderDecisions`布尔值。 如果忽略，则此属性默认为`false`。 如果要自动渲染个性化内容，请将此属性设置为`true`。

>[!IMPORTANT]
>
>`renderDecisions`属性与[`documentUnloading`](documentunloading.md)属性不兼容。 您不应将两个属性同时设置为`true`。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
