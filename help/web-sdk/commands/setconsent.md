---
title: setConsent
description: 用于每个页面，以跟踪用户的同意首选项。
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: 83b4745693749c5f50791d6efeb3a7ba02a4cce5
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 3%

---


# `setConsent`

`setConsent`命令告知Web SDK是应发送数据（选择启用）、丢弃数据（选择禁用）还是使用[`defaultConsent`](configure/defaultconsent.md)（同意未知）。

Web SDK支持以下标准：

* **[Adobe standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**：同时支持1.0和2.0标准。
* **[IAB透明度和同意框架](/help/landing/governance-privacy-security/consent/iab/overview.md)**：如果使用此标准，且您的实施配置正确，则访客的实时客户配置文件将更新为同意信息：
   1. XDM个人配置文件架构包含[IAB TCF 2.0同意字段组](/help/xdm/field-groups/profile/iab.md)。
   1. 体验事件架构包含[IAB TCF 2.0同意字段组](/help/xdm/field-groups/event/iab.md)。
   1. 您将IAB同意信息包含在事件[XDM对象](sendevent/xdm.md)中。 在发送事件数据时，Web SDK不会自动包含同意信息。

使用此命令后，Web SDK会将用户的首选项写入Cookie。 下次用户在浏览器中加载您的网站时，SDK将检索这些保留的首选项，以确定是否可将事件发送到Adobe。

Adobe建议您将任何同意对话框首选项与Web SDK同意分开存储。 Web SDK不提供检索同意的方法。 为确保用户首选项与SDK保持同步，您可以在每次加载页面时调用`setConsent`命令。 Web SDK仅在同意更改时进行服务器调用。

## 身份同步注意事项 {#identity-considerations}

`setConsent`命令仅使用标识映射中的`ECID`，因为该命令在设备级别运行。 `setConsent`命令不考虑标识映射中的其他标识。

## 将`defaultConsent`与`setConsent`一起使用 {#using-consent}

Web SDK提供了两个互补的同意配置命令：

* [`defaultConsent`](configure/defaultconsent.md)：此命令用于捕获使用Web SDK的Adobe客户的同意首选项。
* [`setConsent`](setconsent.md)：此命令用于捕获网站访客的同意首选项。

如果同时使用这些设置，则可能会导致数据收集和Cookie设置结果有所不同，具体取决于其配置的值。

请参阅下表，根据同意设置了解何时进行数据收集以及何时设置Cookie。

| defaultconsent | setConsent | 发生数据收集 | Web SDK设置浏览器Cookie |
|---------|----------|---------|---------|
| `in` | `in` | 是 | 是 |
| `in` | `out` | 否 | 是 |
| `in` | 未设置 | 是 | 是 |
| `pending` | `in` | 是 | 是 |
| `pending` | `out` | 否 | 是 |
| `pending` | 未设置 | 否 | 否 |
| `out` | `in` | 是 | 是 |
| `out` | `out` | 否 | 是 |
| `out` | 未设置 | 否 | 否 |

在同意配置允许时设置以下Cookie：

| 名称 | 最大年龄 | 描述 |
|---|---|---|
| **AMCV_###@AdobeOrg** | 34128000（395天） | 启用[`idMigrationEnabled`](configure/idmigrationenabled.md)时存在。 当站点的某些部分仍在使用`visitor.js`时，转换到Web SDK会很有帮助。 |
| **Demdex Cookie** | 15552000（180天） | 如果启用了ID同步，则会显示。 Audience Manager通过设置此Cookie来向网站访客分配唯一ID。 demdex Cookie可帮助Audience Manger执行基本的功能，例如访客识别、ID同步、分段、建模和报告等。 |
| **kndctr_orgid_cluster** | 1800（30分钟） | 存储Edge Network区域以满足当前用户的请求。 URL路径中使用区域，以便Edge Network能够将请求路由到正确的区域。 如果用户使用不同的IP地址或以不同的会话连接，则请求将再次路由到最近的区域。 |
| **kndct_orgid_identity** | 34128000（395天） | 存储ECID以及与ECID相关的其他信息。 |
| **kndctr_orgid_consent** | 15552000（180天） | 存储网站的用户同意首选项。 |
| **s_ecid** | 63115200（2年） | 包含Experience Cloud ID ([!DNL ECID])或MID的副本。 MID 存储在一个键值对中，它遵循以下语法：`s_ecid=MCMID\|<ECID>`。 |

## 使用Web SDK标记扩展设置同意

在Adobe Experience Platform数据收集标记界面中，将同意设置作为规则中的一项操作。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 规则]**，然后选择所需的规则。
1. 在[!UICONTROL 操作]下，选择现有操作或创建操作。
1. 将[!UICONTROL 扩展]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，并将[!UICONTROL 操作类型]设置为&#x200B;**[!UICONTROL 设置同意]**。
1. 在右侧设置所需字段，包括&#x200B;**[!UICONTROL 标准]**&#x200B;和&#x200B;**[!UICONTROL 一般同意]**。
1. 单击&#x200B;**[!UICONTROL 保留更改]**，然后运行发布工作流程。

您可以在此操作中包含多个同意对象。

## 使用Web SDK JavaScript库设置同意

调用Web SDK的配置实例时运行`setConsent`命令。 您可以在此命令中包含以下对象：

