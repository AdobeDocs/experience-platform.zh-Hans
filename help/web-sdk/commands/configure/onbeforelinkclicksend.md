---
title: onBeforeLinkClickSend
description: 在发送链接跟踪数据之前运行的回调。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

此 `onBeforeLinkClickSend` 回调允许您注册JavaScript函数，该函数可以更改您在将数据发送到Adobe之前发送的链接跟踪数据。 此回调允许您处理 `xdm` 或 `data` 对象，包括添加、编辑或删除元素的功能。 您还可以有条件地完全取消发送数据，例如使用检测到的客户端机器人流量。 Web SDK 2.15.0或更高版本支持此功能。

此回调仅在 [`clickCollectionEnabled`](clickcollectionenabled.md) 已启用。 如果 `clickCollectionEnabled` 禁用，此回调不会执行。 如果两者 `onBeforeEventSend` 和 `onBeforeLinkClickSend` 包含已注册的函数， `onBeforeLinkClickSend` 函数首先执行。 一旦 `onBeforeLinkClickSend` 函数结束， `onBeforeEventSend` 然后执行函数。

>[!WARNING]
>
>此回调允许使用自定义代码。 如果您包含在回调中的任意代码引发未捕获的异常，则对事件的处理将中止。 数据不会发送到Adobe。

## 在before link上，单击使用Web SDK标记扩展发送回调

选择 **[!UICONTROL 在链接前提供点击事件发送回调代码]** 按钮时间 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). 此按钮将打开一个模式窗口，您可以在其中插入所需的代码。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下滚动到 [!UICONTROL 数据收集] 部分，然后选中复选框 **[!UICONTROL 启用点击数据收集]**.
1. 选择标记为的按钮 **[!UICONTROL 在链接前提供点击事件发送回调代码]**.
1. 此按钮将打开一个带代码编辑器的模式窗口。 插入所需的代码，然后单击 **[!UICONTROL 保存]** 以关闭模式窗口。
1. 单击 **[!UICONTROL 保存]** 在扩展设置下，然后发布更改。

在代码编辑器中，您可以添加、编辑或删除以下项中的元素： `content` 对象。 此对象包含发送到Adobe的有效负载。 您无需定义 `content` 对象，或将任何代码包装在函数中。 任何在外部定义的变量 `content` 可使用，但不包含在发送到Adobe的有效负载中。

>[!TIP]
>
>对象 `content.xdm`， `content.data`、和 `content.clickedElement` 始终在此上下文中定义，因此无需检查它们是否存在。 这些对象中的某些变量取决于您的实施和数据层。 Adobe建议检查这些对象中的未定义值以防止JavaScript错误。

例如，假设您要执行以下操作：

* 修改当前页面URL
* 捕获Adobe AnalyticseVar中点击的元素
* 将链接类型从“其他”更改为“下载”

模态窗口中的等效代码如下所示：

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

类似于 [`onBeforeEventSend`](onbeforeeventsend.md)，您可以 `return true` 立即完成功能，或者 `return false` 立即取消发送数据。 如果您取消在中发送数据 `onBeforeLinkClickSend` 当两者 `onBeforeEventSend` 和 `onBeforeLinkClickSend` 包含已注册的函数， `onBeforeEventSend` 函数未运行。

## 在链接之前单击使用Web SDK JavaScript库发送回调

注册 `onBeforeLinkClickSend` 运行 `configure` 命令。 您可以更改 `content` 变量名称为所需的任何值（通过更改内联函数中的参数变量）。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to immediately complete the function
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
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
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": lastChanceLinkLogic
});    
```
