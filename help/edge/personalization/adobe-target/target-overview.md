---
title: 将Adobe Target与Platform Web SDK结合使用
description: 了解如何使用Experience PlatformWeb SDK渲染个性化内容(使用Adobe Target)
keywords: Target;Adobe Target;activity.id;experience.id;renderDecisions;decisionScopes；预隐藏代码片段；VEC；基于表单的体验编辑器；XDM；受众；决策；范围；架构；
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 3%

---

# 将Adobe Target与Platform Web SDK结合使用

Adobe Experience Platform [!DNL Web SDK]可以将Adobe Target中管理的个性化体验交付和渲染到Web渠道中。 您可以使用名为[可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)(VEC)的WYSIWYG编辑器，或者使用非可视化界面（[基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)）来创建、激活和提供活动和个性化体验。

以下功能已经过测试，目前在Target中受支持：

* A/B测试
* A4T展示和转化报表
* 自动个性化
* 体验定位
* 多变量测试
* 本机Target展示和转化报表
* VEC支持

## 启用Adobe Target

要启用[!DNL Target]，请执行以下操作：

1. 在[数据流](../../fundamentals/datastreams.md)中使用相应的客户端代码启用Target。
1. 将`renderDecisions`选项添加到事件中。

然后，您也可以选择添加以下选项：

* `decisionScopes`:通过向事件添加此选项来检索特定活动（对于通过基于表单的编辑器创建的活动非常有用）。
* [预隐藏代码片段](../manage-flicker.md):仅隐藏页面的某些部分。

## 使用Adobe Target VEC

要将VEC与Platform Web SDK实施结合使用，请安装并激活[Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/)或[Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC助手扩展。

## 自动渲染VEC活动

Adobe Experience Platform Web SDK能够在Web上为用户自动渲染通过Adobe Target VEC定义的体验。 要指示Adobe Experience Platform Web SDK自动渲染VEC活动，请发送一个包含`renderDecisions = true`的事件：

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

## 使用基于表单的编辑器

基于表单的体验编辑器是一个非可视化界面，可用于配置具有不同响应类型（如JSON、HTML、图像等）的A/B测试、[!DNL Experience Targeting]、Automated Personalization和Recommendations活动。 根据Adobe Target返回的响应类型或决策，可以执行您的核心业务逻辑。 要检索基于表单的编辑器活动的决策，请发送一个事件，其中包含您要为其检索决策的所有“decisionScopes”。

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

`decisionScopes` 定义要在其中呈现个性化体验的页面区域、位置或部分。这些`decisionScopes`是可自定义的，且由用户定义。 对于当前的[!DNL Target]客户，`decisionScopes`也称为“mbox”。 在[!DNL Target] UI中， `decisionScopes`显示为“位置”。

## `__view__`范围

Adobe Experience Platform Web SDK提供了一项功能，通过该功能，您无需依赖SDK即可检索VEC操作，从而为您渲染VEC操作。 发送定义为`decisionScopes`的`__view__`事件。

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

## XDM中的受众

在为通过Adobe Experience Platform Web SDK交付的Target活动定义受众时，必须定义和使用[XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hans)。 在定义XDM架构、类和架构字段组后，您可以创建由XDM数据定义的用于定位的Target受众规则。 在Target中，XDM数据会作为自定义参数显示在受众生成器中。 XDM使用点表示法进行序列化（例如，`web.webPageDetails.name`）。

如果您的Target活动具有使用自定义参数或用户配置文件的预定义受众，则这些受众无法通过SDK正确交付。 您必须改用XDM，而不是使用自定义参数或用户配置文件。 但是，通过Adobe Experience Platform Web SDK支持的一些现成的受众定位字段不需要XDM。 这些字段在Target UI中可用，不需要XDM:

* 定位库
* Adobe Target 中的地域
* 网络
* Operating System
* 网站页面
* 浏览器
* 流量源
* 时间范围

## 术语

__决策：__ 在中 [!DNL Target]，决策与从活动中选择的体验相关联。

__架构：__ 决策的架构是中的选件类 [!DNL Target]型。

__范围：__ 决定的范围。在[!DNL Target]中，范围为mBox。 全局mBox是`__view__`范围。

__XDM:__ XDM将序列化为点表示法，然后作为mBox [!DNL Target] 参数放入中。
