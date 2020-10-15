---
title: 将IAB TCF 2.0与Experience Platform Launch一起使用
seo-title: 设置IAB TCF 2.0同意Adobe Experience Platform Launch和Adobe Experience PlatformWeb SDK
description: 了解如何设置IAB TCF 2.0与Adobe Experience Platform Launch和Adobe Experience PlatformWeb SDK的同意
seo-description: 了解如何设置IAB TCF 2.0与Adobe Experience Platform Launch和Adobe Experience PlatformWeb SDK的同意
translation-type: tm+mt
source-git-commit: db742119d8f169817080f1fd4e0dc08a0f0faa47
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%

---


# 将IAB TCF 2.0与Experience Platform Launch和AEP Web SDK扩展一起使用

Adobe Experience PlatformWeb软件开发工具包(Adobe Experience PlatformWeb SDK)支持交互式广告局透明度和同意框架，版本2.0(IAB TCF 2.0)。 本指南向您展示如何设置一个Adobe Experience Platform Launch属性，用于使用AEP Web SDK扩展向Adobe发送IAB TCF 2.0同意信息以用于Experience Platform Launch。

如果您不想使用Experience Platform Launch，请参阅有关使用IAB TCF 2. [0而不使用Experience Platform Launch的指南](./without-launch.md)。

## 入门指南

要将IAB TCF 2.0与Experience Platform Launch及AEP Web SDK扩展一起使用，您需要提供XDM模式和数据集。 如果您尚未设置以上任一设置，请在继续操作之前查看本《Adobe Experience PlatformWeb SDK Launch快速开始指南》进行开始。

此外，本指南要求您对Adobe Experience PlatformWeb SDK有有效的了解。 要获得快速复习资料，请阅读 [Adobe Experience PlatformWeb SDK概述](../../home.md)[和常见问题解答文档](../../web-sdk-faq.md) 。

## 设置默认同意

在扩展配置中，存在默认同意设置。 这可控制未获得同意cookie的客户的行为。 如果要为未获得同意cookie的客户排队体验事件，请将其设置为 `pending`。

>[!NOTE]
>
>目前，无法通过Experience Platform Launch扩展动态设置此扩展。

有关默认同意的详细信息，请参 [阅SDK配置文档中](../../fundamentals/configuring-the-sdk.md#default-consent) “默认同意”部分。

## 在获得同意信息的情况下更新用户档案 {#consent-code-1}

要在客户 `setConsent` 同意偏好发生更改时采取相应措施，您需要创建新的Experience Platform Launch规则。 开始，添加新事件并选择核心扩展的“自定义代码”事件类型。

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

* 设置两个数据元素，一个包含同意字符串，另一个包含标 `gdprApplies` 志。 这在以后填写“设置同意”操作时很有用。

* 在同意偏好发生更改时触发规则。 只要同意偏好发生更改，应使用“设置同意”操作。 在扩展中添加“设置同意”操作，然后按如下方式填写表单：

* 标准：&quot;IAB TCF&quot;
* 版本：“2.0”
* 值：&quot;%IAB TCF同意字符串%&quot;
* GDPR适用：&quot;%IAB TCF同意GDPR%&quot;

![IAB设置同意操作](../../../assets/iab_set_consent_action.png)

>[!IMPORTANT]
>
>无法使用数据元素选择器选择这些数据元素，因为它们是通过自定义代码创建的。 必须键入带百分号的数据元素名称。 此代码会在客户发生更改时使用新的同意偏好更新其用户档案。 此外，服务器返回一个cookie值，这可能会阻止Adobe Experience PlatformWeb SDK记录体验事件。

## 为体验事件创建XDM数据元素

同意字符串应包含在XDM体验事件中。 为此，请使用XDM对象数据元素。 开始，方法是创建新的XDM对象数据元素，或者使用已创建的元素发送事件。 如果您已将体验事件隐私混合添加到模式，您应该在XDM `consentStrings` 对象中有一个键。

1. 选择 **[!UICONTROL connenceStrings]**。

1. 选择 **[!UICONTROL 提供单个项目]** ，然后选择 **[!UICONTROL 添加项目]**。

1. 展开 **[!UICONTROL conventionString]** 标题，并展开第一个项目，然后填写以下值：

* `consentStandard`:IAB TCF
* `consentStandardVersion`: 2.0
* `consentStringValue`:%IAB TCF同意字符串%
* `gdprApplies`:%IAB TCF同意GDPR%

>[!IMPORTANT]
>
>无法使用数据元素选择器选择这些数据元素，因为它们是通过自定义代码创建的。 必须键入带百分号的数据元素名称。

## 使用IAB TCF 2.0同意信息发送初始体验事件

如果页面上的初始体验事件是通过页面加载事件触发的，则同意字符串可能尚未加载。 此规则用于替换当前页面加载事件。 要确保首先加载同意信息，请创建新规则，并将以下代码添加为自定义代码事件:

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

此代码与以前的自定义代码相同，只是同时处理 `useractioncomplete` 和 `tcloaded` 事件。 之前 [的自定义代码](#consent-code-1) ，仅在客户首次选择其首选项时触发。 当客户已选择其首选项时，也会触发此代码。 例如，在第二页加载。

从Adobe Experience PlatformWeb SDK扩展添加“发送事件”操作。 在XDM字段中，选择您在上一节中创建的XDM数据元素。

## 发送其他事件，并提供IAB TCF 2.0同意信息

当事件在初始体验事件后触发时，仍然会定义这两个数据元素，并可用于发送IAB同意信息。 使用相同的XDM数据元素发送未来事件。 包含IAB TCF 2.0信息。

## 后续步骤

既然您已经学习了如何将IAB TCF 2.0与Adobe Experience PlatformWeb SDK扩展一起使用，您还可以选择与其他Adobe解决方案(如Adobe Analytics或实时客户数据平台)集成。 有关更 [多信息，请参阅IAB透明度和同意框架](./overview.md) 2.0概述。
