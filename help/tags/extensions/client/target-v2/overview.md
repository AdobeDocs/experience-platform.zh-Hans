---
title: Adobe Target v2扩展概述
description: 了解Adobe Experience Platform中的Adobe Target v2标记扩展。
exl-id: 8f491d67-86da-4e27-92bf-909cd6854be1
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1298'
ht-degree: 60%

---

# Adobe Target v2扩展概述

使用本参考可了解有关使用此扩展构建规则时可用的选项的信息。

## 配置 Adobe Target v2 扩展

>[!IMPORTANT]
>
>Adobe Target 扩展需要使用 At.js 2.x。

如果尚未安装 Adobe Target 扩展，请打开您的资产，接下来选择 **[!UICONTROL Extensions > Catalog]**，将鼠标悬停在 Target 扩展上，然后选择 **[!UICONTROL Install]**。

要配置该扩展，请打开 Extensions 选项卡，将鼠标悬停在该扩展上，然后选择 **[!UICONTROL Configure]**。

![](../../../images/targetv2config.png)

### at.js 设置

所有at.js设置（Timeout除外）将自动从Target UI的at.js配置中进行检索。 该扩展仅在首次添加时才会从Target UI中检索设置，因此如果需要进行其他更新，则应在UI中管理所有设置。

可以使用以下配置选项：

#### Client Code

客户端代码是Target的帐户标识符。 此值几乎应始终保留为默认值。 可使用数据元素对其进行更改。

#### Organization ID

此 ID 可将您的实施绑定到 Adobe Experience Cloud 帐户。此值几乎应始终保留为默认值。 可使用数据元素对其进行更改。

#### Server Domain

服务器域是指发送Target请求的域。 此选项几乎应始终保留为默认值。

#### GDPR Opt-In

如果启用此选项，Adobe Target 将提供选择启用功能，以帮助支持您的同意管理策略。选择启用功能让客户可自行决定如何以及何时触发 Target 标记。有关 Adobe 选择启用的更多信息，请参阅[隐私和一般数据保护条例  (GDPR)](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=zh-Hans)。

#### Timeout (ms)

如果在定义的时间段内未收到来自 Target 的响应，则请求会超时并显示默认内容。在访客会话期间会继续尝试发起其他请求。默认值为 3000 毫秒，这可能与 Target 用户界面中配置的超时不同。

有关超时设置的工作方式的更多信息，请参阅 [Adobe Target 帮助](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/deploy-at-js/implementing-target-without-a-tag-manager.html?lang=zh-Hans)。

## Target 扩展操作类型

此部分介绍 Target 扩展中可用的操作类型。

Target 扩展在规则的 Then 部分中提供了以下操作：

### Load Target

将此操作添加到适合在上下文中加载Target的标记规则中。 这会将 at.js 库加载到页面中。在大多数实施中，应在您网站的每个页面上加载 Target。Adobe 建议，仅在执行 Target 调用之后再使用“加载 Target”操作。否则，您可能会遇到 Analytics 调用延迟等问题。

无需进行配置。

### 通过设备上决策加载Target

将此操作添加到标记规则中，其中加载在规则上下文中启用[设备上决策](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/on-device-decisioning/on-device-decisioning.html?lang=zh-Hans)的Target是可行的。 此操作会将启用了设备上决策的at.js库加载到页面中。 在大多数实施中，应在您网站的每个页面上加载 Target。Adobe建议，仅在执行Target调用之后再结合使用“Load Target与设备上决策”操作。 否则，您可能会遇到 Analytics 调用延迟等问题。

>[!IMPORTANT]
>
>仅将页面加载请求与设备上决策结合使用（如果已配置）。 将此操作添加到规则将增加最终Launch捆绑包的大小，因为它包含设备上决策规则引擎。

### 向所有请求添加参数

此操作类型允许将参数添加到所有Target请求。 必须先使用 Load Target 操作。

1. 指定要添加的任意参数的名称和值。
1. 选择添加图标可添加更多参数。

### Add Params to Page Load Request

此操作类型允许专门向页面加载请求添加参数。 必须先使用 Load Target 操作。

1. 指定要添加的任意参数的名称和值。
1. 选择添加图标可添加更多参数。

### 触发页面加载请求

此操作类型允许Target在页面加载时触发请求。 必须先使用 Load Target 操作。

