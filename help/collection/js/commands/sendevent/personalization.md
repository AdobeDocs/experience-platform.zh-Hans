---
title: 个性化
description: 向不同的用户呈现不同的内容，为他们创建个性化体验。
exl-id: 4bd370c8-8d8d-469e-9666-b5b6d0e3a660
source-git-commit: 54cd49bc1e6f23e3fb6d539274ea16d36ea21386
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---

# `personalization`

`personalization`对象配置请求哪些个性化决策（优惠或建议），以及如何在请求和响应中处理这些决策。 它在Adobe Target或Adobe Journey Optimizer实施中特别有用，因为它是允许您按用户自定义显示内容的驱动力。

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["hero-banner"],
    surfaces: ["web://example.com"],
    schemas: ["https://ns.adobe.com/personalization/dom-action"],
    sendDisplayEvent: true,
    sendDisplayNotifications: true,
    includePendingDisplayNotifications: true,
    defaultPersonalizationEnabled: false
  },
  renderDecisions: true,
  xdm: adobeDataLayer.getState(reference)
});
```

`personalization`对象包含以下属性：

## `personalization.decisionScopes`

`decisionScopes`属性是一个字符串数组，它指示Web SDK检索并返回个性化决策。 数组中的每个项目标识需要个性化内容的位置、上下文或逻辑位置。

当您想要显式获取页面特定区域或组件的个性化内容时，此属性很有用。 在需要随着用户的导航或视图更改而设置不同选件集的单页应用程序中，此选项特别有用。 您还可以使用此属性通过仅检索与用户相关的UI元素的选件来优化性能。

```js
personalization: {
  decisionScopes: ["hero-banner", "cart-offer"]
}
```

在Adobe Target中，每个决策范围都映射到mbox或活动。 在Adobe Journey Optimizer中，每个决策范围都映射到基于决策的Web内容投放或营销活动。 在Offer Decisioning中，决策范围映射到访客应收到的选件或建议。

>[!TIP]
>
>如果要请求（或阻止）全局范围，请使用[`defaultPersonalizationEnabled`](#personalizationdefaultpersonalizationenabled)，而不是在`decisionScopes`中在此处指定它。

## `personalization.surfaces`

`surfaces`属性是[表面URI](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/channels/code-based-experience/configure-code-based-channel/code-based-surface#surface-uri)字符串的数组，这些字符串手动定义从中请求个性化的渠道、设备或上下文。 它们允许您区分不同的数字体验，例如跨渠道生态系统内的域、应用程序或设备平台。 默认情况下，库推断来自当前页面的缺省曲面。 可以使用此属性覆盖当前页面的自动推断表面。

当您想要使用跨渠道个性化并且必须区分个性化在单独的渠道之间的工作方式时，此属性很有价值。 它允许您为同一Adobe Experience Platform组织下的不同站点创建不同的选件。

```js
personalization: {
  surfaces: ["web://example.com", "web://support.example.com/contact"]
}
```

此属性基本与Adobe Journey Optimizer一起使用，因为它与Journey Optimizer营销活动和表面管理中设置的表面相匹配。

## `personalization.schemas`

`schemas`属性是一个架构URI字符串数组，用于筛选从Edge Network请求的个性化内容类型。 设置此属性可限制您从Adobe收到的响应，使其仅包含与您指定的内容类型定义匹配的选件。 如果忽略，则库将请求匹配范围或表面的所有可用架构的选件。

此属性有助于优化响应大小，并确保您的网站或应用程序仅接收它可处理的选件类型。 当与以特定方式呈现个性化内容的单页应用程序一起使用时（例如仅使用DOM操作或仅使用JSON对象），此功能也非常有用。

```js
personalization: {
  schemas: [
    "https://ns.adobe.com/personalization/dom-action",
    "https://ns.adobe.com/personalization/html-content-item"
  ]
}
```

支持以下架构URI：

* **`https://ns.adobe.com/personalization/dom-action`**：直接DOM操作的选件，通常由Adobe Target中的可视化体验编辑器生成。 它们包含无需其他代码即可自动处理页面上元素的说明。 它是自动渲染Web个性化的标准。
* **`https://ns.adobe.com/personalization/html-content-item`**：包含作为字符串交付的原始HTML的选件。 您的实施通常将此内容插入到页面上的所需位置，从而使您比DOM操作拥有更大的控制权。 通常用于横幅、代码片段或模态内容。
* **`https://ns.adobe.com/personalization/json-content-item`**：格式为JSON对象的选件。 最常用于基于API的实施或预期结构化数据而不是HTML或DOM更改的前端。
* **`https://ns.adobe.com/personalization/redirect-item`**：重定向到其他URL的选件。 用于根据定位或决策逻辑（如登陆页面或载入流程）将用户引导至新页面。
* **`https://ns.adobe.com/personalization/ruleset-item`**：提供业务逻辑块以支持客户端规则引擎。 包含定义逻辑条件和结果（if/then个性化逻辑）的版本化规则集。
* **`https://ns.adobe.com/personalization/message/in-app`**：专门为Adobe Journey Optimizer应用程序内消息设置格式的选件，通常呈现为模式、横幅、弹出窗口或叠加图。
* **`https://ns.adobe.com/personalization/message/content-card`**：专门针对Adobe Journey Optimizer内容卡格式化的、专门为Web或移动应用程序中的持久性或收件箱式馈送设计的选件。
* **`https://ns.adobe.com/personalization/message/native-alert`**：专门为Adobe Journey Optimizer本机警报设置格式的选件，触发平台本机通知对话框。
* **`https://ns.adobe.com/personalization/measurement`**：用于跟踪对个性化优惠的点击和交互。 不包含可渲染的内容。
* **`https://ns.adobe.com/personalization/eventHistoryOperation`**：用于更改本地存储中访客的事件历史记录的架构。 供SDK内部用于跟踪已交付或阻止的体验。 不包含可渲染的内容。
* **`https://ns.adobe.com/personalization/default-content-item`**：回退或默认内容，通常在没有个性化优惠合格时。 它可确保不符合条件的用户仍会收到内容，并保持一致的体验。

