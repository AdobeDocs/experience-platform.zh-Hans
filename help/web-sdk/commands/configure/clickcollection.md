---
title: clickCollection
description: 微调单击收藏集设置。
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---


# `clickCollection`

此 `clickCollection` 对象包含多个变量，可帮助您控制自动收集的链接数据。 当您想要在数据收集中包含或排除类型的链接时，请使用这些变量。

它需要 [`clickCollectionEnabled`](clickcollectionenabled.md) 已启用。

Web SDK 2.25.0或更高版本支持此功能。

以下变量可在 `clickCollection` 对象：

* **`clickCollection.internalLinkEnabled`**：一个布尔值，确定是否自动跟踪当前域中的链接。 例如， `https://example.com/index.html` 到 `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**：一个布尔值，用于确定库是否根据 [`downloadLinkQualifier`](downloadlinkqualifier.md) 属性。
* **`clickCollection.externalLinkEnabled`**：一个布尔值，确定是否自动跟踪指向外部域的链接。 例如， `https://example.com` 到 `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**：一个布尔值，用于确定库是否等到下一页发送链接跟踪数据。 加载下一页面时，将链接跟踪数据与页面加载事件相结合。 启用此选项可减少您发送到Adobe的事件数。 如果 `internalLinkEnabled` 禁用，则此变量不执行任何操作。
* **`clickCollection.sessionStorageEnabled`**：一个布尔值，用于确定链接跟踪数据是存储在会话存储中还是存储在本地变量中。 如果 `internalLinkEnabled` 或 `eventGroupingEnabled` 禁用，则此变量不执行任何操作。

  Adobe强烈建议在以下情况下启用此变量： `eventGroupingEnabled`. 如果 `eventGroupingEnabled` 已启用，但 `sessionStorageEnabled` 将禁用，单击到新页面会导致链接跟踪数据丢失，因为它未保留在会话存储中。 虽然可以禁用 `sessionStorageEnabled` 在单页应用程序中，它不适用于非SPA页面。
* **`filterClickDetails`**：回调函数，对您收集的链接跟踪数据提供完全控制。 您可以使用此回调函数来更改、模糊处理或中止发送链接跟踪数据。 当您要忽略特定信息（如链接中的个人身份信息）时，此回调很有用。

## 单击使用Web SDK标记扩展的收藏集设置

选择 **[!UICONTROL 启用点击数据收集]** 复选框，条件 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). 启用此复选框将显示以下与点击收藏集相关的选项：

* [!UICONTROL 内部链接]
   * [!UICONTROL 启用事件分组]
   * [!UICONTROL 启用会话存储]
* [!UICONTROL 外部链接]
* [!UICONTROL 下载链接]
* [!UICONTROL 筛选点击属性]

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下滚动到 [!UICONTROL 数据收集] 部分，然后选中复选框 **[!UICONTROL 启用点击数据收集]**.
1. 选择所需的单击收藏集设置。
1. 单击 **[!UICONTROL 保存]**，然后发布更改。

此 [!UICONTROL 筛选点击属性] callback会打开一个自定义代码编辑器，允许您插入所需的代码。 在代码编辑器中，您可以访问以下变量：

* **`content.clickedElement`**：被单击的DOM元素。
* **`content.pageName`**：发生单击时的页面名称。
* **`content.linkName`**：点击链接的名称。
* **`content.linkRegion`**：点击链接的区域。
* **`content.linkType`**：链接类型（退出、下载或其他）。
* **`content.linkURL`**：点击链接的目标URL。
* **`return true`**：立即使用当前变量值退出回调。
* **`return false`**：立即退出回调并中止收集数据。

任何在外部定义的变量 `content` 可使用，但不包含在发送到Adobe的有效负载中。

## 单击使用Web SDK JavaScript库的收藏集设置

在中设置所需的变量 `clickCollection` 对象 [`configure`](overview.md) 命令。 如果未设置，则此对象的默认设置取决于 [`clickCollectionEnabled`](clickcollectionenabled.md).

* `internalLinkEnabled`：匹配 `clickCollectionEnabled`
* `downloadLinkEnabled`：匹配 `clickCollectionEnabled`
* `externalLinkEnabled`：匹配 `clickCollectionEnabled`
* `eventGroupingEnabled`：默认为 `false`；必须显式启用
* `sessionStorageEnabled`：默认为 `false`；必须显式启用
* `filterClickDetails`：不包含函数；必须显式注册

>[!TIP]
>Adobe建议启用 `eventGroupingEnabled`，因为它有助于减少计入合同使用的事件数量。

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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
