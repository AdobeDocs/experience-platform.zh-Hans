---
title: clickCollectionEnabled
description: 了解如何配置Web SDK以测试是否自动收集链接点击数据。
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# `clickCollectionEnabled`

此 `clickCollectionEnabled` 属性是一个布尔值，用于确定Web SDK是否自动收集链接数据。 如果不设置此变量，则其默认值为 `true` 这意味着默认情况下会自动收集链接跟踪数据。 将此属性设置为 `false` 当您希望手动跟踪链接数据时，非常有用。

时间 `clickCollectionEnabled` 启用后，以下XDM元素会自动填充数据：

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

默认情况下，如果启用此布尔值，则会自动跟踪内部链接、下载链接和退出链接。 如果您希望更好地控制自动链接跟踪，Adobe建议使用 [`clickCollection`](clickcollection.md) 对象。

## 自动链接跟踪逻辑

Web SDK跟踪所有点击 `<a>` 和 `<area>` HTML元素（如果没有） `onClick` 属性。 捕获的点击量 [capture](https://www.w3.org/TR/uievents/#capture-phase) 单击附加到文档的事件侦听器。 在单击有效链接后，将按顺序运行以下逻辑：

1. 如果链接根据中的值匹配标准 [`downloadLinkQualifier`](downloadlinkqualifier.md)，或者，如果链接包含 `download` HTML属性， `xdm.web.webInteraction.type` 设置为 `"download"` (如果 `clickCollection.downloadLinkEnabled` 已启用)。
1. 如果链接目标域不同于当前 `window.location.hostname`， `xdm.web.webInteraction.type` 设置为 `"exit"` (如果 `clickCollection.exitLinkEnabled` 已启用)。
1. 如果链接不符合任一条件 `"download"` 或 `"exit"`， `xdm.web.webInteraction.type` 设置为 `"other"`.

在所有情况下， `xdm.web.webInteraction.name` 设置为链接文本标签，并且 `xdm.web.webInteraction.URL` 设置为链接目标URL。 如果您还想将链接名称设置为URL，则可以使用覆盖此XDM字段 `filterClickDetails` 中的回调 `clickCollection` 对象。

## 使用Web SDK标记扩展启用自动链接跟踪 {#tag-extension}

选择 **[!UICONTROL 启用点击数据收集]** 复选框，条件 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下滚动到 [!UICONTROL 数据收集] 部分，然后选中复选框 **[!UICONTROL 启用点击数据收集]**.
1. 单击 **[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库启用自动链接跟踪 {#library}

设置 `clickCollectionEnabled` 布尔值 `configure` 命令。 如果在配置Web SDK时省略此属性，则默认使用 `true`. 将此值设置为 `false` 如果您希望设置 `xdm.web.webInteraction.type` 和 `xdm.web.webInteraction.value` 手动。

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
