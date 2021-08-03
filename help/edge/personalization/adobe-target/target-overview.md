---
title: 将Adobe Target与Platform Web SDK结合使用
description: 了解如何使用Experience PlatformWeb SDK渲染个性化内容(使用Adobe Target)
keywords: Target;Adobe Target;activity.id;experience.id;renderDecisions;decisionScopes；预隐藏代码片段；VEC；基于表单的体验编辑器；XDM；受众；决策；范围；架构；系统图；图
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 930756b4e10c42edf2d58be16c51d71df207d1af
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 5%

---

# 将[!DNL Adobe Target]与[!DNL Platform Web SDK]一起使用

[!DNL Adobe Experience Platform] [!DNL Web SDK] 可以在web渠道中提供和呈现管理 [!DNL Adobe Target] 的个性化体验。您可以使用名为[可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)(VEC)的WYSIWYG编辑器，或者使用非可视化界面（[基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)）来创建、激活和提供活动和个性化体验。

>[!IMPORTANT]
>
>[Adobe Target文档](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/aep-implementation/aep-web-sdk.html?lang=en)包含的主题包含特定于Platform Web SDK的信息，这些信息与Target特性和功能相关。

以下功能已经过测试，目前在[!DNL Target]中受支持：

* [A/B测试](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T展示和转化报表](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=zh-Hans)
* [Automated Personalization活动](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [体验定位活动](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [多变量测试(MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations活动](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [本机Target展示和转化报表](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC支持](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] 系统图

下图可帮助您了解[!DNL Target]和[!DNL Platform Web SDK]边缘决策的工作流程。

![Adobe Target Web SDK边缘决策图](./assets/target-platform-web-sdk.png)

| 调用 | 详细信息 |
| --- | --- |
| 1 | 设备加载[!DNL Platform Web SDK]。 [!DNL Platform Web SDK]会向边缘网络发送一个请求，其中包含XDM数据、数据流环境ID、传递的参数和客户ID（可选）。 页面（或容器）已预隐藏。 |
| 2 | 边缘网络会向边缘服务发送请求，以便通过访客ID、同意和其他访客上下文信息（如地理位置和设备友好名称）来扩充请求。 |
| 3 | 边缘网络会使用访客ID和传递的参数将扩充的个性化请求发送到[!DNL Target]边缘。 |
| 4 | 配置文件脚本先执行，然后馈送到[!DNL Target]配置文件存储中。 配置文件存储从[!UICONTROL 受众库]中提取区段（例如，从[!DNL Adobe Analytics]、[!DNL Adobe Audience Manager]和[!DNL Adobe Experience Platform]共享的区段）。 |
| 5 | [!DNL Target]根据URL请求参数和配置文件数据，确定要为访客显示哪些活动和体验以用于当前页面查看和将来预取的查看。 [!DNL Target] 然后将此数据发送回边缘网络。 |
| 6 | a.边缘网络会将个性化响应发送回页面，其中可能包含其他个性化的配置文件值。 当前页面上的个性化内容会在默认内容不发生闪烁的情况下尽快显示。<br>b.单页应用程序(SPA)中作为用户操作结果显示的视图的个性化内容会被缓存，这样在触发视图时，便可以立即应用该内容，而无需额外的服务器调用。<br>c.边缘网络发送访客ID以及Cookie中的其他值，例如同意、会话ID、身份、Cookie检查、个性化等。 |
| 7 | 边缘网络将[!UICONTROL Analytics for Target](A4T)详细信息（活动、体验和转化元数据）转发到[!DNL Analytics]边缘。 |

## 启用[!DNL Adobe Target]

要启用[!DNL Target]，请执行以下操作：

1. 在[datastream](../../fundamentals/datastreams.md)中使用相应的客户端代码启用[!DNL Target]。
1. 将`renderDecisions`选项添加到事件中。

然后，您也可以选择添加以下选项：

* **`decisionScopes`**:通过向事件添加此选项来检索特定活动（对于通过基于表单的编辑器创建的活动非常有用）。
* **[预隐藏代码片段](../manage-flicker.md)**:仅隐藏页面的某些部分。

## 使用Adobe Target VEC

要将VEC与[!DNL Platform Web SDK]实施结合使用，请安装并激活[Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/)或[Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC助手扩展。

有关更多信息，请参阅&#x200B;*Adobe Target指南*&#x200B;中的[Visual Experience Composer帮助程序扩展](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html)。

## 呈现个性化内容

有关更多信息，请参阅[渲染个性化内容](../rendering-personalization-content.md)。

## XDM中的受众

在为通过[!DNL Platform Web SDK]交付的[!DNL Target]活动定义受众时，必须定义并使用[XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hans)。 定义XDM架构、类和架构字段组后，可以创建由XDM数据定义的用于定位的[!DNL Target]受众规则。 在[!DNL Target]中，XDM数据作为自定义参数显示在[!UICONTROL Audience Builder]中。 XDM使用点表示法进行序列化（例如，`web.webPageDetails.name`）。

如果您的[!DNL Target]活动包含使用自定义参数或用户配置文件的预定义受众，则这些活动无法通过SDK正确交付。 您必须改用XDM，而不是使用自定义参数或用户配置文件。 但是，通过[!DNL Platform Web SDK]支持的一些现成受众定位字段不需要XDM。 在[!DNL Target] UI中，不需要XDM的字段如下：

* 定位库
* Adobe Target 中的地域
* 网络
* Operating System
* 网站页面
* 浏览器
* 流量源
* 时间范围

有关更多信息，请参阅&#x200B;*Adobe Target指南*&#x200B;中的[受众类别](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en)。

### 响应令牌

响应令牌主要用于将元数据发送到Google、Facebook等第三方。 返回响应令牌
`propositions` -> `items`内的`meta`字段中。 以下是一个示例：

```
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

要收集响应令牌，您必须订阅`alloy.sendEvent` promise，并遍历`propositions`
并从`items` -> `meta`中提取详细信息。 每个`proposition`都有一个`renderAttempted`布尔字段
指示是否呈现了`proposition`。 请参阅以下示例：

```
alloy("sendEvent",
  {
    renderDecisions: true,
    decisionScopes: [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

启用自动渲染后，命题数组包含：

#### 在页面加载时：

* 基于表单的编辑器，其标记设置为`renderAttempted`且基于`propositions``false`
* 基于可视化体验编辑器的命题，其中`renderAttempted`标记设置为`true`
* 基于可视化体验编辑器的建议，提供了将`renderAttempted`标记设置为`true`的单页应用程序视图

#### 在查看时 — 更改（对于缓存的视图）：

* 基于可视化体验编辑器的建议，提供了将`renderAttempted`标记设置为`true`的单页应用程序视图

禁用自动渲染时，命题数组包含：

#### 在页面加载时：

* 基于表单的编辑器，其标记设置为`renderAttempted`且基于`propositions``false`
* 基于可视化体验编辑器的命题，其中`renderAttempted`标记设置为`false`
* 基于可视化体验编辑器的建议，提供了将`renderAttempted`标记设置为`false`的单页应用程序视图

#### 在查看时 — 更改（对于缓存的视图）：

* 基于可视化体验编辑器的建议，提供了将`renderAttempted`标记设置为`false`的单页应用程序视图

### 单个配置文件更新

使用[!DNL Platform Web SDK]可将配置文件更新为[!DNL Target]配置文件，并将[!DNL Platform Web SDK]作为体验事件更新为。

要更新[!DNL Target]配置文件，请确保配置文件数据与以下内容一起传递：

* 在 `“data {“`
* 在 `“__adobe.target”`
* 前缀`“profile.”`，例如，如下所示

| 键 | 类型 | 描述 |
| --- | --- | --- |
| `renderDecisions` | 布尔值 | 指示个性化组件是否应解释DOM操作 |
| `decisionScopes` | 阵列`<String>` | 要检索决策的范围列表 |
| `xdm` | 对象 | 在XDM中格式化的数据，这些数据会作为体验事件进入Platform Web SDK中 |
| `data` | 对象 | 发送到目标类下[!DNL Target]解决方案的任意键/值对。 |

使用此命令的典型[!DNL Platform Web SDK]代码如下所示：

**`sendEvent`使用用户档案数据**

```
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**如何将用户档案属性发送到Adobe Target:**

```
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## 请求推荐

下表列出了[!DNL Recommendations]属性，以及是否通过[!DNL Platform Web SDK]支持每个属性：

| 类别 | 属性 | 支持状态 |
| --- | --- | --- |
| Recommendations — 默认实体属性 | entity.id | 受支持 |
|  | entity.name | 受支持 |
|  | entity.categoryId | 受支持 |
|  | entity.pageUrl | 受支持 |
|  | entity.thumbnailUrl | 受支持 |
|  | entity.message | 受支持 |
|  | entity.value | 受支持 |
|  | entity.inventory | 受支持 |
|  | entity.brand | 受支持 |
|  | entity.margin | 受支持 |
|  | entity.event.detailsOnly | 受支持 |
| Recommendations — 自定义实体属性 | entity.yourCustomAttributeName | 受支持 |
| Recommendations — 保留的mbox/页面参数 | excludedIds | 受支持 |
|  | cartIds | 受支持 |
|  | productPurchasedId | 受支持 |
| 类别亲和度的页面或项目类别 | user.categoryId | 受支持 |

**如何将Recommendations属性发送到Adobe Target:**

```
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id" : "123",
        "entity.genre" : "Drama"
      }
    }
  }
});
```

## 调试

mboxTrace和mboxDebug已被弃用。 使用[[!DNL Platform Web SDK] 调试](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html)。

## 术语

__命题：__ 在中 [!DNL Target]，命题与从活动中选择的体验相关联。

__架构：__ 决策的架构是中的选件类 [!DNL Target]型。

__范围：__ 决定的范围。在[!DNL Target]中，范围为mBox。 全局mBox是`__view__`范围。

__XDM:__ XDM将序列化为点表示法，然后作为mBox [!DNL Target] 参数放入中。