* **`consent[]`**： `consent`对象的数组。 同意对象的格式有所不同，具体取决于您选择的标准和版本。 有关每个同意对象的示例，请参见下面的选项卡，具体取决于同意标准。
* **`identityMap`**：一个对象，它控制如何生成ECID以及同意信息绑定到哪些ID。 Adobe建议当`setConsent`在其他命令（如[`sendEvent`](sendevent/overview.md)）之前运行时包含此对象。
* **`edgeConfigOverrides`**：包含[数据流配置的对象将覆盖](datastream-overrides.md)。

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0标准`consent`对象

如果您使用的是Adobe Experience Platform，则需要在配置文件架构中包含隐私架构字段组。 有关Adobe Experience Platform 2.0标准的更多信息，请参阅[Adobe中的治理、隐私和安全性](../../landing/governance-privacy-security/overview.md)。 您可以在对应于[!UICONTROL 同意和偏好设置]配置文件字段组的`consents`字段的架构的下方值对象中添加数据。

* **`standard`**：您选择的同意标准。 为Adobe 2.0标准将此属性设置为`"Adobe"`。
* **`version`**：表示同意标准版本的字符串。 为Adobe 2.0标准将此属性设置为`"2.0"`。
* **`value`**：包含同意值的对象。
   * **`value.collect.val`**：同意值。 当用户选择加入时将此项设置为`"y"`，当用户选择退出时将此项设置为`"n"`。
   * **`value.metadata.time`**：用户上次更新其同意设置的时间戳。

```js
// Set consent using the Adobe 2.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "collect": {
        "val": "y"
      },
      "metadata": {
        "time": "YYYY-03-17T15:48:42-07:00"
      }
    }
  }]
});
```

>[!TAB IAB TCF 2.0]

### IAB TCF 2.0标准`consent`对象

要记录通过交互式Advertising Bureau Europe (IAB)透明度和同意框架(TCF)标准提供的用户同意首选项，请设置如下所示的同意字符串。

以这种方式设置同意后，Real-time Customer Profile将更新同意信息。 要使此功能正常工作，配置文件XDM架构需要包含[配置文件隐私架构字段组](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md)。 发送事件时，需要手动将IAB同意信息添加到事件XDM对象。 Web SDK不会自动在事件中包含同意信息。

要在事件中发送同意信息，您必须将体验事件隐私字段组添加到已启用[!DNL Profile]的[!DNL XDM ExperienceEvent]架构中。 有关如何配置此架构的步骤，请参阅数据集准备指南中有关[更新ExperienceEvent架构](../../landing/governance-privacy-security/consent/iab/dataset.md#event-schema)的部分。

* **`standard`**：您选择的同意标准。 对于IAB TCF 2.0标准，将此属性设置为`"IAB TCF"`。
* **`version`**：表示同意标准版本的字符串。 对于IAB TCF 2.0标准，将此属性设置为`"2.0"`。
* **`value`**：包含同意值的字符串。
* **`gdprApplies`**：一个布尔值，用于确定GDPR是否适用于此同意值。 其默认值为`true`。
* **`gdprContainsPersonalData`**：一个布尔值，用于确定与此用户关联的事件数据是否包含个人数据。 其默认值为`false`。

```js
// Set consent using the IAB TCF 2.0 standard
alloy("setConsent", {
  consent: [{
    "standard": "IAB TCF",
    "version": "2.0",
    "value": "CO052l-O052l-DGAMBFRACBgAIBAAAAABIYgEawAQEagAAAA",
    "gdprApplies": true,
    "gdprContainsPersonalData": true
  }]
});
```

>[!TAB Adobe 1.0]

### Adobe 1.0标准`consent`对象

* **`standard`**：您选择的同意标准。 为Adobe 1.0标准将此属性设置为`"Adobe"`。
* **`version`**：表示同意标准版本的字符串。 为Adobe 1.0标准将此属性设置为`"1.0"`。
* **`value.general`**：同意值。 当用户选择加入时将此项设置为`"in"`，当用户选择退出时将此项设置为`"out"`。

```js
// Set consent using the Adobe 1.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "1.0",
    "value": {
      "general": "in"
    }
  }]
});
```

>[!ENDTABS]

### 在一个请求中发送多个标准 {#multiple-standards}

Web SDK还支持在请求中发送多个同意对象，如下面的示例所示。

```js
alloy("setConsent", {
    consent: [{
        standard: "Adobe",
        version: "2.0",
        value: {
            collect: {
                val: "y"
            },
            metadata: {
                time: "2021-03-17T15:48:42-07:00"
            }
        }
    }, {
        standard: "IAB TCF",
        version: "2.0",
        value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
        gdprApplies: true
    }]
});
```

## 同意偏好设置的持久性 {#persistence}

使用`setConsent`命令向Web SDK传达用户偏好设置后，SDK会保留对Cookie的用户偏好设置。 下次用户在浏览器中加载您的网站时，Web SDK将检索并使用这些保留的首选项，确定是否可将事件发送到Adobe。

您需要单独存储用户偏好设置才能显示同意对话框以及当前偏好设置。 无法从Web SDK检索用户偏好设置。 为确保用户首选项与SDK保持同步，您可以在每次加载页面时调用`setConsent`命令。 只有在首选项发生更改时，Web SDK才会进行服务器调用。
