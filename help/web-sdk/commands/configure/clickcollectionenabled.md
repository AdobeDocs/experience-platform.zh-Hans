---
title: clickCollectionEnabled
description: 了解如何配置Web SDK以测试是否自动收集链接点击数据。
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# `clickCollectionEnabled`

`clickCollectionEnabled`属性是一个布尔值，用于确定Web SDK是否自动收集链接数据。 如果不设置此变量，则其默认值为`true`，这意味着默认情况下会自动收集链接跟踪数据。 如果您希望手动跟踪链接数据，则将此属性设置为`false`很有用。

启用`clickCollectionEnabled`后，以下XDM元素会自动填充数据：

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

默认情况下，如果启用此布尔值，则会自动跟踪内部链接、下载链接和退出链接。 如果要更好地控制自动链接跟踪，Adobe建议使用[`clickCollection`](clickcollection.md)对象。

## 自动链接跟踪逻辑

如果Web SDK不具有`onClick`属性，则它会跟踪`<a>`和`<area>`HTML元素上的所有点击。 点击通过附加到文档的[捕获](https://www.w3.org/TR/uievents/#capture-phase)点击事件侦听器捕获。 在单击有效链接后，将按顺序运行以下逻辑：

1. 如果链接基于[`downloadLinkQualifier`](downloadlinkqualifier.md)中的值匹配条件，或者如果链接包含`download`HTML属性，则`xdm.web.webInteraction.type`设置为`"download"`（如果已启用`clickCollection.downloadLinkEnabled`）。
1. 如果链接目标域与当前`window.location.hostname`不同，`xdm.web.webInteraction.type`将设置为`"exit"`（如果已启用`clickCollection.exitLinkEnabled`）。
1. 如果该链接不符合`"download"`或`"exit"`的条件，则`xdm.web.webInteraction.type`将设置为`"other"`。

在所有情况下，`xdm.web.webInteraction.name`都设置为链接文本标签，`xdm.web.webInteraction.URL`设置为链接目标URL。 如果您还想将链接名称设置为URL，则可以使用`clickCollection`对象中的`filterClickDetails`回调覆盖此XDM字段。

## 使用Web SDK标记扩展启用自动链接跟踪 {#tag-extension}

此变量由标记扩展自动管理；您无需明确设置它。 如果在[配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)时选择以下任一项，则会收集适用的链接跟踪数据：

* [!UICONTROL 收集内部链接点击次数]
* [!UICONTROL 收集外部链接点击次数]
* [!UICONTROL 收集下载链接点击次数]

有关详细信息，请参阅[`clickCollection`](clickcollection.md)。

## 使用Web SDK JavaScript库启用自动链接跟踪 {#library}

运行`configure`命令时设置`clickCollectionEnabled`布尔值。 如果在配置Web SDK时省略此属性，则默认设置为`true`。 如果您希望手动设置`xdm.web.webInteraction.type`和`xdm.web.webInteraction.value`，请将此值设置为`false`。

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
