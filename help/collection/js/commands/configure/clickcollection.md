---
title: clickCollection
description: 微调单击收藏集设置。
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# `clickCollection`

`clickCollection`对象包含多个帮助您控制自动收集的链接数据的变量。 当您想要在数据收集中包含或排除类型的链接时，请使用这些变量。 Web SDK版本2.25.0或更高版本支持此功能。

此变量需要满足以下所有条件：

* 必须启用[`clickCollectionEnabled`](clickcollectionenabled.md)。
* 如果您使用`clickCollection.filterClickDetails`，则已弃用的方法[`onBeforeLinkClickSend`](onbeforelinkclicksend.md)必须为空。
* 事件有效负载必须在访客访问期间的`xdm.web.webPageDetails.name`中包含一个值。

如果您的实施不满足以上所有要求，则此对象不执行任何操作。

`clickCollection`对象中有以下属性可用：

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| **`internalLinkEnabled`** | `boolean` | 确定是否自动跟踪当前域中的链接。 例如，`https://example.com/index.html`到`https://example.com/product.html`将被视为内部链接。 |
| **`downloadLinkEnabled`** | `boolean` | 根据[`downloadLinkQualifier`](downloadlinkqualifier.md)属性确定库是否跟踪符合下载条件的链接。 |
| **`externalLinkEnabled`** | `boolean` | 确定是否自动跟踪指向外部域的链接。 例如，`https://example.com`到`https://example.net`将被视为外部链接。 |
| **`eventGroupingEnabled`** | `boolean` | 确定库是否等到下一个“页面查看”事件才发送链接跟踪数据。 当有效负载中包含以下元素时，库会将事件视为“页面查看”：<ul><li>`xdm.web.webPageDetails.name`包含字符串值</li><li>`xdm.web.webPageDetails.pageViews.value`大于`0`</li></ul>加载“页面查看”事件后，库会将存储的链接跟踪数据与该事件中的其余数据整合在一起。 启用此选项可减少您发送到Adobe的事件总数。 如果`internalLinkEnabled`被禁用，则此变量不执行任何操作。 |
| **`sessionStorageEnabled`** | `boolean` | 确定链接跟踪数据是否存储在会话存储中而不是存储在本地变量中。 如果`internalLinkEnabled`或`eventGroupingEnabled`被禁用，则此变量不执行任何操作。<br>Adobe强烈建议在使用`eventGroupingEnabled`的单页应用程序之外时启用此变量。 如果在`eventGroupingEnabled`被禁用时启用了`sessionStorageEnabled`，则单击到新页面会导致链接跟踪数据丢失，因为它未保留在会话存储中。 由于单页应用程序通常不会导航到新页面，因此SPA页面不需要会话存储。 |
| **`filterClickDetails`** | `function` | 一种回调函数，可让您完全控制所收集的链接跟踪数据。 您可以使用此回调函数来更改、模糊处理或中止发送链接跟踪数据。 当您要忽略特定信息（如链接中的个人身份信息）时，此回调很有用。 |

如果未在[`configure`](overview.md)命令中设置此对象，则此对象的默认设置取决于[`clickCollectionEnabled`](clickcollectionenabled.md)的值：

* `internalLinkEnabled`：匹配`clickCollectionEnabled`
* `downloadLinkEnabled`：匹配`clickCollectionEnabled`
* `externalLinkEnabled`：匹配`clickCollectionEnabled`
* `eventGroupingEnabled`：默认为`false`；必须显式启用
* `sessionStorageEnabled`：默认为`false`；必须显式启用
* `filterClickDetails`：不包含函数；必须显式注册

>[!TIP]
>
>Adobe建议在启用`eventGroupingEnabled`时启用`internalLinkEnabled`，因为它减少了计入合同使用情况的事件数。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true,
    filterClickDetails: function(content) {
      // If the link is a clickable telephone number, anonymize it
      if(content.linkUrl?.includes("tel:")) {
        content.linkName = content.linkUrl = "Phone number";
      }
      // If the link is an email address, anonymize it
      if(content.linkUrl?.includes("mailto:")) {
        content.linkName = content.linkUrl = "Email address";
      }
    }
  }
});
```

## 为Web SDK标记扩展配置点击收藏集

可以使用[数据收集配置设置](/help/tags/extensions/client/web-sdk/configure/data-collection.md)在Web SDK标记扩展中配置这些设置。
