---
title: onBeforeLinkClickSend
description: 在发送链接跟踪数据之前运行的回调。
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>此回调已弃用。 使用 [`filterClickDetails`](clickcollection.md) 而是。

此 `onBeforeLinkClickSend` 回调允许您注册JavaScript函数，该函数可以更改您在将数据发送到Adobe之前发送的链接跟踪数据。 此回调允许您处理 `xdm` 或 `data` 对象，包括添加、编辑或删除元素的功能。 您还可以有条件地完全取消发送数据，例如使用检测到的客户端机器人流量。 Web SDK 2.15.0或更高版本支持此功能。

此回调仅在 [`clickCollectionEnabled`](clickcollectionenabled.md) 已启用，并且 [`filterClickDetails`](clickcollection.md) 不包含已注册的函数。 如果 `clickCollectionEnabled` 已禁用，或者 `filterClickDetails` 包含已注册的函数，则此回调将不会执行。 如果 `onBeforeEventSend` 和 `onBeforeLinkClickSend` 都包含已注册的函数， `onBeforeLinkClickSend` 首先执行。

>[!WARNING]
>
>此回调允许使用自定义代码。 如果您包含在回调中的任意代码引发未捕获的异常，则对事件的处理将中止。 数据不会发送到Adobe。

## 使用Web SDK标记扩展在before link上配置单击发送回调 {#tag-extension}

选择 **[!UICONTROL 在链接前提供点击事件发送回调代码]** 按钮时间 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). 此按钮将打开一个模式窗口，您可以在其中插入所需的代码。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下滚动到 [!UICONTROL 数据收集] 部分，然后选中复选框 **[!UICONTROL 启用点击数据收集]**.
1. 选择标记为的按钮 **[!UICONTROL 在链接前提供点击事件发送回调代码]**.
1. 此按钮将打开一个带代码编辑器的模式窗口。 插入所需的代码，然后单击 **[!UICONTROL 保存]** 以关闭模式窗口。
1. 单击 **[!UICONTROL 保存]** 在扩展设置下，然后发布更改。

在代码编辑器中，您可以访问以下变量：

* **`content.clickedElement`**：被单击的DOM元素。
* **`content.xdm`**：事件的XDM有效负载。
* **`content.data`**：事件的数据对象有效负载。
* **`return true`**：立即使用当前变量值退出回调。 此 `onBeforeEventSend` 如果包含注册的函数，则会运行callback。
* **`return false`**：立即退出回调并中止向Adobe发送数据。 此 `onBeforeEventSend` 不执行回调。

任何在外部定义的变量 `content` 可使用，但不包含在发送到Adobe的有效负载中。

```js
// Set an already existing value to something else
content.xdm.web.webPageDetails.URL = "https://example.com/current.html";

// Use nullish coalescing assignments to create objects if they don't yet exist, preventing undefined errors. 
// Can be omitted if you are certain that the object is already defined
content.xdm._experience ??= {};
content.xdm._experience.analytics ??= {};
content.xdm._experience.analytics.customDimensions ??= {};
content.xdm._experience.analytics.customDimensions.eVars ??= {};

// Then set the property to the clicked element
content.xdm._experience.analytics.customDimensions.eVars.eVar1 = content.clickedElement;

// Use optional chaining to check if each object is defined, preventing undefined errors
if(content.xdm.web?.webInteraction?.type === "other") content.xdm.web.webInteraction.type = "download";
```

类似于 [`onBeforeEventSend`](onbeforeeventsend.md)，您可以 `return true` 立即完成功能，或者 `return false` 以中止将数据发送到Adobe。 如果中止在中发送数据 `onBeforeLinkClickSend` 当两者 `onBeforeEventSend` 和 `onBeforeLinkClickSend` 包含已注册的函数， `onBeforeEventSend` 函数未运行。

## 在链接之前配置，单击使用Web SDK JavaScript库发送回调 {#library}

注册 `onBeforeLinkClickSend` 运行 `configure` 命令。 您可以更改 `content` 变量名称为所需的任何值（通过更改内联函数中的参数变量）。

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to complete the function immediately
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to cancel sending data immediately
    if(myBotDetector.isABot()){
      return false;
    }
  }
});
```

您还可以注册自己的函数，而不是内联函数。

```js
function lastChanceLinkLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: lastChanceLinkLogic
});    
```
