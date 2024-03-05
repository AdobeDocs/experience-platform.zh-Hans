---
title: onBeforeEventSend
description: 在发送数据之前运行的回调。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# `onBeforeEventSend`

此 `onBeforeEventSend` 回调允许您注册JavaScript函数，该函数可以更改您在将数据发送到Adobe之前发送的数据。 此回调允许您处理 `xdm` 或 `data` 对象，包括添加、编辑或删除元素的功能。 您还可以有条件地完全取消发送数据，例如使用检测到的客户端机器人流量。

>[!WARNING]
>
>此回调允许使用自定义代码。 如果您包含在回调中的任意代码引发未捕获的异常，则对事件的处理将中止。 数据不会发送到Adobe。

## 使用Web SDK标记扩展在before事件发送回调时开启

选择 **[!UICONTROL 在事件发送回调代码之前提供]** 按钮时间 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). 此按钮将打开一个模式窗口，您可以在其中插入所需的代码。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下滚动到 [!UICONTROL 数据收集] 部分，然后选择按钮 **[!UICONTROL 在事件发送回调代码之前提供]**.
1. 此按钮将打开一个带代码编辑器的模式窗口。 插入所需的代码，然后单击 **[!UICONTROL 保存]** 以关闭模式窗口。
1. 单击 **[!UICONTROL 保存]** 在扩展设置下，然后发布更改。

在代码编辑器中，您可以添加、编辑或删除以下项中的元素： `content` 对象。 此对象包含发送到Adobe的有效负载。 您无需定义 `content` 对象，或将任何代码包装在函数中。 任何在外部定义的变量 `content` 可使用，但不包含在发送到Adobe的有效负载中。

>[!TIP]
>
>对象 `content.xdm` 和 `content.data` 始终在此上下文中定义，因此无需检查它们是否存在。 这些对象中的某些变量取决于您的实施和数据层。 Adobe建议检查这些对象中的未定义值以防止JavaScript错误。

例如，如果您想要：

* 添加XDM元素 `xdm.commerce.order.purchaseID`
* 强制所有字符位于 `xdm.marketing.trackingCode` 转换为小写
* 删除 `xdm.environment.operatingSystemVersion`
* 如果事件类型是链接点击，则会立即发送数据，而不考虑其下方的代码
* 如果检测到机器人，取消向Adobe发送数据

模态窗口中的等效代码如下所示：

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

>[!NOTE]
>
>避免返回 `false` 在页面上的第一个事件中。 正在返回 `false` 对于第一个事件，可能会对个性化产生负面影响。

## 在事件使用Web SDK JavaScript库发送回调之前

注册 `onBeforeEventSend` 运行 `configure` 命令。 您可以更改 `content` 变量名称为所需的任何值（通过更改内联函数中的参数变量）。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
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
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": lastChanceLogic
});    
```