必须指定是否启用主体隐藏以防止闪烁，以及在隐藏主体元素时使用的样式。 可以使用以下选项：

* **Body Hiding：**&#x200B;您可以启用或禁用此设置。默认值为 Enabled，表示隐藏 HTML 主体。
* **Body Hidden Style：**&#x200B;默认值为body{opacity:0}。 此值可更改为其他内容，如body{display:none}。

有关更多信息，请参阅 [Target 联机帮助文档](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/advanced-mboxjs-settings.html?lang=zh-Hans)。

### Trigger View

每当加载新页面或重新呈现页面上的组件时，都可以调用Trigger View操作。 应为单页应用程序实施触发器视图。

1. 指定必须触发的视图名称。
1. 通过选中 Page 复选框，指定是否应将视图触发归因于要报告的展示。如果视图与重新渲染的组件相关，而不归因于要报告的展示，则应将 Page 复选框保留为取消选中状态。

有关触发视图的更多信息，请参阅[`triggerView()`帮助文档](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/functions-overview/adobe-target-triggerview-atjs-2.html?lang=zh-Hans)。

## Adobe Target 基本部署

安装 Target 扩展后，需创建至少一个规则才能正确部署该扩展。您首先需要加载 Target 库 (at.js)，指定要用于页面加载请求的参数，然后触发页面加载请求。

具有此基本实施的 Target 规则如下所示：

![](../../../images/targetv2deploy.png)

保存此规则后，您需要将其添加到库并对其进行生成/部署，以便测试该行为。

## 使用异步部署的 Adobe Target 扩展

标记可以异步部署。 如果您异步加载包含Target的标记库，则也将会异步加载Target。 这是一个完全支持的方案，但有一个额外的注意事项必须加以处理。

在异步部署中，页面可能会在 Target 库完全加载并执行内容交换之前完成默认内容渲染。这可能会导致所谓的“闪烁”，在这种情况下，会先短暂显示默认内容，然后再将该内容替换为 Target 指定的个性化内容。如果要避免出现这种闪烁情况，我们建议您使用预隐藏代码片段并异步加载标记包来避免任何内容闪烁。

在使用预隐藏代码片段时，请谨记以下事项：

* 必须在加载标记页眉嵌入代码之前添加代码片段。
* 标记无法管理此代码，因此必须将其直接添加到页面。
* 当发生以下事件时（以最先发生者为准），将显示该页面：
   * 收到页面加载响应
   * 页面加载请求超时
   * 代码片段本身超时
* 应在所有使用预隐藏代码片段的页面上使用“Fire Page Load Request”操作，以最大程度地缩短预隐藏的持续时间。
* 您还必须在用于Target的页面加载规则的页面加载请求操作中启用主体隐藏；否则，所有页面加载在超时期间都将保持隐藏状态。

预隐藏代码片段如下所示，该代码片段可以缩小。可配置的选项位于末尾：

```js
;(function(win, doc, style, timeout) {
  var STYLE_ID = 'at-body-style';

  function getParent() {
    return doc.getElementsByTagName('head')[0];
  }

  function addStyle(parent, id, def) {
    if (!parent) {
      return;
    }

    var style = doc.createElement('style');
    style.id = id;
    style.innerHTML = def;
    parent.appendChild(style);
  }

  function removeStyle(parent, id) {
    if (!parent) {
      return;
    }

    var style = doc.getElementById(id);

    if (!style) {
      return;
    }

    parent.removeChild(style);
  }

  addStyle(getParent(), STYLE_ID, style);
  setTimeout(function() {
    removeStyle(getParent(), STYLE_ID);
  }, timeout);
}(window, document, "body {opacity: 0 !important}", 3000));
```

默认情况下，该代码片段会预先隐藏整个 HTML 主体。在某些情况下，您可能只想预先隐藏某些 HTML 元素，而不是整个页面。您可以通过自定义样式参数来实现这一点。可将其替换为只预先隐藏页面特定区域的内容。

例如，如果您有两个分别采用 ID container-1 和 container-2 进行标识的区域，则可以将样式替换为以下内容：

```css
#container-1, #container-2 {opacity: 0 !important}
```

而不是默认内容：

```css
body {opacity: 0 !important}
```

默认情况下，代码片段会在 3000 毫秒或 3 秒后超时。此值可进行自定义。
