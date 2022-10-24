---
title: 使用Adobe Experience Platform Web SDK集成IAB TCF 2.0支持
description: 了解如何在不使用标记的情况下为网站设置IAB TCF 2.0支持。
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# 将IAB TCF 2.0支持与平台Web SDK集成

本指南演示了如何在不使用标记的情况下，将交互式广告局透明度与同意框架版本2.0(IAB TCF 2.0)与Adobe Experience Platform Web SDK集成。 有关与IAB TCF 2.0集成的概述，请阅读 [概述](./overview.md). 有关如何与标记集成的指南，请阅读 [适用于标记的IAB TCF 2.0指南](./with-launch.md).

## 快速入门

本指南使用 `__tcfapi` 用于访问同意信息的界面。 直接与云管理提供程序(CMP)集成可能会比较容易。 但是，本指南中的信息可能仍然有用，因为CMP通常提供与TCF API类似的功能。

>[!NOTE]
>
>以下示例假定在运行代码时， `window.__tcfapi` 在页面上定义。 CMP可以提供一个挂接，在 `__tcfapi` 对象已准备就绪。

要将IAB TCF 2.0与标记和Adobe Experience Platform Web SDK扩展一起使用，您需要提供XDM模式。 如果尚未设置其中任一设置，请先查看此页面，然后再继续。

此外，本指南还要求您对Adobe Experience Platform Web SDK有一定的了解。 如需快速刷新，请阅读 [Adobe Experience Platform Web SDK概述](../../home.md) 和 [常见问题解答](../../web-sdk-faq.md) 文档。

## 启用默认同意

如果您希望对所有未知用户都一视同仁，可以将默认同意设置为 `pending` 或 `out`. 在收到同意首选项之前，会将体验事件排入队列或丢弃该事件。

有关默认同意的更多信息，请参阅 [默认同意部分](../../fundamentals/configuring-the-sdk.md#default-consent) 平台Web SDK配置文档中的。

### 根据 `gdprApplies`

某些CMP提供了确定《通用数据保护条例》(GDPR)是否适用于客户的功能。 如果您希望在客户同意不适用GDPR的情况下，可以使用 `gdprApplies` TCF API调用中的标记。

以下示例显示了一种实现此目的的方法：

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

在本例中， `configure` 命令在 `tcData` 从TCF API获取。 如果 `gdprApplies` 为true，则默认同意设置为 `pending`. 如果 `gdprApplies` 为false，则默认同意设置为 `in`. 请务必填写 `alloyConfiguration` 变量。

>[!NOTE]
>
>默认同意设置为 `in`, `setConsent` 命令仍可用于记录客户同意首选项。

## 使用setConsent事件

IAB TCF 2.0 API为客户更新同意时提供事件。 这发生在客户最初设置其首选项以及客户更新其首选项时。

以下示例显示了一种实现此目的的方法：

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

此代码块侦听 `useractioncomplete` 事件，然后设置同意，并传递同意字符串和 `gdprApplies` 标记。 如果您有客户的自定义身份，请务必填写 `identityMap` 变量。 请参阅 [支持同意](../../consent/supporting-consent.md) 有关调用的更多信息 `setConsent`.

## 在sendEvent中包含同意信息

在XDM架构中，您可以存储体验事件中的同意首选项信息。 可通过两种方式将此信息添加到每个事件。

首先，您可以在每个 `sendEvent` 呼叫。 以下示例显示了一种实现此目的的方法：

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

此示例将获取TCF API的同意信息，然后发送一个事件，其中包含添加到XDM架构的同意信息。 请参阅 [跟踪事件](../../fundamentals/tracking-events.md) 以了解 `sendEvent` 命令选项。

向每个请求添加同意信息的另一种方式是使用 `onBeforeEventSend` 回调。 阅读 [全局修改事件](../../fundamentals/tracking-events.md#modifying-events-globally) ，以了解有关如何执行此操作的更多信息。

## 后续步骤

现在，您已经学会如何将IAB TCF 2.0与Platform Web SDK扩展一起使用，接下来您还可以选择与其他Adobe解决方案(如Adobe Analytics或Adobe Real-time Customer Data Platform)集成。 请参阅 [IAB透明度与同意框架2.0概述](./overview.md) 以了解更多信息。
