---
title: orgId
description: orgId属性是一个字符串，用于告知Adobe将数据发送到哪个组织。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

此 `orgId` 属性是一个字符串，用于告知Adobe该数据将发送到哪个组织。 **使用Web SDK发送的所有数据都需要此属性。**

要查找您的 `orgID`：

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 在Adobe Experience Cloud中的任何位置，按 **`[Ctrl]`** + **`[I]`**. A [!UICONTROL 用户数据调试器] 窗口打开。
1. 单击 **[!UICONTROL 复制]** ![复制](../../assets/copy.png) 旁边的 [!UICONTROL 当前组织ID]，或单击 **[!UICONTROL 已分配的组织]** 选项卡以查看您可以访问的其他组织ID。
1. 完成查找所需信息后，单击 **[!UICONTROL 关闭]**.

组织ID始终为24个字符的字母数字字符串，且始终以结尾 `@AdobeOrg`.

## 配置 `orgID` 使用Web SDK标记扩展

输入组织ID **[!UICONTROL IMS组织ID]** 文本字段，条件 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 将所需的组织ID输入到 [!UICONTROL IMS组织ID] 顶部附近的文本字段。
1. 单击 **[!UICONTROL 保存]**，然后发布更改。

## 配置 `orgID` 使用Web SDK JavaScript库

设置 `orgId` 字符串 `configure` 命令。 如果在配置Web SDK时省略此属性，则Web SDK会引发控制台错误，并且数据不会发送到Adobe。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
