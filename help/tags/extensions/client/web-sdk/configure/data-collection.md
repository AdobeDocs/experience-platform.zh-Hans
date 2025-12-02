---
title: 数据收集配置设置
description: 在Web SDK标记扩展中配置数据收集设置。
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# 数据收集配置设置

通过此配置部分，可决定如何跨扩展收集数据。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Extensions]**，然后在&#x200B;**[!UICONTROL Configure]**&#x200B;信息卡上选择[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下滚动到&#x200B;**[!UICONTROL Data collection]**&#x200B;部分。

![在标记UI中显示Web SDK标记扩展的数据收集设置的图像。](../assets/web-sdk-ext-collection.png)

可以使用以下选项：

## [!UICONTROL On before event send callback]

用于评估和修改发送到Adobe的有效负载的回调函数。 在代码编辑器中，您可以访问以下变量：

* **`content.xdm`**：事件的XDM有效负载。
* **`content.data`**：事件的数据对象有效负载。
* **`return true`**：立即退出回调，并使用`content`对象中的当前值将数据发送到Adobe。
* **`return false`**：立即退出回调并中止向Adobe发送数据。

在`content`之外定义的任何变量都可以使用，但不包含在发送到Adobe的有效负载中。

>[!WARNING]
>
>此回调允许使用自定义代码。 如果您包含在回调中的任意代码引发未捕获的异常，则对事件的处理将中止。 **数据未发送到Adobe。**

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

此回调是相当于JavaScript库中[`onBeforeEventSend`](/help/collection/js/commands/configure/onbeforeeventsend.md)的标记。

## [!UICONTROL Collect internal link clicks]

一个复选框，允许收集网站或资产内部的链接跟踪数据。 此复选框的标记等同于JavaScript库中的[`clickCollection.internalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md)。 启用此复选框后，将显示事件分组选项：

* **[!UICONTROL No event grouping]**：链接跟踪数据将在单独的事件中发送到Adobe。 在单独事件中发送链接点击次数可能会增加发送到Adobe Experience Platform的数据在合同中的使用量。
* **[!UICONTROL Event grouping using session storage]**：将链接跟踪数据存储在会话存储中，直到出现下一个“页面查看”事件。 在下一个被视为“页面查看”的事件中，存储的链接跟踪数据将与“页面查看”事件有效负载合并。 Adobe建议在跟踪内部链接时启用此设置。
* **[!UICONTROL Event grouping using local object]**：将链接跟踪数据存储在本地对象中，直到出现下一个“页面查看”事件。 如果访客导航到新的浏览器页面，则链接跟踪数据将丢失。 此设置在单页应用程序的上下文中最为有用。

当有效负载中包含以下元素时，标记库会将给定事件视为“页面查看”：

* `xdm.web.webPageDetails.name`包含字符串值
* `xdm.web.webPageDetails.pageViews.value`大于`0`

## [!UICONTROL Collect external link clicks]

用于启用外部链接集合的复选框。 此复选框的标记等同于JavaScript库中的[`clickCollection.externalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md)。

## [!UICONTROL Collect download link clicks]

用于启用下载链接集合的复选框。 此复选框的标记等同于JavaScript库中的[`clickCollection.downloadLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md)。

## [!UICONTROL Download link qualifier]

将链接URL限定为下载链接的正则表达式。 此字符串的标记等同于JavaScript库中的[`downloadLinkQualifier`](/help/collection/js/commands/configure/downloadlinkqualifier.md)。

## [!UICONTROL Filter click properties]

一个回调函数，用于在集合之前评估和修改与点击相关的属性。 此函数在[!UICONTROL On before event send callback]之前运行，其标记等同于JavaScript库中的[`clickCollection.filterClickDetails`](/help/collection/js/commands/configure/clickcollection.md)。 在代码编辑器中，您可以访问以下变量：

* **`content.clickedElement`**：被单击的DOM元素。
* **`content.pageName`**：发生点击时的页面名称。
* **`content.linkName`**：点击链接的名称。
* **`content.linkRegion`**：点击链接的区域。
* **`content.linkType`**：链接类型（退出、下载或其他）。
* **`content.linkURL`**：点击链接的目标URL。
* **`return true`**：使用当前变量值立即退出回调。
* **`return false`**：立即退出回调并中止收集数据。
* 在`content`之外定义的任何变量都可以使用，但不包含在发送到Adobe的有效负载中。

>[!TIP]
>
>**[!UICONTROL On before link click send]**&#x200B;字段是一个已弃用的回调，它仅对已配置它的属性可见。 该标记等同于JavaScript库中的[`onBeforeLinkClickSend`](/help/collection/js/commands/configure/onbeforelinkclicksend.md)。 使用&#x200B;**[!UICONTROL Filter click properties]**&#x200B;回调筛选或调整点击数据，或使用&#x200B;**[!UICONTROL On before event send callback]**&#x200B;筛选或调整发送到Adobe的整体有效负载。 如果同时设置了&#x200B;**[!UICONTROL Filter click properties]**&#x200B;回调和&#x200B;**[!UICONTROL On before link click send]**&#x200B;回调，则只运行&#x200B;**[!UICONTROL Filter click properties]**&#x200B;回调。

## 上下文设置

自动收集访客信息，这将为您填充特定XDM字段。 您可以选择&#x200B;**[!UICONTROL All default context information]**&#x200B;或&#x200B;**[!UICONTROL Specific context information]**。 该标记等同于JavaScript库中的[`context`](/help/collection/js/commands/configure/context.md)。

* **[!UICONTROL Web]**：收集有关当前页面的信息。
* **[!UICONTROL Device]**：收集有关用户设备的信息。
* **[!UICONTROL Environment]**：收集有关用户浏览器的信息。
* **[!UICONTROL Place context]**：收集有关用户位置的信息。
* **[!UICONTROL High entropy user-agent hints]**：收集有关用户设备的更多详细信息。
