---
title: idMigrationEnabled
description: 允许Web SDK读取AMCV Cookie。
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# `idMigrationEnabled`

`idMigrationEnabled`属性允许Web SDK读取由以前的Adobe Experience Cloud实施设置的AMCV Cookie。 如果您的组织将实施升级到Web SDK，则此设置允许更平稳地过渡到当前的Adobe Experience Cloud ID服务。 此设置很有价值，因此在升级到Web SDK时，您不会看到独特访客急剧增加。

如果您的组织运行新的Web SDK实施，则启用此设置不会对数据收集或访客识别产生影响。 让此功能在所有实施中都处于启用状态没有坏处。

## 身份迁移的工作方式 {#how-it-works}

访客API将Experience Cloud ID (ECID)存储在名为`AMCV_<ORG_ID>`的Cookie中。 当`idMigrationEnabled`为`true`（默认值）时，Web SDK会自动从AMCV Cookie中读取ECID，并在第一个Edge Network请求中将其用作访客的身份。

1. 访客到达的页面现在使用的是Web SDK而不是访客API。
1. Web SDK检查现有`kndctr_`身份Cookie（它自己的Cookie格式）。 如果未找到，则查找`AMCV_` Cookie。
1. 如果找到`AMCV_` Cookie，Web SDK将提取ECID并使用它初始化访客身份。
1. Web SDK使用相同的ECID设置新的`kndctr_`身份Cookie。
1. 在后续访问中，Web SDK直接使用`kndctr_` Cookie。 不再需要`AMCV_` Cookie。

为使迁移正常工作，必须将Web SDK配置为使用访客API使用的相同[`orgId`](/help/collection/js/commands/configure/orgid.md)，并且必须在设置AMCV Cookie的相同域（或相同父域的子域）上部署。

## 支持的迁移方案

ID迁移支持以下过渡模式：

* **某些页面仍使用访客API，而其他页面则使用Web SDK**： SDK会读取现有AMCV Cookie并使用现有ECID写入新的Cookie。 它还写入AMCV Cookie，以便仍在使用访客API的页面继续识别同一访客。
* **Web SDK和访客API都存在于同一页面上**：如果未设置AMCV Cookie，SDK将在页面上查找访客API并使用它获取ECID。
* **该站点已完全移至Web SDK**：您可以在一段时间内保持启用迁移，以便现有基于AMCV的访客在转换Cookie时保持连续性。

>[!IMPORTANT]
>
>除非您确认已设置AMCV Cookie，否则不要在同一页面上同时加载访客API和Web SDK。 在单个页面上运行两个库可能会导致争用情况，在这种情况下，每个库都会尝试单独管理身份，从而生成重复或冲突的ECID。

## 关闭迁移 {#turn-off-migration}

当整个网站在Web SDK上运行并且没有访客只携带不带相应`AMCV_` Cookie的`kndctr_` Cookie后，您可以通过将`idMigrationEnabled`设置为`false`安全地禁用身份迁移。 这是次要的性能优化，可缩小标识逻辑的表面积。

作为指导，请等待AMCV Cookie的最长生命周期在迁移最后一个页面后过期。 如果您的AMCV Cookie有效期为两年，请在最终页面切换到Web SDK后等待两年。 实际上，大多数组织会更早（在几个月后）禁用迁移，并接受数量较少的访客在长时间缺席后首次回访所产生的微不足道的虚增。

## Audience Manager特征更新

在迁移期间将XDM格式的数据发送到Audience Manager时，必须将该数据转换为信号。 必须更新您的特征以反映XDM提供的新密钥。 使用[BAAAM工具](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management)可简化此过程。

## 第三方ID迁移 {#third-party-id}

如果您的访客API实施使用第三方ID(`demdex.net` Cookie)，则Web SDK也可以迁移它们。 在Web SDK配置中将[`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md)配置为`true`。 Web SDK读取现有Demdex Cookie，并将第三方身份包含在其Edge Network请求中，迁移模式与AMCV Cookie相同。

## 验证 {#validation}

要验证身份迁移是否正常工作，请执行以下操作：

1. 在现有`AMCV_` Cookie的浏览器中打开以前使用访客API（现在使用Web SDK）的页面。
2. 在开发人员工具中，验证是否已设置`kndctr_`标识Cookie，并且ECID是否与`AMCV_` Cookie中的标识匹配。
3. 部署后，比较迁移前后同一时间段的独特访客计数。 独特访客数量显着增加可能表明迁移未使身份向前发展。

>[!TIP]
>
>使用`getIdentity`以编程方式检索ECID以进行比较：
>
>```js
>alloy("getIdentity", { namespaces: ["ECID"] }).then(function(result) {
>   console.log("ECID:", result.identity.ECID);
>});
>```

## 配置`idMigrationEnabled` {#configure}

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
