---
title: Adobe Target v2擴充功能概觀
description: 瞭解Adobe Experience Platform中的Adobe Target v2標籤擴充功能。
exl-id: 8f491d67-86da-4e27-92bf-909cd6854be1
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 61%

---

# Adobe Target v2擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

使用本参考可了解有关使用此扩展构建规则时可用的选项的信息。

## 配置 Adobe Target v2 扩展

>[!IMPORTANT]
>
>Adobe Target 扩展需要使用 At.js 2.x。

如果尚未安裝Adobe Target擴充功能，請開啟您的屬性，然後選取「 」 **[!UICONTROL 擴充功能>目錄]**，將游標暫留在Target擴充功能上，然後選取 **[!UICONTROL 安裝]**.

若要設定擴充功能，請開啟「擴充功能」標籤、將游標暫留在擴充功能上方，然後選取「 」 **[!UICONTROL 設定]**.

![](../../../images/targetv2config.png)

### at.js 设置

所有at.js設定（Timeout除外）都會自動從Target UI中的at.js設定中擷取。 擴充功能只會在其首次新增時從Target UI擷取設定，因此如有其他更新，應在UI中管理所有設定。

可以使用以下配置选项：

#### Client Code

使用者端代碼是Target的帳戶識別碼。 此选项几乎应始终保留为默认值。可使用資料元素加以變更。

#### Organization ID

此 ID 可将您的实施绑定到 Adobe Experience Cloud 帐户。此选项几乎应始终保留为默认值。可使用資料元素加以變更。

#### Server Domain

伺服器網域是指傳送Target要求的網域。 此选项几乎应始终保留为默认值。

#### GDPR Opt-In

如果启用此选项，Adobe Target 将提供选择启用功能，以帮助支持您的同意管理策略。选择启用功能让客户可自行决定如何以及何时触发 Target 标记。有关 Adobe 选择启用的更多信息，请参阅[隐私和一般数据保护条例  (GDPR)](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)。

#### Timeout (ms)

如果在定义的时间段内未收到来自 Target 的响应，则请求会超时并显示默认内容。在访客会话期间会继续尝试发起其他请求。默认值为 3000 毫秒，这可能与 Target 用户界面中配置的超时不同。

有关超时设置的工作方式的更多信息，请参阅 [Adobe Target 帮助](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/deploy-at-js/implementing-target-without-a-tag-manager.html)。

## Target 扩展操作类型

此部分介绍 Target 扩展中可用的操作类型。

Target 扩展在规则的 Then 部分中提供了以下操作：

### Load Target

將此動作新增至您的標籤規則，其中在此規則的內容中載入Target是可行的。 这会将 at.js 库加载到页面中。在大多数实施中，应在您网站的每个页面上加载 Target。Adobe 建议，仅在执行 Target 调用之后再使用“加载 Target”操作。否则，您可能会遇到 Analytics 调用延迟等问题。

无需进行配置。

### 使用裝置上決策載入Target

將此動作新增至您的標籤規則，其中載入Target是可行的 [裝置上決策](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/on-device-decisioning/on-device-decisioning.html) 已在規則內容中啟用。 這會將at.js程式庫載入頁面，並啟用裝置上決策。 在大多数实施中，应在您网站的每个页面上加载 Target。Adobe建議，您必須先執行Target呼叫，才能將「載入Target」與「裝置上決策」動作搭配使用。 否则，您可能会遇到 Analytics 调用延迟等问题。

无需进行配置。

### Add Params to All Requests

此動作型別可讓引數新增至所有Target請求。 必须先使用 Load Target 操作。

1. 指定要添加的任意参数的名称和值。
1. 选择添加图标可添加更多参数。

### Add Params to Page Load Request

此動作型別可專門將引數新增至頁面載入請求。 必须先使用 Load Target 操作。

1. 指定要添加的任意参数的名称和值。
1. 选择添加图标可添加更多参数。

### 触发页面加载请求

此動作型別可讓Target在頁面載入時觸發要求。 必须先使用 Load Target 操作。

您必須指定是否啟用主體隱藏以防止閃爍，以及隱藏主體元素時所使用的樣式。 可以使用以下选项：

* **Body Hiding：**&#x200B;您可以启用或禁用此设置。默认值为 Enabled，表示隐藏 HTML 主体。
* **Body Hidden Style：**&#x200B;默认值为 body{opacity:0}。此值可更改为其他内容，如 body{display:none}。

有关更多信息，请参阅 [Target 联机帮助文档](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/advanced-mboxjs-settings.html)。

### Trigger View

每當載入新頁面或重新呈現頁面上的元件時，都可以呼叫「觸發檢視」動作。 應為單頁應用程式實作觸發器檢視。

1. 指定必须触发的视图名称。
1. 通过选中 Page 复选框，指定是否应将视图触发归因于要报告的展示。如果视图与重新渲染的组件相关，而不归因于要报告的展示，则应将 Page 复选框保留为取消选中状态。

有关触发视图的更多信息，请参阅[`triggerView()`帮助文档](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/functions-overview/adobe-target-triggerview-atjs-2.html)。

## Adobe Target 基本部署

安装 Target 扩展后，需创建至少一个规则才能正确部署该扩展。您首先需要加载 Target 库 (at.js)，指定要用于页面加载请求的参数，然后触发页面加载请求。

具有此基本实施的 Target 规则如下所示：

![](../../../images/targetv2deploy.png)

儲存此規則後，您需要將其新增至程式庫，然後進行建置/部署，以便測試行為。

## 使用异步部署的 Adobe Target 扩展

標籤可非同步部署。 如果您以非同步方式載入標籤程式庫，且其中包含Target，則Target也會以非同步方式載入。 这是一个完全支持的方案，但有一个额外的注意事项必须加以处理。

在异步部署中，页面可能会在 Target 库完全加载并执行内容交换之前完成默认内容渲染。这可能会导致所谓的“闪烁”，在这种情况下，会先短暂显示默认内容，然后再将该内容替换为 Target 指定的个性化内容。若要避免這種閃爍問題，建議您使用預先隱藏的程式碼片段，然後非同步載入標籤套件組合，以避免任何內容閃爍。

在使用预隐藏代码片段时，请谨记以下事项：

* 載入標籤標頭內嵌程式碼之前，必須先新增程式碼片段。
* 標籤無法管理此程式碼，因此必須直接新增至頁面。
* 当发生以下事件时（以最先发生者为准），将显示该页面：
   * 收到页面加载响应
   * 页面加载请求超时
   * 代码片段本身超时
* 應使用預先隱藏程式碼片段，在所有頁面上使用「引發頁面載入請求」動作，以將預先隱藏的時間減至最少。
* 您也必須在Target使用的頁面載入規則的「頁面載入請求」動作中啟用內文隱藏功能；否則，所有頁面載入會在逾時期間保持隱藏狀態。

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
