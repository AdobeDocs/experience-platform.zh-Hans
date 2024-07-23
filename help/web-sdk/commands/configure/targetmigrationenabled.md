---
title: Targetmigrationenabled
description: 允许Web SDK读取和写入Adobe Target Cookie。
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

`targetMigrationEnabled`属性是一个布尔值，允许Web SDK读取和写入Adobe Target 1.x和2.x库使用的mbox和mboxEdgeCluster Cookie。 通过此选项，您可以在使用以前的Adobe Target实施的页面与使用Web SDK的页面之间保留访客配置文件。

## 使用Web SDK标记扩展启用从at.js的Target迁移

选中[配置标记扩展时&#x200B;**[!UICONTROL 将Target从at.js迁移到Web SDK]**&#x200B;复选框](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 扩展]**，然后单击[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 配置]**。
1. 向下滚动到[!UICONTROL Personalization]部分，然后选中复选框&#x200B;**[!UICONTROL 将Target从at.js迁移到Web SDK]**。
1. 单击&#x200B;**[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库启用从at.js的Target迁移

运行`configure`命令时设置`targetMigrationEnabled`布尔值。 如果在配置Web SDK时省略此属性，则默认设置为`false`。 如果您的某些页面仍使用Adobe Target 1.x或2.x库，请将此值设置为`true`。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```
