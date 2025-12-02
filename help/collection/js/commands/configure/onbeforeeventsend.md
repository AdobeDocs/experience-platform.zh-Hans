---
title: onBeforeEventSend
description: 了解如何配置Web SDK以注册JavaScript函数，该函数可以更改您在将数据发送到Adobe之前发送的数据。
exl-id: 945f4fa1-380c-46aa-a92a-bbcfd6644751
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# `onBeforeEventSend`

`onBeforeEventSend`回调允许您注册JavaScript函数，该函数可以更改您在将数据发送到Adobe之前发送的数据。 此回调允许您处理`xdm`或`data`对象，包括添加、编辑或删除元素的功能。 您还可以有条件地完全取消发送数据，例如使用检测到的客户端机器人流量。

>[!WARNING]
>
>此回调允许使用自定义代码。 如果您包含在回调中的任意代码引发未捕获的异常，则对事件进行的处理会暂停，并且&#x200B;**数据不会发送到Adobe。**

运行`onBeforeEventSend`命令时注册`configure`回调。 您可以通过更改内联函数中的参数变量，将`content`变量名称更改为所需的任何值。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: function(content) {
    // Use nullish coalescing assignments to add a new value
    content.xdm._experience ??= {};
    content.xdm._experience.analytics ??= {};
    content.xdm._experience.analytics.customDimensions ??= {};
    content.xdm._experience.analytics.customDimensions.eVars ??= {};
    content.xdm._experience.analytics.customDimensions.eVars.eVar1 = "Analytics custom value";
    
    // Use optional chaining to change an existing value
    if(content.xdm.web?.webPageDetails) content.xdm.web.webPageDetails.URL = content.xdm.web.webPageDetails.URL.toLowerCase();
    
    // Remove an existing value
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
    
    // Return true to immediately send data
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
    if(myBotDetector.isABot()){
      return false;
    }
    
    // Assign the value in the 'cid' query string to the tracking code XDM element
    content.xdm.marketing ??= {};
    content.xdm.marketing.trackingCode = new URLSearchParams(window.location.search).get('cid');
  }
});
```

您还可以注册自己的函数，而不是内联函数。

```js
function lastChanceLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```

## 使用Web SDK标记扩展在事件发送回调之前进行配置

可以使用[数据收集配置设置](/help/tags/extensions/client/web-sdk/configure/data-collection.md#on-before-event-send-callback)在Web SDK标记扩展中配置这些设置。