## `personalization.sendDisplayEvent`

`sendDisplayEvent`属性是一个布尔值，用于确定在页面上呈现个性化内容后是否立即将显示通知事件自动发送到Edge Network。 如果忽略，则其默认值为`true`。 如果您不想指示已针对展示跟踪呈现个性化内容，请将此变量设置为`false`。

将此变量设置为`false`的最常见用例是当您计划在实施中的其他位置发送另一个标记显示事件的命令时。 某些实施同时具有展示次数和Analytics事件；此属性可让您完全控制哪些`sendEvent`命令递增展示次数。

```js
personalization: {
  sendDisplayEvent: true
}
```

>[!NOTE]
>
>Web SDK的早期版本（版本2.12.0及更早版本）使用`sendDisplayNotifications`。

## `personalization.includePendingDisplayNotifications`

`includePendingDisplayNotifications`属性是一个布尔值，它控制当前`sendEvent`调用中是否捆绑了任何挂起的显示通知。 待处理显示通知是已渲染但尚未作为显示事件报告给Edge Network的个性化内容的展示次数。 当使用单页应用程序时，此属性非常有用，因为呈现个性化内容和`sendEvent`调用可能相互异步。

此属性的默认值为`false`。 如果要批处理并刷新任何待处理的显示通知，以便准确记录其展示次数，请将此属性设置为`true`。 同步实施（如传统网站）通常不需要设置此属性。

```js
personalization: {
  includePendingDisplayNotifications: true
}
```

## `personalization.defaultPersonalizationEnabled`

`defaultPersonalizationEnabled`属性是一个布尔值，用于显式控制Web SDK如何请求此`__view__`命令的默认全页个性化范围(`sendEvent`)和表面。 默认情况下，在页面加载后的第一个`sendEvent`命令上，Web SDK请求提供默认页面范围的个性化范围和关联的界面。 后续`sendEvent`命令不请求默认个性化。 您可以使用此属性来覆盖该行为。 它在单页应用程序实施中非常有用，您可以在实施中在用户浏览网站时再次请求默认个性化。 当您希望&#x200B;_仅_&#x200B;发送显示事件而不复制选件检索时，也可以使用此属性。

```js
personalization: {
  defaultPersonalizationEnabled: false
}
```

此属性会根据其设置方式使用以下逻辑：

* **未设置**：在尚未请求默认个性化时，请求默认个性化。 通常在页面加载后的前`sendEvent`个页面上请求默认个性化，然后在同一页面上的后续`sendEvent`调用中不再请求默认个性化。 设置此属性将覆盖此行为。
* **`true`**：显式请求页面范围和默认表面，即使此`sendEvent`命令不是页面加载后的第一个命令。 将此属性设置为`true`的理想时机是您需要强制使用默认个性化请求，如在单页应用程序场景中。
* **`false`**：显式禁止对页面范围和默认表面的请求，即使此`sendEvent`命令是页面加载后的第一个命令也是如此。 将此属性设置为`false`的理想时机是，您希望给定的`sendEvent`命令不要请求新优惠，而只是将数据发送到Analytics或发送显示事件。

## 使用Web SDK标记扩展的Personalization组件

在配置“[**[!UICONTROL Personalization]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields)”操作时，此属性的Web SDK标记扩展等效项是[!UICONTROL Send event]部分。
