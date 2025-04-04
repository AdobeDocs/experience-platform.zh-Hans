---
title: 使用标记和Experience Platform Web SDK扩展集成IAB TCF 2.0支持
description: 了解如何使用标记和Adobe Experience Platform Web SDK扩展设置IAB TCF 2.0同意。
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---

# 使用标记和Experience Platform Web SDK扩展集成IAB TCF 2.0支持

Adobe Experience Platform Web SDK支持交互式Advertising Bureau Transparency &amp; Consent Framework版本2.0 (IAB TCF 2.0)。 本指南向您展示了如何使用Adobe Experience Platform Web SDK标记扩展设置标记属性，以将IAB TCF 2.0同意信息发送到Adobe。

如果您不想使用标记，请参阅关于使用[不带标记的IAB TCF 2.0的指南](./without-tags.md)。

## 快速入门

要将包含标记的IAB TCF 2.0和Experience Platform Web SDK扩展结合使用，您需要具有XDM架构和数据集。

此外，本指南要求您实际了解Adobe Experience Platform Web SDK。 如需快速刷新，请阅读[Adobe Experience Platform Web SDK概述](../../home.md)和[常见问题解答](../../faq.md)文档。

## 设置默认同意

在扩展配置中，有一个默认同意设置。 这会控制没有同意Cookie的客户的行为。 如果要对没有同意Cookie的客户的Experience Event进行排队，请将此参数设置为`pending`。 如果要放弃没有同意Cookie的客户的体验事件，请将此参数设置为`out`。 您还可以使用数据元素动态设置默认同意值。 有关详细信息，请参阅[`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md)。

## 使用同意信息更新用户档案 {#consent-code-1}

要在客户同意首选项发生更改时调用[`setConsent`](/help/web-sdk/commands/setconsent.md)操作，请创建标记规则。 首先，添加新事件，然后选择核心扩展的“自定义代码”事件类型。

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

此自定义代码执行两项操作：

* 设置两个数据元素，一个包含同意字符串，另一个包含`gdprApplies`标志。 在稍后填写“设置同意”操作时，这将很有用。

* 同意首选项发生更改时触发规则。 每当同意首选项发生更改时，都应使用“设置同意”操作。 在扩展中添加“Set Consent”操作并填写表单，如下所示：

* 标准：“IAB TCF”
* 版本： &quot;2.0&quot;
* 值：“%IAB TCF同意字符串%”
* GDPR适用：“%IAB TCF同意GDPR%”

![IAB设置同意操作](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>无法使用数据元素选择器选择这些数据元素，因为它们是通过自定义代码创建的。 您必须键入带有百分比符号的数据元素名称。 此代码会在客户发生更改时用他们的新同意首选项更新他们的配置文件。 此外，服务器会返回一个Cookie值，这可能会阻止Adobe Experience Platform Web SDK记录体验事件。

## 为体验事件创建XDM数据元素

同意字符串应包含在XDM体验事件中。 为此，请使用XDM对象数据元素。 首先，创建一个新的XDM对象数据元素，或者使用已创建的用于发送事件的数据元素。 如果您已将“体验事件隐私”架构字段组添加到您的架构，则在XDM对象中应具有`consentStrings`密钥。

1. 选择&#x200B;**[!UICONTROL consentStrings]**。

1. 选择&#x200B;**[!UICONTROL 提供单个项目]**&#x200B;并选择&#x200B;**[!UICONTROL 添加项目]**。

1. 展开&#x200B;**[!UICONTROL consentString]**&#x200B;标题，并展开第一项，然后填写以下值：

* `consentStandard`： IAB TCF
* `consentStandardVersion`： 2.0
* `consentStringValue`： %IAB TCF同意字符串%
* `gdprApplies`： %IAB TCF同意GDPR%

>[!IMPORTANT]
>
>无法使用数据元素选择器选择这些数据元素，因为它们是通过自定义代码创建的。 您必须键入带有百分比符号的数据元素名称。

## 使用IAB TCF 2.0同意信息发送初始体验事件

如果页面上的初始体验事件通过页面加载事件触发，则同意字符串可能尚未加载。 此规则旨在替换当前的页面加载事件。 要确保首先加载同意信息，请创建新规则并将以下代码添加为自定义代码事件：

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

此代码与以前的自定义代码相同，不同之处在于`useractioncomplete`和`tcloaded`事件均已处理。 [previous自定义代码](#consent-code-1)仅在客户首次选择其偏好设置时触发。 当客户已选择其偏好设置时，也会触发此代码。 例如，在第二次加载页面时。

从Experience Platform Web SDK扩展添加“发送事件”操作。 在XDM字段中，选择您在上一部分中创建的XDM数据元素。

## 使用IAB TCF 2.0同意信息发送其他事件

在初始体验事件后触发事件时，仍会定义这两个数据元素，并且它们可用于发送IAB同意信息。 使用相同的XDM数据元素来发送未来的事件。 包含IAB TCF 2.0信息。

## 后续步骤

现在，您已了解如何将IAB TCF 2.0与Experience Platform Web SDK扩展一起使用，您还可以选择与其他Adobe解决方案(如Adobe Analytics或Adobe Real-Time Customer Data Platform)集成。 有关详细信息，请参阅[IAB透明度和同意框架2.0概述](./overview.md)。
