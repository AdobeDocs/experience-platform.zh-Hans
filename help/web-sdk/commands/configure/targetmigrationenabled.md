---
title: Targetmigrationenabled
description: 允许Web SDK读取和写入Adobe Target Cookie。
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

此 `targetMigrationEnabled` 属性是一个布尔值，允许Web SDK读取和写入Adobe Target 1.x和2.x库使用的mbox和mboxEdgeCluster Cookie。 通过此选项，您可以在使用以前的Adobe Target实施的页面与使用Web SDK的页面之间保留访客配置文件。

## 使用Web SDK标记扩展启用从at.js的Target迁移

选择 **[!UICONTROL 将Target从at.js迁移到Web SDK]** 复选框，条件 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下滚动到 [!UICONTROL 个性化] 部分，然后选中复选框 **[!UICONTROL 将Target从at.js迁移到Web SDK]**.
1. 单击 **[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库启用从at.js的Target迁移

设置 `targetMigrationEnabled` 布尔值 `configure` 命令。 如果在配置Web SDK时省略此属性，则默认使用 `false`. 将此值设置为 `true` 如果您的某些页面仍使用Adobe Target 1.x或2.x库，请执行以下操作。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
