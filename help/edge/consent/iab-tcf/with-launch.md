---
title: 使用标记和平台Web SDK扩展集成IAB TCF 2.0支持
description: 了解如何使用标记和Adobe Experience Platform Web SDK扩展设置IAB TCF 2.0同意。
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---

# 使用标记和Platform Web SDK扩展集成IAB TCF 2.0支持

Adobe Experience Platform Web SDK支持交互式广告局透明度与同意框架版本2.0(IAB TCF 2.0)。 本指南将向您演示如何设置标记属性，以便使用Adobe Experience Platform Web SDK标记扩展将IAB TCF 2.0同意信息发送到Adobe。

如果您不希望使用标记，请参阅 [在不使用标记的情况下使用IAB TCF 2.0](./without-launch.md).

## 快速入门

要将IAB TCF 2.0与标记和Platform Web SDK扩展一起使用，您需要具有可用的XDM架构和数据集。

此外，本指南还要求您对Adobe Experience Platform Web SDK有一定的了解。 如需快速刷新，请阅读 [Adobe Experience Platform Web SDK概述](../../home.md) 和 [常见问题解答](../../web-sdk-faq.md) 文档。

## 设置默认同意

在扩展配置中，有一个默认同意设置。 这可控制没有同意Cookie的客户的行为。 如果要为没有同意Cookie的客户排入体验事件队列，请将其设置为 `pending`. 如果要为没有同意Cookie的客户放弃体验事件，请将其设置为 `out`. 您还可以使用数据元素动态设置默认同意值。

有关如何配置默认同意的更多信息，请参阅 [默认同意部分](../../fundamentals/configuring-the-sdk.md#default-consent) （在SDK配置指南中）。

## 使用同意信息更新用户档案 {#consent-code-1}

调用 `setConsent` 当客户同意首选项发生更改时，您需要创建新的标记规则。 首先添加新事件，然后选择核心扩展的“Custom Code”事件类型。

为新事件使用以下代码示例：

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

此自定义代码可执行两项操作：

* 设置两个数据元素，一个包含同意字符串，另一个包含 `gdprApplies` 标记。 这在以后填写“设置同意”操作时非常有用。

* 在同意首选项发生更改时触发规则。 每当同意首选项发生更改时，应使用“设置同意”操作。 在扩展中添加“Set Consent”操作，并按如下方式填写表单：

* 标准：&quot;IAB TCF&quot;
* 版本：&quot;2.0&quot;
* 值：&quot;%IAB TCF同意字符串%&quot;
* GDPR适用：&quot;%IAB TCF同意GDPR%&quot;

![IAB设置同意操作](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>您无法使用数据元素选择器选择这些数据元素，因为它们是通过自定义代码创建的。 您必须在数据元素名称中键入百分比符号。 此代码会在客户发生更改时使用其新同意首选项来更新其配置文件。 此外，服务器会返回一个Cookie值，这可能会阻止Adobe Experience Platform Web SDK记录体验事件。

## 为体验事件创建XDM数据元素

同意字符串应包含在XDM体验事件中。 要实现此目的，请使用XDM对象数据元素。 首先，创建新的XDM对象数据元素，或者使用已创建的数据元素来发送事件。 如果您已将体验事件隐私架构字段组添加到架构，则您应该具有 `consentStrings` 键。

1. 选择 **[!UICONTROL consentStrings]**.

1. 选择 **[!UICONTROL 提供单个项目]** 选择 **[!UICONTROL 添加项目]**.

1. 展开 **[!UICONTROL consentString]** ，然后展开第一个项目，然后填写以下值：

* `consentStandard`:IAB TCF
* `consentStandardVersion`:2.0
* `consentStringValue`:%IAB TCF同意字符串%
* `gdprApplies`:%IAB TCF同意GDPR%

>[!IMPORTANT]
>
>您无法使用数据元素选择器选择这些数据元素，因为它们是通过自定义代码创建的。 您必须在数据元素名称中键入百分比符号。

## 发送包含IAB TCF 2.0同意信息的初始体验事件

如果页面上的初始体验事件是通过页面加载事件触发的，则可能尚未加载同意字符串。 此规则旨在替换您当前的页面加载事件。 要确保先加载同意信息，请创建新规则，并将以下代码添加为自定义代码事件：

```javascript
// Wait for window.__tcfapi to be defined, then trigger when there is a consent string
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF GDPR Applies", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn"t defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

此代码与之前的自定义代码相同，不同之处在于 `useractioncomplete` 和 `tcloaded` 事件会得到处理。 的 [上一个自定义代码](#consent-code-1) 仅当客户首次选择首选项时才会触发。 当客户已选择其首选项时，也会触发此代码。 例如，第二次加载页面时。

从Platform Web SDK扩展添加“发送事件”操作。 在XDM字段中，选择在上一部分中创建的XDM数据元素。

## 使用IAB TCF 2.0同意信息发送其他事件

当事件在初始体验事件后触发时，仍然会定义这两个数据元素，可用于发送IAB同意信息。 使用相同的XDM数据元素发送将来的事件。 包含IAB TCF 2.0信息。

## 后续步骤

现在，您已经学会如何将IAB TCF 2.0与Platform Web SDK扩展一起使用，接下来您还可以选择与其他Adobe解决方案(如Adobe Analytics或实时客户数据平台)集成。 请参阅 [IAB透明度与同意框架2.0概述](./overview.md) 以了解更多信息。
