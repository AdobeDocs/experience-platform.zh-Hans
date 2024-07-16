---
title: onBeforeEventSend
description: 了解如何配置Web SDK以注册JavaScript函数，该函数可以更改您在将数据发送到Adobe之前发送的数据。
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# `onBeforeEventSend`

`onBeforeEventSend`回调允许您注册JavaScript函数，该函数可以更改您在将数据发送到Adobe之前发送的数据。 此回调允许您处理`xdm`或`data`对象，包括添加、编辑或删除元素的功能。 您还可以有条件地完全取消发送数据，例如使用检测到的客户端机器人流量。

>[!WARNING]
>
>此回调允许使用自定义代码。 如果您包含在回调中的任意代码引发未捕获的异常，则对事件的处理将中止。 数据不会发送到Adobe。

## 使用Web SDK标记扩展在事件发送回调之前进行配置 {#tag-extension}

在[配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)时，选择&#x200B;**[!UICONTROL 在事件发送回调代码之前提供]**&#x200B;按钮。 此按钮将打开一个模式窗口，您可以在其中插入所需的代码。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 扩展]**，然后单击[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 配置]**。
1. 向下滚动到[!UICONTROL 数据收集]部分，然后选择按钮&#x200B;**[!UICONTROL 在事件发送回调代码之前提供]**。
1. 此按钮将打开一个带代码编辑器的模式窗口。 插入所需的代码，然后单击&#x200B;**[!UICONTROL 保存]**&#x200B;以关闭模式窗口。
1. 单击扩展设置下的&#x200B;**[!UICONTROL 保存]**，然后发布更改。

在代码编辑器中，您可以访问以下变量：

* **`content.xdm`**：事件的[XDM](../sendevent/xdm.md)有效负载。
* **`content.data`**：事件的[data](../sendevent/data.md)对象有效负载。
* **`return true`**：立即退出回调，并使用`content`对象中的当前值将数据发送到Adobe。
* **`return false`**：立即退出回调并中止向Adobe发送数据。

在`content`之外定义的任何变量都可以使用，但不包括在发送到Adobe的有效负载中。

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!TIP]
>避免在页面上的第一个事件中返回`false`。 在第一个事件中返回`false`可能会对个性化产生负面影响。

## 使用Web SDK JavaScript库在事件发送回调之前进行配置 {#library}

运行`configure`命令时注册`onBeforeEventSend`回调。 您可以通过更改内联函数中的参数变量，将`content`变量名称更改为所需的任何值。

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```
