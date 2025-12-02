---
title: Targetmigrationenabled
description: 允许Web SDK读取和写入Adobe Target Cookie。
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: dade74bf4a5cfd7b60eaf216583deb67b93a61db
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# `targetMigrationEnabled`

`targetMigrationEnabled`属性是一个布尔值，它允许Web SDK读取和写入Adobe Target 1.x和2.x库使用的[`mbox`和`mboxEdgeCluster` Cookie](https://experienceleague.adobe.com/zh-hans/docs/core-services/interface/data-collection/cookies/web-sdk)。 通过此选项，您可以在使用以前的Adobe Target实施的页面与使用Web SDK的页面之间保留访客配置文件。

运行`targetMigrationEnabled`命令时设置`configure`布尔值。 如果在配置Web SDK时省略此属性，则默认设置为`false`。 如果您的某些页面仍使用Adobe Target 1.x或2.x库，请将此值设置为`true`。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```

## 使用Web SDK标记扩展启用Target迁移

可以使用[Personalization配置设置](/help/tags/extensions/client/web-sdk/configure/personalization.md#migrate-target-from-atjs-to-the-web-sdk)在Web SDK标记扩展中配置此设置。
