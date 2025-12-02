---
title: defaultconsent
description: 为Web属性设置默认同意收集方法。
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: 1e272eb18fac2f59f9737756d48947a25573d772
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 5%

---


# `defaultConsent`

`defaultConsent`属性确定在调用[`setConsent`](../setconsent.md)命令之前如何处理数据收集同意。 当您不希望意外从居住在数据收集之前需要获得同意的区域中的个人收集数据时，此属性很有价值。

如果您的访客不属于《通用数据保护条例》(GDPR)的管辖范围，则默认同意可以设置为`in`。 GDPR管辖区内的访客可以将默认同意设置为`pending`。 您的同意管理平台(CMP)可以检测客户的区域，并向IAB TCF 2.0提供标记`gdprApplies`。此标记可用于设置默认同意。

运行`defaultConsent`命令时，将`configure`字符串属性设置为所需的同意级别。 此属性区分大小写，并且仅支持以下三个值： `"in"`、`"out"`和`"pending"`。 如果尝试使用任何其他值，则库会引发错误。 如果未在`configure`命令中进行设置，则默认值为&#x200B;**`in`**。

>[!IMPORTANT]
>
>`defaultConsent`值在页面加载之间不持久。 确保每次调用`configure`命令时都设置所需的默认同意。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```

* **`in`**：数据收集正常运行，直到用户选择退出为止。
* **`out`**：数据将永久丢弃，直到用户选择加入为止。
* **`pending`**：数据存储在本地，直到用户使用[`setConsent`](../setconsent.md)命令选择加入为止。

>[!NOTE]
>
>尽管Adobe计划构建一组更强大的用途或类别，这些用途或类别与Adobe功能和产品相对应，但当前实施对于选择加入是一种“全有或全无”的方法。 此限制仅适用于Web SDK，而不适用于其他Adobe JavaScript库。

## 将`defaultConsent`与`setConsent`一起使用 {#using-consent}

Web SDK提供了两个互补的同意选项：

* `defaultConsent` （此页面）：确定默认同意首选项。
* [`setConsent`](../setconsent.md)：捕获访客的同意首选项。

如果同时使用这些设置，则可能会导致数据收集和Cookie设置结果有所不同，具体取决于其配置的值。

请参阅下表，根据同意设置了解何时进行数据收集以及何时设置Cookie。

| `defaultConsent` | `setConsent` | 发生数据收集 | Web SDK设置浏览器Cookie |
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

有关库设置的Cookie列表，请参阅[Adobe Experience Platform Web SDK Cookie](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk)。

>[!NOTE]
>
>即使访客选择退出跟踪，也会设置身份和同意Cookie。 这些Cookie是尊重其数据收集偏好所必需的。

## 基于`gdprApplies`设置默认同意

某些CMP提供了确定《通用数据保护条例》(GDPR)是否适用于客户的能力。 如果您希望客户同意不适用GDPR的情况，则可以在TCF API调用中使用`gdprApplies`标记。 例如：

```js
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

在上述代码块中，在从TCF API获取`configure`之后调用`tcData`命令。 如果`gdprApplies`为true，则默认同意设置为`pending`。 如果`gdprApplies`为false，则默认同意设置为`in`。 请确保使用您的配置填写`alloyConfiguration`变量。

## 使用Web SDK标记扩展的默认同意

请参阅Web SDK标记扩展文档中的[同意设置](/help/tags/extensions/client/web-sdk/configure/consent.md)，了解如何使用标记执行这些操作。
