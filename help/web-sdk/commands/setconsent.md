---
title: setConsent
description: 用于每个页面，以跟踪用户的同意首选项。
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: d3591053939147589dae24e1e4c20d53b1f87dd3
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 2%

---


# `setConsent`

此 `setConsent` 命令告知Web SDK是应发送数据（选择启用）、丢弃数据（选择禁用）还是使用 [`defaultConsent`](configure/defaultconsent.md) （同意未知）。

Web SDK支持以下标准：

* **[Adobe标准](/help/landing/governance-privacy-security/consent/adobe/overview.md)**：同时支持1.0和2.0标准。
* **[IAB透明度和同意框架](/help/landing/governance-privacy-security/consent/iab/overview.md)**：如果您使用此标准，并且在您的实施配置正确的情况下，访客的Real-time Customer Profile将会更新为同意信息：
   1. XDM个人资料架构包含 [IAB TCF 2.0同意字段组](/help/xdm/field-groups/profile/iab.md).
   1. 体验事件架构包含 [IAB TCF 2.0同意字段组](/help/xdm/field-groups/event/iab.md).
   1. 在事件中包含IAB同意信息 [XDM对象](sendevent/xdm.md). 在发送事件数据时，Web SDK不会自动包含同意信息。

使用此命令后，Web SDK会将用户的首选项写入Cookie。 下次用户在浏览器中加载您的网站时，SDK将检索这些保留的首选项，以确定是否可将事件发送到Adobe。

Adobe建议您将任何同意对话框首选项与Web SDK同意分开存储。 Web SDK不提供检索同意的方法。 要确保用户首选项与SDK保持同步，您可以调用 `setConsent` 命令进行加载。 Web SDK仅在同意更改时进行服务器调用。

## 使用 `defaultConsent` 与 `setConsent` {#using-consent}

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
| **AMCV_###@AdobeOrg** | 34128000（395天） | 前提条件 [`idMigrationEnabled`](configure/idmigrationenabled.md) 已启用。 当站点的某些部分仍在使用时，在过渡到Web SDK时非常有用 `visitor.js`. |
| **Demdex Cookie** | 15552000（180天） | 如果启用了ID同步，则会显示。 Audience Manager通过设置此Cookie来向网站访客分配唯一ID。 demdex Cookie可帮助Audience Manger执行基本的功能，例如访客识别、ID同步、分段、建模和报告等。 |
| **kndctr_orgid_cluster** | 1800（30分钟） | 存储为当前Edge Network提供请求的请求区域。 URL路径中使用区域，以便Edge Network能够将请求路由到正确的区域。 如果用户使用不同的IP地址或以不同的会话连接，则请求将再次路由到最近的区域。 |
| **kndct_orgid_identity** | 34128000（395天） | 存储ECID以及与ECID相关的其他信息。 |
| **kndctr_orgid_consent** | 15552000（180天） | 存储网站的用户同意首选项。 |
| **s_ecid** | 63115200（2年） | 包含Experience CloudID的副本([!DNL ECID])或MID。 MID 存储在一个键值对中，它遵循以下语法：`s_ecid=MCMID\|<ECID>`。 |

## 使用Web SDK标记扩展设置同意

在Adobe Experience Platform数据收集标记界面中，将同意设置作为规则中的一项操作。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 规则]**，然后选择所需的规则。
1. 下 [!UICONTROL 操作]，选择现有操作或创建操作。
1. 设置 [!UICONTROL 扩展名] 下拉字段至 **[!UICONTROL Adobe Experience Platform Web SDK]**，并设置 [!UICONTROL 操作类型] 到 **[!UICONTROL 设置同意]**.
1. 在右侧设置所需字段，包括 **[!UICONTROL 标准]** 和 **[!UICONTROL 一般同意]**.
1. 单击 **[!UICONTROL 保留更改]**，然后运行发布工作流程。

您可以在此操作中包含多个同意对象。

## 使用Web SDK JavaScript库设置同意

运行 `setConsent` 命令。 您可以在此命令中包含以下对象：

