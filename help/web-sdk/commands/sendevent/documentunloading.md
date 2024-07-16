---
title: 文档卸载
description: 使用JavaScript sendBeacon API将数据发送到Adobe。
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# `documentUnloading`

`documentUnloading`属性允许您使用JavaScript的[`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)方法将数据发送到Adobe。 如果典型请求花费的时间过长，浏览器可以取消该请求。 您可以指示Web SDK使用`sendBeacon`，以便在您离开页面后，请求在后台运行。 启用此属性有助于防止卸载时浏览器取消数据请求。

多个浏览器对可与`sendBeacon`一起发送的数据量施加了64 KB的限制。 如果浏览器因有效负载过大而拒绝事件，则Web SDK将回退以使用其常规传输方法。

## 使用Web SDK标记扩展配置文档卸载

启用标记规则操作中的&#x200B;**[!UICONTROL 文档将卸载]**&#x200B;复选框。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 规则]**，然后选择所需的规则。
1. 在[!UICONTROL 操作]下，选择现有操作或创建操作。
1. 将[!UICONTROL 扩展]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，并将[!UICONTROL 操作类型]设置为&#x200B;**[!UICONTROL 发送事件]**。
1. 启用[!UICONTROL 数据]部分中的&#x200B;**[!UICONTROL 文档将卸载]**&#x200B;复选框。
1. 单击&#x200B;**[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 使用Web SDK JavaScript库配置文档卸载

运行`sendEvent`命令时设置`documentUnloading`布尔值。 其默认值为`false`。 如果要使用`sendBeacon`方法将数据发送到Adobe，请将此属性设置为`true`。

>[!IMPORTANT]
>
>`documentUnloading`属性与[`renderDecisions`](renderdecisions.md)属性不兼容。 您不应将两个属性同时设置为`true`。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
