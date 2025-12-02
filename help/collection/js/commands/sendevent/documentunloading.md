---
title: 文档卸载
description: 使用JavaScript sendBeacon API将数据发送到Adobe。
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: a229cec4a53ab85d13590205a008612719019ebd
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# `documentUnloading`

`documentUnloading`属性允许您使用JavaScript的[`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)方法将数据发送到Adobe。 如果典型请求花费的时间过长，浏览器可以取消该请求。 您可以告知Web SDK使用`sendBeacon`，以便在您离开该页面后，该请求将在后台运行。 启用此属性有助于防止卸载时浏览器取消数据请求。

多个浏览器对可与`sendBeacon`一起发送的数据量施加了64 KB的限制。 如果由于有效负载过大，浏览器拒绝该事件，则Web SDK将回退使用其普通传输方法。 即使给定的浏览器允许更大的负载，Adobe数据收集服务器也会将负载截断为64 KB。

运行`documentUnloading`命令时设置`sendEvent`布尔值。 其默认值为`false`。 如果要使用`true`方法将数据发送到Adobe，请将此属性设置为`sendBeacon`。

>[!IMPORTANT]
>
>`documentUnloading`属性与[`renderDecisions`](renderdecisions.md)属性不兼容。 避免同时将两个属性设置为`true`。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```

## 使用Web SDK标记扩展卸载文档

使用Web SDK标记扩展配置&#x200B;**[!UICONTROL Document will unload]**&#x200B;操作时，[**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields)复选框可用。