* **`consent[]`**：数组 `consent` 对象。 同意对象的格式有所不同，具体取决于您选择的标准和版本。 有关每个同意对象的示例，请参见下面的选项卡，具体取决于同意标准。
* **`identityMap`**：一个对象，可控制如何生成ECID以及同意信息绑定到哪些ID。 Adobe建议在以下情况下包含此对象： `setConsent` 在其他命令之前运行，例如 [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**：包含 [数据流配置覆盖](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe2.0]

### Adobe2.0标准 `consent` 对象

如果您使用的是Adobe Experience Platform，则需要在配置文件架构中包含隐私架构字段组。 请参阅 [Adobe Experience Platform中的治理、隐私和安全性](../../landing/governance-privacy-security/overview.md) 以了解有关Adobe2.0标准的更多信息。 您可以在对应于以下架构的值对象中添加数据 `consents` 字段 [!UICONTROL 同意和偏好设置] 配置文件字段组。

* **`standard`**：您选择的同意标准。 将此属性设置为 `"Adobe"` 用于Adobe2.0标准。
* **`version`**：表示同意标准版本的字符串。 将此属性设置为 `"2.0"` 用于Adobe2.0标准。
* **`value`**：包含同意值的对象。
   * **`value.collect.val`**：同意值。 将此项设置为 `"y"` 用户选择启用并启用 `"n"` 用户选择退出时。
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

### IAB TCF 2.0标准 `consent` 对象

要记录通过欧洲互动广告局(IAB)透明度和同意框架(TCF)标准提供的用户同意首选项，请设置如下所示的同意字符串。

以这种方式设置同意后，Real-time Customer Profile将更新同意信息。 要使此功能正常工作，配置文件XDM架构需要包含 [配置文件隐私架构字段组](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). 发送事件时，需要手动将IAB同意信息添加到事件XDM对象。 Web SDK不会自动在事件中包含同意信息。

要在事件中发送同意信息，您必须将体验事件隐私字段组添加到 [!DNL Profile] — 启用 [!DNL XDM ExperienceEvent] 架构。 请参阅以下部分 [更新ExperienceEvent架构](../../landing/governance-privacy-security/consent/iab/dataset.md#event-schema) ，以了解如何配置此功能的步骤。

* **`standard`**：您选择的同意标准。 将此属性设置为 `"IAB TCF"` 适用于IAB TCF 2.0标准。
* **`version`**：表示同意标准版本的字符串。 将此属性设置为 `"2.0"` 适用于IAB TCF 2.0标准。
* **`value`**：包含同意值的字符串。
* **`gdprApplies`**：一个布尔值，用于确定GDPR是否适用于此同意值。 其默认值为 `true`.
* **`gdprContainsPersonalData`**：一个布尔值，用于确定与此用户关联的事件数据是否包含个人数据。 其默认值为 `false`.

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

>[!TAB Adobe1.0]

### Adobe1.0标准 `consent` 对象

* **`standard`**：您选择的同意标准。 将此属性设置为 `"Adobe"` 对于Adobe1.0标准。
* **`version`**：表示同意标准版本的字符串。 将此属性设置为 `"1.0"` 对于Adobe1.0标准。
* **`value.general`**：同意值。 将此项设置为 `"in"` 用户选择启用并启用 `"out"` 用户选择退出时。

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

在使用向Web SDK传达用户偏好设置后， `setConsent` 命令时，SDK会保留用户对Cookie的偏好设置。 下次用户在浏览器中加载您的网站时，Web SDK将检索并使用这些保留的首选项来确定是否可将事件发送到Adobe。

您需要单独存储用户偏好设置才能显示同意对话框以及当前偏好设置。 无法从Web SDK检索用户偏好设置。 要确保用户首选项与SDK保持同步，您可以调用 `setConsent` 命令进行加载。 只有在首选项发生更改时，Web SDK才会进行服务器调用。

## 在设置同意时同步身份 {#sync-identities}

当默认同意(通过 [defaultconsent](configure/defaultconsent.md) parameter)设置为 `pending` 或 `out`， `setConsent` 设置可能是第一个发出并建立身份的请求。 因此，在第一个请求上同步身份可能很重要。 您可以将标识映射添加到 `setConsent` 命令，就像在 `sendEvent` 命令。 请参阅 [使用identitymap](../identity/overview.md#using-identitymap) 有关如何在命令中包含标识映射的示例。
