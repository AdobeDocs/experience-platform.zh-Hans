---
title: 配置Adobe Experience Platform Web SDK
description: 了解如何配置Adobe Experience Platform Web SDK。
seo-description: Learn how to configure the Experience Platform Web SDK
keywords: 配置；配置；SDK；边缘；Web SDK；配置；edgeConfigId；上下文；Web；设备；placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;Web SDK设置；prehidingStyle;ocookieDestinationsEnable;urlDestinationsEnabled;idMigCookiesEnabled；第三方Cookies
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: a192a746fa227b658fcdb8caa07ea6fb4ac1a944
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 9%

---

# 配置平台Web SDK

SDK的配置已通过 `configure` 命令。

>[!IMPORTANT]
>
>`configure` is *always* 第一个命令名为。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

在配置过程中可以设置许多选项。 所有选项都可在下面找到，并按类别分组。

## 常规选项

### `edgeConfigId`

>[!NOTE]
>
>**边缘配置已重新命名为数据流。 数据流ID与配置ID相同。**

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 字符串 | 是 | None |

{style="table-layout:auto"}

您分配的配置ID，用于将SDK关联到相应的帐户和配置。 在单个页面中配置多个实例时，必须配置其他 `edgeConfigId` （对于每个实例）。

### `context` {#context}

| **类型** | 必需 | **默认值** |
| ---------------- | ------------ | -------------------------------------------------- |
| 字符串数组 | 否 | `["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]` |

{style="table-layout:auto"}

指示要自动收集的上下文类别，如 [自动信息](../data-collection/automatic-information.md). 如果未指定此配置，则默认使用所有类别。

>[!IMPORTANT]
>
>除 `highEntropyUserAgentHints`，则默认情况下处于启用状态。 如果您在Web SDK配置中手动指定上下文属性，则必须启用所有上下文属性才能继续收集所需的信息。

启用 [高熵客户端提示](user-agent-client-hints.md#enabling-high-entropy-client-hints) 在Web SDK部署中，您必须包含 `highEntropyUserAgentHints` 上下文选项，以及现有配置。

例如，要从Web属性中检索高熵客户端提示，您的配置将如下所示：

`context: ["highEntropyUserAgentHints", "web"]`


### `debugEnabled`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `false` |

{style="table-layout:auto"}

指示是否启用调试。 将此配置设置为 `true` 启用以下功能：

| **功能** | **函数** |
| ---------------------- | ------------------ |
| 控制台日志记录 | 允许在浏览器的JavaScript控制台中显示调试消息 |

{style="table-layout:auto"}

### `edgeDomain` {#edge-domain}

使用第一方域填充此字段。 有关更多详细信息，请参阅 [文档](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=zh-Hans).

域类似于 `data.{customerdomain.com}` 网站www.{customerdomain.com}。

### `edgeBasePath` {#edge-base-path}

用于与Adobe服务通信和交互的edgeDomain后面的路径。  通常，仅当不使用默认生产环境时，这种情况才会发生更改。

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 字符串 | 否 | ee |

{style="table-layout:auto"}

### `orgId`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 字符串 | 是 | None |

{style="table-layout:auto"}

您分配的 [!DNL Experience Cloud] 组织ID。 在一个页面中配置多个实例时，必须配置其他 `orgId` （对于每个实例）。

## 数据收集

### `clickCollectionEnabled` {#clickCollectionEnabled}

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style="table-layout:auto"}

