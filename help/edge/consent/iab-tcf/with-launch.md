---
title: 使用Platform launch和Platform Web SDK扩展集成IAB TCF 2.0支持
description: 了解如何设置Adobe Experience Platform Launch和Adobe Experience Platform Web SDK扩展的IAB TCF 2.0同意。
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---


# 使用Platform launch和Platform Web SDK扩展集成IAB TCF 2.0支持

Adobe Experience Platform Web SDK支持Interactive Advertising Bureau透明度和同意框架，版本2.0(IAB TCF 2.0)。 本指南向您介绍如何设置Adobe Experience Platform Launch属性，以便使用Adobe Experience Platform Web SDK扩展将IAB TCF 2.0同意信息发送到Adobe进行Experience Platform Launch。

如果您不想使用Experience Platform Launch，请参阅[上关于使用不带Experience Platform Launch的IAB TCF 2.0的指南](./without-launch.md)。

## 入门指南

要将IAB TCF 2.0与Experience Platform Launch及Platform Web SDK扩展一起使用，您需要提供XDM模式和数据集。

此外，本指南要求您对Adobe Experience Platform Web SDK有正确的了解。 有关快速复习，请阅读[Adobe Experience Platform Web SDK概述](../../home.md)和[常见问题解答](../../web-sdk-faq.md)文档。

## 设置默认同意

在扩展配置中，存在默认同意设置。 这会控制没有同意Cookie的客户的行为。 如果要为未获得同意Cookie的客户排队体验事件，请将其设置为`pending`。

>[!NOTE]
>
>目前，无法通过Experience Platform Launch扩展动态设置。

有关默认同意的详细信息，请参阅SDK配置文档中的[默认同意部分](../../fundamentals/configuring-the-sdk.md#default-consent)。

## 使用同意信息{#consent-code-1}更新用户档案

要在客户同意偏好发生更改时调用`setConsent`操作，您需要创建新的Experience Platform Launch规则。 开始，添加新事件并选择核心扩展的“自定义代码”事件类型。

对新事件使用以下代码示例：

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

此自定义代码具有两项功能：

* 设置两个数据元素，一个包含同意字符串，另一个包含`gdprApplies`标志。 这在以后填写“设置同意”操作时很有用。

* 在同意偏好发生更改时触发规则。 每当同意偏好发生更改时，应使用“设置同意”操作。 在扩展中添加“设置同意”操作，然后按如下方式填写表单：

* 标准：&quot;IAB TCF&quot;
* 版本：“2.0”
* 值：&quot;%IAB TCF同意字符串%&quot;
* GDPR适用：&quot;%IAB TCF同意GDPR%&quot;

![IAB设置同意操作](../../../assets/iab_set_consent_action.png)

>[!IMPORTANT]
>
>您无法使用数据元素选择器选择这些数据元素，因为它们是通过自定义代码创建的。 您必须在数据元素名称中键入百分号。 此代码会在客户更改时使用新的同意首选项更新其用户档案。 此外，服务器返回一个Cookie值，这可能会阻止Adobe Experience Platform Web SDK录制Experience事件。

## 为体验事件创建XDM数据元素

同意字符串应包含在XDM体验事件中。 为此，请使用XDM对象数据元素。 开始，方法是创建新的XDM对象数据元素，或者使用您已创建的用于发送事件的元素。 如果您已将体验事件隐私混合添加到模式，则XDM对象中应包含`consentStrings`键。

1. 选择&#x200B;**[!UICONTROL connenceStrings]**。

1. 选择&#x200B;**[!UICONTROL 提供单个项目]**&#x200B;并选择&#x200B;**[!UICONTROL 添加项目]**。

1. 展开&#x200B;**[!UICONTROL connenceString]**&#x200B;标题，展开第一个项目，然后填写以下值：

* `consentStandard`:IAB TCF
* `consentStandardVersion`:2.0
* `consentStringValue`:%IAB TCF同意字符串%
* `gdprApplies`:%IAB TCF同意GDPR%

>[!IMPORTANT]
>
>您无法使用数据元素选择器选择这些数据元素，因为它们是通过自定义代码创建的。 您必须在数据元素名称中键入百分号。

## 使用IAB TCF 2.0同意信息发送初始体验事件

如果页面上的初始体验事件是通过页面加载事件触发的，则同意字符串可能尚未加载。 此规则旨在替换当前页面加载事件。 要确保首先加载同意信息，请创建新规则，并将以下代码添加为自定义代码事件:

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

此代码与以前的自定义代码相同，只是处理了`useractioncomplete`和`tcloaded`事件。 [之前的自定义代码](#consent-code-1)仅在客户首次选择其首选项时触发。 当客户已选择其首选项时，也会触发此代码。 例如，在第二页加载时。

从Platform Web SDK扩展添加“发送事件”操作。 在XDM字段中，选择您在上一节中创建的XDM数据元素。

## 使用IAB TCF 2.0同意信息发送其他事件

当事件在初始体验事件后触发时，仍会定义两个数据元素，并可用于发送IAB同意信息。 使用相同的XDM数据元素发送将来的事件。 包括IAB TCF 2.0信息。

## 后续步骤

现在，您已学习如何将IAB TCF 2.0与Platform Web SDK扩展一起使用，您还可以选择与其他Adobe解决方案(如Adobe Analytics或实时客户数据平台)集成。 有关详细信息，请参阅[IAB透明度和同意框架2.0概述](./overview.md)。
