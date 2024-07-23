---
title: idMigrationEnabled
description: 允许Web SDK读取AMCV Cookie。
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# `idMigrationEnabled`

`idMigrationEnabled`属性允许Web SDK读取由以前的Adobe Experience Cloud实施设置的AMCV Cookie。 如果您的组织将实施升级到Web SDK，则此设置允许更平稳地过渡到当前的Adobe Experience Cloud ID服务。 此设置很有价值，因此在升级到Web SDK时，您不会看到独特访客急剧增加。

如果您的组织运行新的Web SDK实施，则启用此设置不会对数据收集或访客识别产生影响。 让此功能在所有实施中都处于启用状态没有坏处。

## 使用Web SDK标记扩展启用ID迁移

选中[配置标记扩展时&#x200B;**[!UICONTROL 将ECID从VisitorAPI迁移到Web SDK]**&#x200B;复选框](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 扩展]**，然后单击[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 配置]**。
1. 找到[!UICONTROL 标识]部分，然后选中复选框&#x200B;**[!UICONTROL 将ECID从VisitorAPI迁移到Web SDK]**。
1. 单击&#x200B;**[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库启用ID迁移

运行`configure`命令时设置`idMigrationEnabled`布尔值。 如果在配置Web SDK时省略此属性，则默认设置为`true`。 如果要禁用读取由访客API设置的AMCV Cookie的功能，请设置此属性。 大多数组织不需要设置此属性。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```
