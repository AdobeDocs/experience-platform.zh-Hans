---
title: 使用IAB TCF 2.0而无Experience Platform Launch
seo-title: 设置与Adobe Experience PlatformWeb SDK的IAB TCF 2.0同意
description: 了解如何设置IAB TCF 2.0与Adobe Experience PlatformWeb SDK的同意
seo-description: 了解如何设置IAB TCF 2.0与Adobe Experience PlatformWeb SDK的同意
translation-type: tm+mt
source-git-commit: db742119d8f169817080f1fd4e0dc08a0f0faa47
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---


# 将IAB TCF 2.0与Adobe Experience PlatformWeb SDK扩展一起使用

本指南说明如何在不使用Experience Platform Launch的情况下将交互式广告局透明度和同意框架2.0版(IAB TCF 2.0)与Adobe Experience PlatformWeb SDK集成。 有关与IAB TCF 2.0集成的概述，请阅读 [概述](./overview.md)。 有关如何与Experience Platform Launch集成的指南，请阅 [读IAB TCF 2.0Experience Platform Launch指南](./with-launch.md)。

## 入门指南

本指南使用该 `__tcfapi` 界面访问同意信息。 您可能更容易直接与云管理提供商(CMP)集成。 但是，本指南中的信息可能仍然有用，因为CMP通常提供与TCF API类似的功能。

>[!NOTE]
>
>这些示例假定在运行代码时在页 `window.__tcfapi` 面上定义该代码。 CMP可以提供一个挂接，在对象准备就绪时，您可以在该挂 `__tcfapi` 接处运行这些函数。

要将IAB TCF 2.0与Experience Platform Launch及AEP Web SDK扩展一起使用，您需要提供XDM模式。 如果尚未设置其中任何一个，请在继续操作之前查看此页面进行开始。

此外，本指南要求您对Adobe Experience PlatformWeb SDK有有效的了解。 要获得快速复习资料，请阅读 [Adobe Experience PlatformWeb SDK概述](../../home.md)[和常见问题解答文档](../../web-sdk-faq.md) 。

## 启用默认同意

如果要对所有未知用户一视同仁，可以将默认同意设置为 `pending`。 此队列在收到同意首选项之前为体验事件排队。

有关默认同意的详细信息，请参 [阅Platform Web SDK配置文](../../fundamentals/configuring-the-sdk.md#default-consent) 档中的默认同意部分。

### 根据 `gdprApplies`

某些CMP提供确定一般数据保护规定(GDPR)是否适用于客户的能力。 如果您想要为不适用GDPR的客户征得同意，可以在TCF API调 `gdprApplies` 用中使用该标志。

以下示例演示了实现此操作的一种方法：

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

在此示例中， `configure` 从TCF API获 `tcData` 取命令后调用该命令。 如果 `gdprApplies` 为真，则默认同意设置为 `pending`。 如果 `gdprApplies` 为false，则默认同意设置为 `in`。 请务必用配置 `alloyConfiguration` 填写变量。

>[!NOTE]
>
>当默认同意设置为 `in`时， `setConsent` 该命令仍可用于记录客户同意偏好。

## 使用setConnence事件

IAB TCF 2.0 API为客户更新同意时提供事件。 当客户初始设置其偏好和更新其偏好时，会发生这种情况。

以下示例演示了实现此操作的一种方法：

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

此代码块监听 `useractioncomplete` 事件，然后设置同意，传递同意字符串和标 `gdprApplies` 志。 如果您有客户的自定义身份，请务必填写该变 `identityMap` 量。 有关呼叫的详细信 [息，请参](../../consent/supporting-consent.md) 阅支持同意指南 `setConsent`。

## 在sendEvent中包括同意信息

在XDM模式中，您可以存储体验事件的同意偏好信息。 有两种方法可将此信息添加到每个事件。

首先，您可以在每次呼叫时提供相关的XDM `sendEvent` 模式。 以下示例演示了实现此操作的一种方法：

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

此示例获取TCF API的同意信息，然后发送事件并添加同意信息到XDM模式。 请参 [阅跟踪事件](../../fundamentals/tracking-events.md) 指南，了解命令选项中应包含 `sendEvent` 的内容。

向每个请求添加同意信息的另一种方法是使用回 `onBeforeEventSend` 调。 有关如何执行此操 [作的详细信息](../../fundamentals/tracking-events.md#modifying-events-globally) ，请阅读跟踪事件文档中有关全局修改事件的部分。

## 后续步骤

既然您已经学习了如何将IAB TCF 2.0与Adobe Experience PlatformWeb SDK扩展一起使用，您还可以选择与其他Adobe解决方案(如Adobe Analytics或实时客户数据平台)集成。 有关更 [多信息，请参阅IAB透明度和同意框架](./overview.md) 2.0概述。
