---
title: 'Adobe Target和Adobe Experience PlatformWeb SDK。 '
seo-title: Adobe Experience PlatformWeb SDK和使用Adobe Target
description: 了解如何使用Experience PlatformWeb SDK使用Adobe Target呈现个性化内容
seo-description: 了解如何使用Experience PlatformWeb SDK使用Adobe Target呈现个性化内容
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisionScopes;prehiding snippet;vec;Form-Based Experience Composer;xdm;audiences;decisions;scope;schema;
translation-type: tm+mt
source-git-commit: d069b3007265406367ca9de2b85540b2a070cf36
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 3%

---


# [!DNL Target] 概述

Adobe Experience Platform可 [!DNL Web SDK] 以向网络渠道提供和呈现在Adobe Target管理的个性化体验。 您可以使用WYSIWYG编辑器(称为 [Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) (VEC))或非可视界面(基于表 [单的体验书写器](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html))来创建、激活和提供您的活动和个性化体验。

## 使Adobe Target

要启 [!DNL Target]用，您需要执行以下操作：

1. 在UI中打开活动.id和experience.id响应令 [!DNL Target] 牌。

![目标响应令牌](./assets/target_response_token.png)

1. 在边缘配置中 [启用目标](../../fundamentals/edge-configuration.md) ，并使用相应的客户端代码。
1. 将选项 `renderDecisions` 添加到事件。

然后（可选）您还可以：

* 添加 `decisionScopes` 到事件以检索特定活动(对于使用基于表单的书写器创建的活动很有用)。
* 添加预 [隐藏片段](../manage-flicker.md) ，以仅隐藏页面的某些部分。

## 使用Adobe TargetVEC

在SDK中，您可以正常使用VEC，但有一个例外：您需要安 [装目标VEC帮助程序](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) ，并处于活动状态。

## 自动渲染VEC活动

AEP Web SDK能够在Web上自动呈现通过Adobe Target的VEC定义的体验，供您的用户使用。 要向AEP Web SDK指示自动渲染VEC活动，请发送事件，其中 `renderDecisions = true`:

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

基于表单的体验书写器是一个非可视界面，可用于配置A/B测试、 [!DNL Experience Targeting]Automated Personalization和Recommendations活动（JSON、HTML、图像等不同响应类型）。 根据Adobe Target返回的响应类型或决策，可以执行您的核心业务逻辑。 要检索基于表单的书写器活动的决策，请发送包含所有要检索决策的“决策范围”的事件。

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

`decisionScopes` 定义要呈现个性化体验的页面部分、位置或部分。 这些 `decisionScopes` 功能可自定义且由用户定义。 对于当 [!DNL Target] 前客 `decisionScopes` 户，也称为“mboxes”。 在UI [!DNL Target] 中， `decisionScopes` 显示为“位置”。

## 范 `__view__` 围

AEP [!DNL Web SDK] 提供了一项功能，您可以在该功能中检索VEC操作，而不依 [!DNL Web SDK] 赖AEP为您渲染VEC操作。 发送定义 `__view__` 为的事件 `decisionScopes`。

```javascript
alloy("sendEvent", {
  decisionScopes: [“__view__”,"foo", "bar"], 
  "xdm": { 
    "web": { 
      "webPageDetails": { 
        "name": "Home Page"
       }
      } 
     }
    }
   ).then(results){
  for (decision of results.decisions){
     if(decision.decisionScope == "__view__")
       console.log(decision.content)
}
};
```

## 受众XDM

为将通过AEP Web SDK交付的受众活动定义目标时，必 [须定义](https://docs.adobe.com/content/help/zh-Hans/experience-platform/xdm/home.html) 并使用XDM。 定义XDM模式、类和混合后，您可以创建由XDM数据定义的目标受众规则进行定位。 在目标中，XDM数据在受众生成器中显示为一个自定义参数。 XDM使用点记号(例如， `web.webPageDetails.name`)序列化。

如果您有具有使用自定义参数或用户用户档案的预定义受众的目标活动，请注意，这些无法通过AEP Web SDK正确提供。 您必须改用XDM，而不是使用自定义参数或用户用户档案。 但是，AEP Web SDK支持的现成受众定位字段不需要XDM。 以下是目标UI中不需要XDM的可用字段：

* 定位库
* Adobe Target 中的地域
* 网络
* Operating System
* 网站页面
* 浏览器
* 流量源
* 时间范围

## 术语

__决策：__ 在 [!DNL Target]中，这些属性与从活动中选择的体验相关。

__模式:__ 决策的模式是优惠的类型 [!DNL Target]。

__范围：__ 决定的范围。 这 [!DNL Target]是mBox。 全局mBox是范 `__view__` 围。

__XDM:__ XDM被串行化为点记号，然后作为mBox参 [!DNL Target] 数输入。
