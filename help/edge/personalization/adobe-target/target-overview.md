---
title: 将Adobe Target与Platform Web SDK结合使用
description: 了解如何使用Experience PlatformWeb SDK渲染个性化内容(使用Adobe Target)
keywords: Target;Adobe Target;activity.id;experience.id;renderDecisions;decisionScopes；预隐藏代码片段；VEC；基于表单的体验编辑器；XDM；受众；决策；范围；架构；系统图；图
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 5a048505be139b58dbb3bf85120df5e3cc46881e
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 6%

---

# 使用 [!DNL Adobe Target] 和 [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] 可以提供和呈现在中管理的个性化体验 [!DNL Adobe Target] 到web渠道。 您可以使用WYSIWYG编辑器，称为 [可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC)，或者非可视化界面， [基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)，以创建、激活和提供活动和个性化体验。

>[!IMPORTANT]
>
>了解如何使用 [将Target从at.js 2.x迁移到平台Web SDK](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html) 教程。
>
>了解如何首次使用 [使用Web SDK实施Adobe Experience Cloud](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hans) 教程。 有关特定于Target的信息，请参阅标题为的教程部分 [使用Platform Web SDK设置Target](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).


以下功能已经过测试，目前在 [!DNL Target]:

* [A/B测试](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T展示和转化报表](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization活动](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [体验定位活动](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [多变量测试(MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations 活动](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [本机Target展示和转化报表](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC支持](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] 系统图

下图可帮助您了解 [!DNL Target] 和 [!DNL Platform Web SDK] 边缘决策。

![Adobe Target Web SDK边缘决策图](./assets/target-platform-web-sdk.png)

| 调用 | 详细信息 |
| --- | --- |
| 1 | 设备加载 [!DNL Platform Web SDK]. 的 [!DNL Platform Web SDK] 向边缘网络发送请求，其中包含XDM数据、数据流环境ID、传递的参数和客户ID（可选）。 页面（或容器）已预隐藏。 |
| 2 | 边缘网络会向边缘服务发送请求，以便通过访客ID、同意和其他访客上下文信息（如地理位置和设备友好名称）来扩充请求。 |
| 3 | 边缘网络将扩充的个性化请求发送到 [!DNL Target] 具有访客ID和传入参数的边缘。 |
| 4 | 配置文件脚本先执行，然后馈送到中 [!DNL Target] 配置文件存储。 配置文件存储从 [!UICONTROL 受众库] (例如，从 [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform])。 |
| 5 | 根据URL请求参数和配置文件数据， [!DNL Target] 确定要为访客显示哪些活动和体验以用于当前页面查看和将来预取的查看。 [!DNL Target] 然后将此数据发送回边缘网络。 |
| 6 | a.边缘网络会将个性化响应发送回页面，其中可能包含其他个性化的配置文件值。 当前页面上的个性化内容会在默认内容不发生闪烁的情况下尽快显示。<br>b.单页应用程序(SPA)中作为用户操作结果显示的视图的个性化内容会被缓存，这样在触发视图时，便可以立即应用该内容，而无需额外的服务器调用。 <br>c.边缘网络发送访客ID以及Cookie中的其他值，例如同意、会话ID、身份、Cookie检查、个性化等。 |
| 7 | 边缘网络转发 [!UICONTROL Analytics for Target] (A4T)详细信息（活动、体验和转化元数据） [!DNL Analytics] 边缘。 |

## 启用 [!DNL Adobe Target]

启用 [!DNL Target]，请执行以下操作：

1. 启用 [!DNL Target] 在 [数据流](../../datastreams/overview.md) 和相应的客户端代码。
1. 添加 `renderDecisions` 选项。

然后，您也可以选择添加以下选项：

* **`decisionScopes`**:通过向事件添加此选项来检索特定活动（对于通过基于表单的编辑器创建的活动非常有用）。
* **[预隐藏代码片段](../manage-flicker.md)**:仅隐藏页面的某些部分。

## 使用Adobe Target VEC

要将VEC与 [!DNL Platform Web SDK] 实施、安装和激活 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 或 [铬黄](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC助手扩展。

有关更多信息，请参阅 [可视化体验编辑器助手扩展](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) 在 *Adobe Target指南*.

## 呈现个性化内容

请参阅 [呈现个性化内容](../rendering-personalization-content.md) 以了解更多信息。

## XDM中的受众

在为 [!DNL Target] 通过 [!DNL Platform Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hans) 必须定义和使用。 在定义XDM架构、类和架构字段组后，您可以创建 [!DNL Target] 由XDM数据定义的用于定位的受众规则。 在 [!DNL Target]，则XDM数据会显示在 [!UICONTROL Audience Builder] 作为自定义参数。 XDM使用点表示法进行序列化(例如， `web.webPageDetails.name`)。

如果 [!DNL Target] 具有使用自定义参数或用户配置文件的预定义受众的活动，无法通过SDK正确交付这些活动。 您必须改用XDM，而不是使用自定义参数或用户配置文件。 但是，通过 [!DNL Platform Web SDK] 不需要XDM的XDM。 这些字段在 [!DNL Target] 不需要XDM的UI:

* 定位库
* 地域
* 网络
* 操作系统
* 站点页面
* 浏览器
* 流量源
* 时间范围

有关更多信息，请参阅 [受众类别](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) 在 *Adobe Target指南*.

### 响应令牌

响应令牌主要用于将元数据发送到Google、Facebook等第三方。 在 `meta` 字段 `propositions` -> `items`. 以下是一个示例：

```json
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

要收集响应令牌，您必须订阅 `alloy.sendEvent` 承诺，迭代 `propositions`
并从 `items` -> `meta`. 每 `proposition` 具有 `renderAttempted` 布尔字段，指示是否 `proposition` 是否呈现。 请参阅以下示例：

```js
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

* 基于表单的编辑器 `propositions` with `renderAttempted` 标志设置为 `false`
* 基于可视化体验编辑器的建议，包括 `renderAttempted` 标志设置为 `true`
* 基于可视化体验编辑器的建议，用于单页应用程序视图 `renderAttempted` 标志设置为 `true`

#### 在查看时 — 更改（对于缓存的视图）：

* 基于可视化体验编辑器的建议，用于单页应用程序视图 `renderAttempted` 标志设置为 `true`

禁用自动渲染时，命题数组包含：

#### 在页面加载时：

* 基于表单的编辑器 `propositions` with `renderAttempted` 标志设置为 `false`
* 基于可视化体验编辑器的建议，包括 `renderAttempted` 标志设置为 `false`
* 基于可视化体验编辑器的建议，用于单页应用程序视图 `renderAttempted` 标志设置为 `false`

#### 在查看时 — 更改（对于缓存的视图）：

* 基于可视化体验编辑器的建议，用于单页应用程序视图 `renderAttempted` 标志设置为 `false`

### 单个配置文件更新

的 [!DNL Platform Web SDK] 允许您将用户档案更新为 [!DNL Target] 和 [!DNL Platform Web SDK] 作为体验事件。

要更新 [!DNL Target] 配置文件，请确保配置文件数据与以下内容一起传递：

* 在 `"data {"`
* 在 `"__adobe.target"`
* 前缀 `"profile."` 例如，如下所示

| 键 | 类型 | 描述 |
| --- | --- | --- |
| `renderDecisions` | 布尔值 | 指示个性化组件是否应解释DOM操作 |
| `decisionScopes` | 数组 `<String>` | 要检索决策的范围列表 |
| `xdm` | 对象 | 在XDM中格式化的数据，这些数据会作为体验事件进入Platform Web SDK中 |
| `data` | 对象 | 发送到的任意键/值对 [!DNL Target] 解决方案。 |

典型 [!DNL Platform Web SDK] 使用此命令的代码如下所示：

**`sendEvent`使用用户档案数据**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**如何将用户档案属性发送到Adobe Target:**

```js
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

下表列出 [!DNL Recommendations] 属性以及是否通过 [!DNL Platform Web SDK]:

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

```js
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## 调试

mboxTrace和mboxDebug已被弃用。 使用 [[!DNL Platform Web SDK] 调试](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## 术语

__建议：__ 在 [!DNL Target]，则命题会将与从活动中选择的体验相关联。

__架构：__ 决策的架构是 [!DNL Target].

__范围：__ 决定的范围。 在 [!DNL Target]，范围为mBox。 全局mBox是 `__view__` 范围。

__XDM:__ XDM将序列化为点符号，然后放入 [!DNL Target] 作为mBox参数。
