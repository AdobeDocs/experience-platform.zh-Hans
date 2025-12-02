---
title: idMigrationEnabled
description: 允许Web SDK读取AMCV Cookie。
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# `idMigrationEnabled`

`idMigrationEnabled`属性允许Web SDK读取由以前的Adobe Experience Cloud实施设置的AMCV Cookie。 如果您的组织将实施升级到Web SDK，则此设置允许更平稳地过渡到当前的Adobe Experience Cloud ID服务。 此设置很有价值，因此在升级到Web SDK时，您不会看到独特访客急剧增加。

如果您的组织运行新的Web SDK实施，则启用此设置不会对数据收集或访客识别产生影响。 让此功能在所有实施中都处于启用状态没有坏处。

运行`idMigrationEnabled`命令时设置`configure`布尔值。 如果在配置Web SDK时省略此属性，则默认设置为`true`。 如果要禁用读取由访客API设置的AMCV Cookie的功能，请设置此属性。 大多数组织不需要设置此属性。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## 使用Web SDK标记扩展启用访客ID迁移

可以使用[身份配置设置](/help/tags/extensions/client/web-sdk/configure/identity.md)在Web SDK标记扩展中配置这些设置。
