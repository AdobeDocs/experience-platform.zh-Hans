---
title: setConsent
description: 用于跟踪每个页面上的用户同意。
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 1%

---

# setConsent

此 `setConsent` 命令告知Web SDK是应发送数据（选择启用）、丢弃数据（选择禁用）还是使用 [`defaultConsent`](configure/defaultconsent.md) （同意未知）。

Web SDK支持以下标准：

* **[Adobe标准](/help/landing/governance-privacy-security/consent/adobe/overview.md)**：同时支持1.0和2.0标准。
* **[IAB透明度和同意框架](/help/landing/governance-privacy-security/consent/iab/overview.md)**：如果您使用此标准，并且在您的实施配置正确的情况下，访客的Real-time Customer Profile将会更新为同意信息：
   1. XDM个人资料架构包含 [IAB TCF 2.0同意字段组](/help/xdm/field-groups/profile/iab.md).
   1. 体验事件架构包含 [IAB TCF 2.0同意字段组](/help/xdm/field-groups/event/iab.md).
   1. 在事件中包含IAB同意信息 [XDM对象](sendevent/xdm.md). 在发送事件数据时，Web SDK不会自动包含同意信息。

使用此命令后，Web SDK会将用户的首选项写入Cookie。 下次用户在浏览器中加载您的网站时，SDK将检索这些保留的首选项，以确定是否可将事件发送到Adobe。

Adobe建议您将任何同意对话框首选项与Web SDK同意分开存储。 Web SDK不提供检索同意的方法。 要确保用户首选项与SDK保持同步，您可以调用 `setConsent` 命令进行加载。 Web SDK仅在同意更改时进行服务器调用。

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

* **`consent[]`**：数组 `consent` 对象。 同意对象的格式有所不同，具体取决于您选择的标准和版本。
* **`identityMap`**：一个对象，可控制如何生成ECID以及同意信息绑定到哪些ID。 Adobe建议在以下情况下包含此对象： `setConsent` 在其他命令之前运行，例如 [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**：包含 [数据流配置覆盖](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe2.0]

### Adobe2.0标准 `consent` 对象

* **`standard`**：您选择的同意标准。 将此属性设置为 `"Adobe"` 用于Adobe2.0标准。
* **`version`**：表示同意标准版本的字符串。 将此属性设置为 `"2.0"` 用于Adobe2.0标准。
* **`value`**：包含同意值的对象。
   * **`value.collect.val`**：同意值。 有效值为 `"y"` （选择启用）和 `"n"` （选择禁用）。
   * **`value.metadata.time`**：用户设置同意值的时间戳。

```js
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

* **`standard`**：您选择的同意标准。 将此属性设置为 `"IAB TCF"` 适用于IAB TCF 2.0标准。
* **`version`**：表示同意标准版本的字符串。 将此属性设置为 `"2.0"` 适用于IAB TCF 2.0标准。
* **`value`**：包含同意值的字符串。
* **`gdprApplies`**：一个布尔值，用于确定GDPR是否适用于此同意值。 其默认值为 `true`。
* **`gdprContainsPersonalData`**：一个布尔值，用于确定与此用户关联的事件数据是否包含个人数据。 其默认值为 `false`。

```js
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
* **`value.general`**：同意值。 有效值为 `"in"` （选择启用）和 `"out"` （选择禁用）。

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
