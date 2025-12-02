---
title: downloadlinkqualifier
description: 帮助确定自动链接跟踪如何限定下载链接。
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `downloadLinkQualifier`

如果使用[`clickCollectionEnabled`](clickcollectionenabled.md)启用自动链接跟踪，`downloadLinkQualifier`属性可帮助确定将URL视为下载链接的条件。

此属性是一个正则表达式字符串。 如果点击的URL与此正则表达式匹配，`xdm.web.webInteraction.type`将设置为`"download"`。 如果链接包含`download` HTML属性，则也会立即将其分类为下载链接。 如果未启用`clickCollectionEnabled`，则此属性不执行任何操作。

运行`downloadLinkQualifier`命令时设置`configure`字符串。 如果省略此属性，则默认使用以下值：

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

如果要使用其他标准来限定下载链接，请将此属性设置为所需的正则表达式值。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```

## 使用Web SDK标记扩展下载链接限定符

配置标记扩展时，此字段的Web SDK标记扩展等效项在[数据收集配置设置](/help/tags/extensions/client/web-sdk/configure/data-collection.md#download-link-qualifier)下。
