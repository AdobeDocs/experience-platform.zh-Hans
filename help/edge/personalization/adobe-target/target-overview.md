---
title: 将Adobe Target与Platform Web SDK结合使用
description: 了解如何使用Experience Platform Web SDK使用Adobe Target呈现个性化内容
keywords: 目标;adobe 目标;活动.id;experience.id;renderDecisions;decisionScopes;prehiding代码片段；vec；基于表单的体验书写器；xdm;受众；决定；范围；模式;
translation-type: tm+mt
source-git-commit: 98db5b92ea0f51c8641651eb14e3fe6cecf7027c
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 3%

---


# 将Adobe Target与Platform Web SDK结合使用

Adobe Experience Platform [!DNL Web SDK]可以向Web渠道提供和呈现Adobe Target中管理的个性化体验。 您可以使用称为[Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html)(VEC)的WYSIWYG编辑器或非可视界面（[基于表单的体验编辑器](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)）来创建、激活和提供您的活动和个性化体验。

以下功能已经过测试，目前在目标中受支持：

* A/B测试
* A4T印象和转换报告
* 自动个性化
* 体验定位
* Multivariate Tests
* 本机目标印象和转换报告
* VEC支持

## 启用Adobe Target

要启用[!DNL Target]，请执行以下操作：

1. 在[边缘配置](../../fundamentals/edge-configuration.md)中启用目标，使用相应的客户端代码。
1. 将`renderDecisions`选项添加到事件。

然后（可选），您还可以添加以下选项：

* `decisionScopes`:通过将此选项添加到您的活动，检索特定事件(对于使用基于表单的书写器创建的活动很有用)。
* [预先隐藏片段](../manage-flicker.md):仅隐藏页面的某些部分。

## 使用Adobe Target VEC

要将VEC与平台Web SDK实现一起使用，请安装并激活[Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/)或[Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC帮助程序扩展。

## 自动渲染VEC活动

Adobe Experience Platform Web SDK能够在Web上自动呈现通过Adobe Target的VEC为您的用户定义的体验。 要指示Adobe Experience Platform Web SDK自动渲染VEC活动，请发送一个事件，其中`renderDecisions = true`:

```javascript
alloy
("sendEvent", 
  { 
  "renderDecisions": true, 
  "xdm": {
    "commerce": { 
      "order": {
        "purchaseID": "a8g784hjq1mnp3", 
         "purchaseOrderNumber": "VAU3123", 
         "currencyCode": "USD", 
         "priceTotal": 999.98 
         } 
      } 
    }
  }
);
```

## 使用基于表单的书写器

基于表单的体验编辑器是一个非可视界面，可用于配置具有不同响应类型（如JSON、HTML、图像等）的A/B测试、[!DNL Experience Targeting]、Automated Personalization和Recommendations活动。 根据Adobe Target返回的响应类型或决策，可以执行您的核心业务逻辑。 要检索基于表单的书写器活动的决策，请发送包含所有要检索决策的“决策范围”的事件。

```javascript
alloy
  ("sendEvent", { 
    decisionScopes: [
      "foo", "bar"], 
      "xdm": {
        "commerce": { 
          "order": { 
            "purchaseID": "a8g784hjq1mnp3", 
            "purchaseOrderNumber": "VAU3123", 
            "currencyCode": "USD", 
            "priceTotal": 999.98 
          } 
        } 
      } 
    }
  );
```

## 决策范围

`decisionScopes` 定义要呈现个性化体验的页面部分、位置或部分。这些`decisionScopes`是可自定义的和用户定义的。 对于当前[!DNL Target]客户，`decisionScopes`也称为“mboxes”。 在[!DNL Target] UI中，`decisionScopes`显示为“locations”。

## `__view__`范围

Adobe Experience Platform Web SDK提供了一些功能，您无需依赖SDK为您渲染VEC操作即可检索VEC操作。 发送定义为`decisionScopes`的`__view__`事件。

```javascript
alloy("sendEvent", {
      "decisionScopes": ["__view__", "foo", "bar"], 
      "xdm": { 
        "web": { 
          "webPageDetails": { 
            "name": "Home Page"
          }
        } 
      }
    }
  ).then(function(results) {
    for (decision of results.decisions) {
      if (decision.decisionScope === "__view__") {
        console.log(decision.content)
      }
    }
  });
```

## 受众XDM

定义通过Adobe Experience Platform Web SDK交付的目标活动的受众时，必须定义并使用[XDM](https://docs.adobe.com/content/help/zh-Hans/experience-platform/xdm/home.html)。 在定义XDM模式、类和混合后，您可以创建由XDM数据定义的用于定位的目标受众规则。 在目标中，XDM数据在受众 Builder中显示为自定义参数。 XDM使用点记号进行序列化（例如`web.webPageDetails.name`）。

如果您有具有预定义受众的目标活动，这些使用自定义参数或用户用户档案，则无法通过SDK正确提供。 您必须改用XDM，而不是使用自定义参数或用户用户档案。 但是，Adobe Experience Platform Web SDK支持的现成受众定位字段不需要XDM。 这些字段在不需要XDM的目标UI中可用：

* 定位库
* Adobe Target 中的地域
* 网络
* Operating System
* 网站页面
* 浏览器
* 流量源
* 时间范围

## 术语

__决策：__ 决策 [!DNL Target]与从活动中选择的体验相关。

__模式:__ 决策的模式是中的优惠类型 [!DNL Target]。

__范围：__ 决定的范围。在[!DNL Target]中，范围是mBox。 全局mBox是`__view__`范围。

__XDM:__ XDM被串行化为点记号，然后作为mBox [!DNL Target] 参数放入。
