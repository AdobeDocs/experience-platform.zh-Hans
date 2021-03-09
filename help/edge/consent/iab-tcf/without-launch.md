---
title: 使用Adobe Experience Platform Web SDK集成IAB TCF 2.0支持
description: 了解如何在不使用Adobe Experience Platform Launch的情况下为您的网站设置IAB TCF 2.0支持。
seo-description: 了解如何设置Adobe Experience Platform Web SDK的IAB TCF 2.0同意
translation-type: tm+mt
source-git-commit: b9fb71ac7eca95c65165d6780b681ada3f16325b
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# 将IAB TCF 2.0支持与Platform Web SDK集成

本指南说明如何在不使用Experience Platform Launch的情况下将Interactive Advertising Bureau透明度和同意框架版本2.0(IAB TCF 2.0)与Adobe Experience Platform Web SDK集成。 有关与IAB TCF 2.0集成的概述，请阅读[概述](./overview.md)。 有关如何与Experience Platform Launch集成的指南，请阅读[IAB TCF 2.0指南，该指南适用于Experience Platform Launch](./with-launch.md)。

## 入门指南

本指南使用`__tcfapi`接口访问同意信息。 您可以更轻松地直接与云管理提供商(CMP)集成。 但是，本指南中的信息可能仍然有用，因为CMP通常提供与TCF API类似的功能。

>[!NOTE]
>
>这些示例假定在运行代码时，`window.__tcfapi`已在页面上定义。 CMP可以提供一个挂接，在`__tcfapi`对象准备就绪时，您可以在该挂接中运行这些函数。

要将IAB TCF 2.0与Experience Platform Launch和Adobe Experience Platform Web SDK扩展一起使用，您需要提供XDM模式。 如果尚未设置其中任一设置，请在继续之前查看此页面进行开始。

此外，本指南要求您对Adobe Experience Platform Web SDK有正确的了解。 有关快速复习，请阅读[Adobe Experience Platform Web SDK概述](../../home.md)和[常见问题解答](../../web-sdk-faq.md)文档。

## 启用默认同意

如果要对所有未知用户一视同仁，可以将默认同意设置为`pending`或`out`。 在收到同意首选项之前，此队列或放弃体验事件。

有关默认同意的详细信息，请参阅Platform Web SDK配置文档中的[默认同意部分](../../fundamentals/configuring-the-sdk.md#default-consent)。

### 根据`gdprApplies`设置默认同意

某些CMP提供确定一般数据保护规定(GDPR)是否适用于客户的能力。 如果您希望在GDPR不适用的客户中获得同意，则可以在TCF API调用中使用`gdprApplies`标志。

下面的示例说明了执行此操作的一种方法：

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

在此示例中，从TCF API获取`tcData`后，将调用`configure`命令。 如果`gdprApplies`为true，则默认同意设置为`pending`。 如果`gdprApplies`为false，则默认同意设置为`in`。 请务必使用您的配置填写`alloyConfiguration`变量。

>[!NOTE]
>
>当默认同意设置为`in`时，`setConsent`命令仍可用于记录您的客户同意偏好。

## 使用setConnence事件

IAB TCF 2.0 API为客户何时更新同意提供事件。 这发生在客户最初设置其偏好和更新其偏好时。

下面的示例说明了执行此操作的一种方法：

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

此代码块监听`useractioncomplete`事件，然后设置同意，通过同意字符串和`gdprApplies`标志。 如果您有客户的自定义身份，请务必填写`identityMap`变量。 有关调用`setConsent`的详细信息，请参阅[支持同意](../../consent/supporting-consent.md)的指南。

## 在sendEvent中包括同意信息

在XDM模式中，您可以存储体验事件的同意首选项信息。 有两种方法可将此信息添加到每个事件。

首先，您可以在每次`sendEvent`调用时提供相关的XDM模式。 下面的示例说明了执行此操作的一种方法：

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

此示例获取TCF API的同意信息，然后发送一个事件，其中包含添加到XDM模式的同意信息。 请参阅[跟踪事件](../../fundamentals/tracking-events.md)指南，了解`sendEvent`命令选项中应包含的内容。

向每个请求添加同意信息的另一种方法是使用`onBeforeEventSend`回调。 有关如何执行此操作的详细信息，请阅读跟踪事件文档中关于[全局修改事件](../../fundamentals/tracking-events.md#modifying-events-globally)的部分。

## 后续步骤

现在，您已学习如何将IAB TCF 2.0与Platform Web SDK扩展一起使用，您还可以选择与其他Adobe解决方案(如Adobe Analytics或实时客户数据平台)集成。 有关详细信息，请参阅[IAB透明度和同意框架2.0概述](./overview.md)。