指示是否自动收集与链接点击量关联的数据。 请参阅 [自动链接跟踪](../data-collection/track-links.md#automaticLinkTracking) 以了解更多信息。 如果链接包含下载属性或链接以文件扩展名结尾，则也会将其标记为下载链接。 下载链接限定符可以配置正则表达式。 默认值为 `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 函数 | 否 | ()=>未定义 |

{style="table-layout:auto"}

在发送每个事件之前，配置为其调用的回调。 具有字段的对象 `xdm` 将发送到回调。 要更改发送的内容，请修改 `xdm` 对象。 在回调函数中， `xdm` 对象已在event命令中传递了数据，并且自动收集了信息。 有关此回调的时间和示例的更多信息，请参阅 [全局修改事件](tracking-events.md#modifying-events-globally).

### `onBeforeLinkClickSend` {#onBeforeLinkClickSend}

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 函数 | 否 | ()=>未定义 |

{style="table-layout:auto"}

在发送每个链接点击跟踪事件之前，配置一个为其调用的回调。 回调会使用 `xdm`, `clickedElement`和 `data` 字段。

使用DOM元素结构过滤链接跟踪时，可以使用 `clickElement` 命令。 `clickedElement` 是已单击并封装父节点树的DOM元素节点。

要更改发送的数据，请修改 `xdm` 和/或 `data` 对象。 在回调函数中， `xdm` 对象已在event命令中传递了数据，并且自动收集了信息。

* 除 `false` 将允许该事件处理并发送回调。
* 如果回调返回 `false` 值时，将停止事件处理，且没有错误，并且不会发送事件。 此机制允许通过检查事件数据并返回来过滤掉某些事件 `false` 如果不应发送该事件。
* 如果回调引发异常，则将停止处理该事件，并且不会发送该事件。


## 隐私选项

### `defaultConsent` {#default-consent}

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 对象 | 否 | `"in"` |

{style="table-layout:auto"}

设置用户的默认同意。 如果尚未为用户保存同意首选项，则使用此设置。 其他有效值为 `"pending"` 和 `"out"`. 此默认值不会持久保留在用户的配置文件中。 用户的配置文件仅在 `setConsent` 调用。
* `"in"`:如果设置此设置或未提供任何值，则在未使用用户同意首选项的情况下继续工作。
* `"pending"`:设置此设置后，工作将排入队列，直到用户提供同意首选项为止。
* `"out"`:设置此设置后，将丢弃工作，直到用户提供同意首选项为止。
在提供用户的首选项后，根据用户的首选项继续或中止工作。 请参阅 [支持同意](../consent/supporting-consent.md) 以了解更多信息。

## 个性化选项 {#personalization}

### `prehidingStyle` {#prehidingStyle}

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 字符串 | 否 | None |

{style="table-layout:auto"}

用于创建CSS样式定义，当从服务器加载个性化内容时，该定义会隐藏网页的内容区域。 如果未提供此选项，则SDK在加载个性化内容时不会尝试隐藏任何内容区域，这可能会导致“闪烁”。

例如，如果网页上的某个元素的ID为 `container`，当您从服务器加载个性化内容时要隐藏的默认内容，请使用以下预隐藏样式：

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

### `targetMigrationEnabled` {#targetMigrationEnabled}

从迁移单个页面时，应使用此选项 [!DNL at.js] 到Web SDK。

使用此选项可启用Web SDK以读取和写入旧版 `mbox` 和 `mboxEdgeCluster` 由 [!DNL at.js]. 这有助于您在从使用Web SDK的页面移动到使用 [!DNL at.js] 图书馆，反之亦然。

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `false` |

## 受众选项

### `cookieDestinationsEnabled`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style="table-layout:auto"}

启用 [!DNL Audience Manager] cookie目标，允许根据区段鉴别来设置cookie。

### `urlDestinationsEnabled`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style="table-layout:auto"}

启用 [!DNL Audience Manager] URL目标，允许根据区段鉴别触发URL。

## 身份选项

### `idMigrationEnabled` {#id-migration-enabled}

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style="table-layout:auto"}

如果为true，则SDK会读取并设置旧的AMCV Cookie。 此选项有助于过渡到使用Adobe Experience Platform Web SDK，而网站的某些部分可能仍使用Visitor.js。

如果页面上定义了访客API，SDK将查询访客API以获取ECID。 此选项允许您使用Adobe Experience Platform Web SDK创建双标记页面，但仍然具有相同的ECID。

### `thirdPartyCookiesEnabled`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style="table-layout:auto"}

启用Adobe第三方Cookie的设置。 SDK可以在第三方上下文中保留访客ID，以便允许在网站之间使用相同的访客ID。 如果您有多个网站，或者希望与合作伙伴共享数据，请使用此选项；但是，有时出于隐私原因不需要此选项。
