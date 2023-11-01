---
title: 将Adobe Target与Platform Web SDK一起使用
description: 了解如何使用Adobe Target通过Experience PlatformWeb SDK呈现个性化内容
keywords: target；adobe target；activity.id；experience.id；renderDecisions；decisionScopes；预隐藏代码片段；vec；基于表单的体验编辑器；xdm；受众；决策；范围；架构；系统图；图
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 6%

---

# 使用 [!DNL Adobe Target] 使用 [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] 可以投放和渲染在中管理的个性化体验 [!DNL Adobe Target] 到Web渠道。 您可以使用WYSIWYG编辑器，称为 [可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC)或非可视化界面， [基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)，创建、激活和交付您的活动和个性化体验。

>[!IMPORTANT]
>
>了解如何使用将Target实施迁移到Platform Web SDK [将Target从at.js 2.x迁移到Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html) 教程。
>
>了解如何使用首次实施Target [利用Web SDK实施Adobe Experience Cloud](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hans) 教程。 有关特定于Target的信息，请参阅名为的教程部分 [使用Platform Web SDK设置Target](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).


以下功能已经过测试，当前在中受支持 [!DNL Target]：

* [A/B测试](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T展示和转化报表](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization活动](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [体验定位活动](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [多变量测试(MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations 活动](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [原生Target展示和转化报表](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC支持](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] 系统图

下图可帮助您了解的工作流 [!DNL Target] 和 [!DNL Platform Web SDK] edge decisioning.

![使用Platform Web SDK的Adobe Target Edge Decisioning示意图](./assets/target-platform-web-sdk.png)

| 调用 | 详细信息 |
| --- | --- |
| 1 | 设备加载 [!DNL Platform Web SDK]. 此 [!DNL Platform Web SDK] 使用XDM数据、数据流环境ID、传入参数和客户ID（可选）向边缘网络发送请求。 页面（或容器）已预先隐藏。 |
| 2 | 边缘网络将请求发送到边缘服务，以使用访客ID、同意和其他访客上下文信息（如地理位置和设备友好名称）扩充其内容。 |
| 3 | 边缘网络将扩充的个性化请求发送至 [!DNL Target] 使用访客ID和传入的参数进行Edge。 |
| 4 | 配置文件脚本先执行，然后注入到 [!DNL Target] 配置文件存储。 配置文件存储从获取区段 [!UICONTROL 受众库] (例如，从共享区段 [!DNL Adobe Analytics]， [!DNL Adobe Audience Manager]， [!DNL Adobe Experience Platform])。 |
| 5 | 根据URL请求参数和配置文件数据， [!DNL Target] 确定可为访客显示的当前页面视图和未来预取视图的活动和体验。 [!DNL Target] 然后将它发回到edge network。 |
| 6 | a.边缘网络将个性化响应发送回页面，其中可能包含其他个性化的配置文件值。 当前页面上的个性化内容会在默认内容不发生闪烁的情况下尽快显示。<br>b.作为用户操作在单页应用程序(SPA)中显示的视图的个性化内容将缓存，这样便可在触发视图时即时应用而无需额外的服务器调用。 <br>c.边缘网络发送访客ID和Cookie中的其他值，如同意、会话ID、身份、Cookie检查、个性化等等。 |
| 7 | 边缘网络转发 [!UICONTROL 目标分析] (A4T)的详细信息（活动、体验和转化元数据） [!DNL Analytics] 边缘。 |

## 正在启用 [!DNL Adobe Target]

要启用 [!DNL Target]，请执行以下操作：

1. 启用 [!DNL Target] 在您的 [数据流](../../../datastreams/overview.md) ，并提供相应的客户端代码。
1. 添加 `renderDecisions` 选项添加到您的事件。

然后，您还可以选择添加以下选项：

* **`decisionScopes`**：通过将此选项添加到您的事件中，检索特定活动（对于使用基于表单的编辑器创建的活动非常有用）。
* **[预隐藏代码片段](../manage-flicker.md)**：仅隐藏页面的某些部分。

## 使用Adobe Target VEC

要将VEC与 [!DNL Platform Web SDK] 实施，安装并激活 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 或 [铬黄](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC助手扩展。

有关更多信息，请参阅 [可视化体验编辑器助手扩展](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) 在 *Adobe Target指南*.

## 呈现个性化内容

请参阅 [呈现个性化内容](../rendering-personalization-content.md) 以了解更多信息。

## XDM中的受众

在为定义受众时 [!DNL Target] 通过交付的活动 [!DNL Platform Web SDK]， [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html) 必须定义和使用。 定义XDM架构、类和架构字段组后，您可以创建 [!DNL Target] 由XDM数据定义的用于定位的受众规则。 范围 [!DNL Target]， XDM数据显示在 [!UICONTROL Audience Builder] 作为自定义参数。 XDM使用点表示法序列化(例如， `web.webPageDetails.name`)。

如果您拥有 [!DNL Target] 如果活动包含使用自定义参数或用户配置文件的预定义受众，则无法通过SDK正确交付这些活动。 您必须改用XDM，而不是使用自定义参数或用户配置文件。 但是，提供开箱即用的受众定位字段，支持它们通过 [!DNL Platform Web SDK] 而不需要XDM。 这些字段在 [!DNL Target] 不需要XDM的UI：

* 定位库
* 地域
* 网络
* 操作系统
* 站点页面
* 浏览器
* 流量源
* 时间范围

有关更多信息，请参阅 [受众类别](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html) 在 *Adobe Target指南*.

### 响应令牌

响应令牌主要用于向Google、Facebook等第三方发送元数据。 响应令牌在中返回 `meta` 字段范围 `propositions` -> `items`. 以下是示例：

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

要收集响应令牌，您必须订阅 `alloy.sendEvent` 承诺，反复访问 `propositions`
并从中提取详细信息 `items` -> `meta`. 每 `proposition` 具有 `renderAttempted` 布尔字段，指示是否 `proposition` 是否呈现。 请参阅下面的示例：

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

启用自动渲染时，建议数组包含：

#### 在页面加载时：

* 基于表单的编辑器 `propositions` 替换为 `renderAttempted` 标志设置为 `false`
* 基于可视化体验编辑器的建议，具有 `renderAttempted` 标志设置为 `true`
* 基于可视化体验编辑器的单页应用程序视图建议 `renderAttempted` 标志设置为 `true`

#### 查看时 — 更改（对于缓存的视图）：

* 基于可视化体验编辑器的单页应用程序视图建议 `renderAttempted` 标志设置为 `true`

禁用自动渲染时，建议数组包含：

#### 在页面加载时：

* 基于表单的编辑器 `propositions` 替换为 `renderAttempted` 标志设置为 `false`
* 基于可视化体验编辑器的建议，具有 `renderAttempted` 标志设置为 `false`
* 基于可视化体验编辑器的单页应用程序视图建议 `renderAttempted` 标志设置为 `false`

#### 查看时 — 更改（对于缓存的视图）：

* 基于可视化体验编辑器的单页应用程序视图建议 `renderAttempted` 标志设置为 `false`

### 单个配置文件更新

此 [!DNL Platform Web SDK] 允许您将配置文件更新到 [!DNL Target] 配置文件和 [!DNL Platform Web SDK] 作为体验事件。

要更新 [!DNL Target] 配置文件时，请确保使用以下各项来传递配置文件数据：

* 在 `"data {"`
* 在 `"__adobe.target"`
* 前缀 `"profile."` 例如，如下所示

| 键 | 类型 | 描述 |
| --- | --- | --- |
| `renderDecisions` | 布尔值 | 指示个性化组件是否应解释DOM操作 |
| `decisionScopes` | 数组 `<String>` | 要检索决策的作用域列表 |
| `xdm` | 对象 | 采用XDM格式的数据，以体验事件形式登陆Platform Web SDK |
| `data` | 对象 | 发送到的任意键/值对 [!DNL Target] 目标类下的解决方案。 |

典型 [!DNL Platform Web SDK] 使用此命令的代码如下所示：

**`sendEvent`包含配置文件数据**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**如何将配置文件属性发送到Adobe Target：**

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

## 请求建议

下表列出了 [!DNL Recommendations] 属性以及是否通过 [!DNL Platform Web SDK]：

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
| 类别亲和度的页面或物料类别 | user.categoryId | 受支持 |

**如何将Recommendations属性发送到Adobe Target：**

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

已弃用mboxTrace和mboxDebug。 使用 [[!DNL Platform Web SDK] 调试](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## 术语

__建议：__ 在 [!DNL Target]，建议与从活动中选择的体验相关联。

__架构：__ 决策的结构是中的优惠类型 [!DNL Target].

__范围：__ 决定的范围。 在 [!DNL Target]，范围是mBox。 全局mBox是 `__view__` 范围。

__XDM：__ XDM将序列化为点表示法，然后放入 [!DNL Target] 作为mBox参数。
