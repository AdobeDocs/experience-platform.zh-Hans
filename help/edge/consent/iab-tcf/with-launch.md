---
title: 使用标记和Platform Web SDK扩展集成IAB TCF 2.0支持
description: 了解如何使用标记和Adobe Experience Platform Web SDK扩展设置IAB TCF 2.0同意书。
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# 使用标记和Platform Web SDK扩展集成IAB TCF 2.0支持

Adobe Experience Platform Web SDK支持Interactive Advertising Bureau Transparency &amp; Consent Framework 2.0版(IAB TCF 2.0)。 本指南向您展示了如何使用Adobe Experience Platform Web SDK标记扩展设置标记属性，以将IAB TCF 2.0同意信息发送到Adobe。

如果您不想使用标记，请参阅的指南 [使用不带标记的IAB TCF 2.0](./without-launch.md).

## 快速入门

要将IAB TCF 2.0与标记和Platform Web SDK扩展结合使用，您需要具有XDM模式和数据集。

此外，本指南还要求您实际了解Adobe Experience Platform Web SDK。 如需快速复习，请阅读 [Adobe Experience Platform Web SDK概述](../../home.md) 和 [常见问题解答](../../web-sdk-faq.md) 文档。

## 设置默认同意

在扩展配置中，有一个默认同意设置。 这会控制没有同意Cookie的客户的行为。 如果要为没有同意Cookie的客户对体验事件进行排队，请将其设置为 `pending`. 如果要放弃没有同意Cookie的客户的体验事件，请将其设置为 `out`. 您还可以使用数据元素来动态设置默认同意值。

有关如何配置默认同意的更多信息，请参阅 [默认同意部分](../../fundamentals/configuring-the-sdk.md#default-consent) （ SDK配置指南）。

## 使用同意信息更新用户档案 {#consent-code-1}

调用 `setConsent` 操作：当客户同意首选项发生更改时，您需要创建一个新的标记规则。 首先，添加新事件，然后选择核心扩展的“Custom Code”事件类型。

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

* 设置两个数据元素，一个包含同意字符串，另一个包含 `gdprApplies` 标志。 这在以后填写“设置同意”操作时很有用。

* 当同意首选项发生更改时触发规则。 每当同意首选项发生更改时，都应使用“设置同意”操作。 在扩展中添加“Set Consent”操作并填写表单，如下所示：

* 标准：“IAB TCF”
* 版本：“2.0”
* 值：“%IAB TCF同意字符串%”
* GDPR适用：“%IAB TCF同意GDPR%”

![IAB设置同意操作](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>您无法使用数据元素选择器选择这些数据元素，因为它们是通过自定义代码创建的。 您必须键入带有百分比符号的数据元素名称。 此代码会随时使用客户的新同意首选项更新他们的配置文件。 此外，服务器会返回一个Cookie值，这可能会阻止Adobe Experience Platform Web SDK记录体验事件。

## 为体验事件创建XDM数据元素

同意字符串应包含在XDM体验事件中。 为此，请使用XDM对象数据元素。 首先创建一个新的XDM对象数据元素，或者使用已经为发送事件创建的元素。 如果您已将“体验事件隐私”架构字段组添加到架构，则您应具有 `consentStrings` 键。

1. 选择 **[!UICONTROL consentstrings]**.

1. 选择 **[!UICONTROL 提供单个项目]** 并选择 **[!UICONTROL 添加项目]**.

1. 展开 **[!UICONTROL consent字符串]** 标题，并展开第一个项目，然后填写以下值：

* `consentStandard`：IAB TCF
* `consentStandardVersion`: 2.0
* `consentStringValue`： %IAB TCF同意字符串%
* `gdprApplies`： %IAB TCF同意GDPR%

>[!IMPORTANT]
>
>您无法使用数据元素选择器选择这些数据元素，因为它们是通过自定义代码创建的。 您必须键入带有百分比符号的数据元素名称。

## 使用IAB TCF 2.0同意信息发送初始体验事件

如果页面上的初始体验事件是通过页面加载事件触发的，则同意字符串可能尚未加载。 此规则用于替换当前页面加载事件。 要确保首先加载同意信息，请创建新规则并将以下代码添加为自定义代码事件：

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

此代码与以前的自定义代码相同，不同之处在于 `useractioncomplete` 和 `tcloaded` 事件已处理。 此 [上一个自定义代码](#consent-code-1) 仅当客户首次选择其偏好时才会触发。 当客户已选择其偏好设置时，也会触发此代码。 例如，在第二个页面加载时。

从Platform Web SDK扩展添加“发送事件”操作。 在XDM字段中，选择您在上一部分中创建的XDM数据元素。

## 发送包含IAB TCF 2.0同意信息的其他事件

如果在初始体验事件之后触发事件，则仍会定义这两个数据元素，并且这些数据元素可用于发送IAB同意信息。 使用同一XDM数据元素发送未来的事件。 包含IAB TCF 2.0信息。

## 后续步骤

现在，您已了解如何将IAB TCF 2.0与Platform Web SDK扩展结合使用，您还可以选择与其他Adobe解决方案(如Adobe Analytics或Adobe Real-time Customer Data Platform)集成。 请参阅 [IAB透明度和同意框架2.0概述](./overview.md) 了解更多信息。
