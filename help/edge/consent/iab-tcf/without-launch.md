---
title: 使用Adobe Experience Platform Web SDK集成IAB TCF 2.0支持
description: 了解如何在不使用标记的情况下为您的网站设置IAB TCF 2.0支持。
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# 将IAB TCF 2.0支持与平台Web SDK集成

本指南演示了如何在不使用标记的情况下将Interactive Advertising Bureau Transparency &amp; Consent Framework版本2.0 (IAB TCF 2.0)与Adobe Experience Platform Web SDK集成。 有关与IAB TCF 2.0集成的概述，请阅读 [概述](./overview.md). 有关如何与标记集成的指南，请阅读 [IAB TCF 2.0标记指南](./with-launch.md).

## 快速入门

本指南使用 `__tcfapi` 用于访问同意信息的界面。 您可以更轻松地直接与云管理提供程序(CMP)集成。 但是，本指南中的信息可能仍然有用，因为CMP通常提供与TCF API类似的功能。

>[!NOTE]
>
>这些示例假定在运行代码时， `window.__tcfapi` 在页面上定义。 CMP可以提供挂接，您可以在挂接时运行这些函数。 `__tcfapi` 对象已就绪。

要将IAB TCF 2.0与标记和Adobe Experience Platform Web SDK扩展结合使用，您需要具有可用的XDM架构。 如果尚未设置这两个选项中的任意一个，请先查看此页面再继续。

此外，本指南还要求您实际了解Adobe Experience Platform Web SDK。 如需快速复习，请阅读 [Adobe Experience Platform Web SDK概述](../../home.md) 和 [常见问题解答](../../web-sdk-faq.md) 文档。

## 启用默认同意

如果要对所有未知用户一视同仁，可将默认同意设置为 `pending` 或 `out`. 在收到同意首选项之前，这会队列或丢弃体验事件。

有关默认同意的更多信息，请参阅 [默认同意部分](../../fundamentals/configuring-the-sdk.md#default-consent) （位于Platform Web SDK配置文档中）。

### 根据以下条件设置默认同意 `gdprApplies`

某些CMP提供了确定《通用数据保护条例》(GDPR)是否适用于客户的能力。 如果您希望客户同意GDPR不适用的情况，则可以使用 `gdprApplies` TCF API调用中的标记。

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

在此示例中， `configure` 命令是在以下命令之后调用： `tcData` 从TCF API获取。 如果 `gdprApplies` 为true，则默认同意设置为 `pending`. 如果 `gdprApplies` 为false，默认同意设置为 `in`. 请务必填写 `alloyConfiguration` 变量填充您的配置。

>[!NOTE]
>
>当默认同意设置为 `in`，则 `setConsent` 命令仍可用于记录客户的同意首选项。

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

此代码块监听 `useractioncomplete` 事件，然后设置同意，传递同意字符串和 `gdprApplies` 标志。 如果您有客户的自定义标识，请务必填写 `identityMap` 变量。 请参阅指南，网址为 [支持同意](../../consent/supporting-consent.md) 有关调用的详细信息 `setConsent`.

## 在sendEvent中包含同意信息

在XDM架构中，您可以存储来自体验事件的同意首选项信息。 可通过两种方式将此信息添加到每个事件。

首先，您可以在每 `sendEvent` 呼叫。 以下示例显示了执行此操作的一种方法：

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

此示例获取TCF API的同意信息，然后发送一个事件，其中包含添加到XDM架构的同意信息。 请参阅 [跟踪事件](../../fundamentals/tracking-events.md) 指南以了解应包含的内容 `sendEvent` 命令选项。

将同意信息添加到每个请求的另一种方法是使用 `onBeforeEventSend` 回调。 阅读以下章节： [全局修改事件](../../fundamentals/tracking-events.md#modifying-events-globally) 从跟踪事件文档中获取有关如何执行此操作的更多信息。

## 后续步骤

现在，您已了解如何将IAB TCF 2.0与Platform Web SDK扩展结合使用，您还可以选择与其他Adobe解决方案(如Adobe Analytics或Adobe Real-time Customer Data Platform)集成。 请参阅 [IAB透明度和同意框架2.0概述](./overview.md) 了解更多信息。
