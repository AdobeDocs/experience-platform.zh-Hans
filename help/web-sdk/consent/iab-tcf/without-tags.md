---
title: 使用Adobe Experience Platform Web SDK集成IAB TCF 2.0支持
description: 了解如何在不使用标记的情况下为您的网站设置IAB TCF 2.0支持。
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# 将IAB TCF 2.0支持与Experience Platform Web SDK集成

本指南演示了如何在不使用标记的情况下将Interactive Advertising Bureau Transparency &amp; Consent Framework版本2.0 (IAB TCF 2.0)与Adobe Experience Platform Web SDK集成。 有关与IAB TCF 2.0集成的概述，请阅读[概述](./overview.md)。 有关如何与标记集成的指南，请阅读标记的[IAB TCF 2.0指南](./with-tags.md)。

## 快速入门

本指南使用`__tcfapi`界面访问同意信息。 您可以更轻松地直接与云管理提供商(CMP)集成。 但是，本指南中的信息可能仍然有用，因为CMP通常提供与TCF API类似的功能。

>[!NOTE]
>
>这些示例假定在运行代码时，页面上定义了`window.__tcfapi`。 CMP可以提供挂接，您可以在`__tcfapi`对象就绪时运行这些函数。

要将包含标记的IAB TCF 2.0和Adobe Experience Platform Web SDK扩展结合使用，您需要具有可用的XDM架构。 如果尚未设置这两个中的任何一个选项，请先查看此页面，然后再继续。

此外，本指南要求您实际了解Adobe Experience Platform Web SDK。 如需快速刷新，请阅读[Adobe Experience Platform Web SDK概述](../../home.md)和[常见问题解答](../../faq.md)文档。

## 启用默认同意

如果要对所有未知用户一视同仁，可将[`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md)设置为`pending`或`out`。 在收到同意首选项之前，这将排队或丢弃体验事件。

### 根据`gdprApplies`设置默认同意

某些CMP提供了确定《通用数据保护条例》(GDPR)是否适用于客户的能力。 如果您希望客户同意不适用GDPR的情况，则可以在TCF API调用中使用`gdprApplies`标记。

以下示例显示了执行此操作的一种方法：

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

在此示例中，在从TCF API获取`tcData`之后调用`configure`命令。 如果`gdprApplies`为true，则默认同意设置为`pending`。 如果`gdprApplies`为false，则默认同意设置为`in`。 请确保使用您的配置填写`alloyConfiguration`变量。

>[!NOTE]
>
>当默认同意设置为`in`时，`setConsent`命令仍可用于记录您的客户同意首选项。

## 使用setConsent事件

IAB TCF 2.0 API为客户更新同意时提供了一个事件。 当客户最初设置其首选项以及更新其首选项时，会发生这种情况。

以下示例显示了执行此操作的一种方法：

```javascript
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

此代码块侦听`useractioncomplete`事件，然后设置同意，传递同意字符串和`gdprApplies`标记。 如果您有客户的自定义标识，请务必填写`identityMap`变量。 有关详细信息，请参阅[setConsent](../../../web-sdk/commands/setconsent.md)指南。

## 在sendEvent中包含同意信息

在XDM架构中，您可以存储来自体验事件的同意偏好设置信息。 可通过两种方式将此信息添加到每个事件。

首先，您可以在每`sendEvent`次调用中提供相关的XDM架构。 以下示例显示了执行此操作的一种方法：

```javascript
var sendEventOptions = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    sendEventOptions.xdm.consentStrings = [{
      consentStandard: "IAB TCF"
      consentStandardVersion: "2.0"
      consentStringValue: tcData.tcString,
      gdprApplies: tcData.gdprApplies
    }];
    window.alloy("sendEvent", sendEventOptions);
  }
});
```

此示例获取TCF API的同意信息，然后发送一个事件，其中包含添加到XDM架构的同意信息。

向每个请求添加同意信息的另一种方法是使用[`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md)回调。

## 后续步骤

现在，您已了解如何将IAB TCF 2.0与Experience Platform Web SDK扩展一起使用，您还可以选择与其他Adobe解决方案(如Adobe Analytics或Adobe Real-Time Customer Data Platform)集成。 有关详细信息，请参阅[IAB透明度和同意框架2.0概述](./overview.md)。
