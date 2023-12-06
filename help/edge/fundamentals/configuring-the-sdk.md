---
title: 配置Adobe Experience Platform Web SDK
description: 了解如何配置Adobe Experience Platform Web SDK。
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 8%

---


# 配置Web SDK

SDK的配置已完成 `configure` 命令。

>[!IMPORTANT]
>
>`configure` 是 *始终* 第一个命令名为。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

配置期间可以设置许多选项。 所有选项都可以在下面找到，按类别分组。

## 常规选项

### `edgeConfigId`

>[!NOTE]
>
>**Edge Configurations已更名为数据流。 数据流ID与配置ID相同。**

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 字符串 | 是 | None |

{style="table-layout:auto"}

您分配的配置ID，用于将SDK链接到相应的帐户和配置。 在单个页面中配置多个实例时，必须配置不同的 `edgeConfigId` 针对每个实例。

### `context` {#context}

| **类型** | 必需 | **默认值** |
| ---------------- | ------------ | -------------------------------------------------- |
| 字符串数组 | 否 | `["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]` |

{style="table-layout:auto"}

指示要自动收集的上下文类别，如中所述 [自动信息](../data-collection/automatic-information.md). 如果未指定此配置，则默认使用所有类别。

>[!IMPORTANT]
>
>所有上下文属性，除 `highEntropyUserAgentHints`，默认情况下处于启用状态。 如果您在Web SDK配置中手动指定了上下文属性，则必须启用所有上下文属性以继续收集所需信息。

要启用 [高熵客户端提示](user-agent-client-hints.md#enabling-high-entropy-client-hints) 在Web SDK部署中，您必须包含其他 `highEntropyUserAgentHints` 上下文选项，以及您的现有配置。

例如，要从Web属性检索高熵客户端提示，您的配置将如下所示：

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

使用您的第一方域填充此字段。 欲知更多详情，请参见 [文档](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=zh-Hans).

该域类似于 `data.{customerdomain.com}` 在www上创建一个网站。{customerdomain.com}。

### `edgeBasePath` {#edge-base-path}

用于与Adobe服务通信和交互的edgeDomain之后的路径。  通常，只有在不使用默认生产环境时，此更改才会更改。

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 字符串 | 否 | ee |

{style="table-layout:auto"}

### `orgId`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 字符串 | 是 | None |

{style="table-layout:auto"}

您分配的 [!DNL Experience Cloud] 组织ID。 在页面中配置多个实例时，必须配置不同的 `orgId` 针对每个实例。

## 数据收集

### `clickCollectionEnabled` {#clickCollectionEnabled}

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style="table-layout:auto"}

指示是否自动收集与链接点击关联的数据。 请参阅 [自动链接跟踪](../data-collection/track-links.md#automaticLinkTracking) 以了解更多信息。 如果链接包含下载属性或以文件扩展名结尾，则也会将其标记为下载链接。 可使用正则表达式配置下载链接限定符。 默认值为 `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 函数 | 否 | () =>未定义 |

{style="table-layout:auto"}

配置在发送之前为每个事件调用的回调。 包含字段的对象 `xdm` 被发送到回调。 要更改发送的内容，请修改 `xdm` 对象。 在回调内部， `xdm` 对象已具有在event命令中传递的数据，以及自动收集的信息。 有关此回调时间及示例的更多信息，请参阅 [全局修改事件](tracking-events.md#modifying-events-globally).

### `onBeforeLinkClickSend` {#onBeforeLinkClickSend}

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 函数 | 否 | () =>未定义 |

{style="table-layout:auto"}

配置在发送之前为每个链接点击跟踪事件调用的回调。 回调发送一个对象，该对象具有 `xdm`， `clickedElement`、和 `data` 字段。

使用DOM元素结构过滤链接跟踪时，您可以使用 `clickElement` 命令。 `clickedElement` 是已单击并已封装父节点树的DOM元素节点。

要更改发送的数据，请修改 `xdm` 和/或 `data` 对象。 在回调内部， `xdm` 对象已具有在event命令中传递的数据，以及自动收集的信息。

* 除以外的任何值 `false` 允许处理事件并发送回调。
* 如果回调返回 `false` 值，事件处理将停止，并且不会出现错误，并且不会发送事件。 此机制允许通过检查事件数据并返回来过滤某些事件 `false` 如果不应发送该事件。
* 如果回调引发异常，则停止处理事件，并且不发送事件。


## 隐私选项

### `defaultConsent` {#default-consent}

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 对象 | 否 | `"in"` |

{style="table-layout:auto"}

设置用户的默认同意。 当尚未为用户保存同意首选项时，使用此设置。 其他有效值为 `"pending"` 和 `"out"`. 此默认值不会保留在用户配置文件中。 仅当出现以下情况时，才会更新用户配置文件 `setConsent` 称为。
* `"in"`：如果设置此设置或未提供值，则无需用户同意首选项即可继续工作。
* `"pending"`：设置此设置后，工作将排入队列，直到用户提供同意首选项。
* `"out"`：设置此设置后，将放弃工作，直到用户提供同意首选项为止。
提供用户的首选项后，工作会根据用户的首选项进行或中止。 请参阅 [支持同意](../consent/supporting-consent.md) 以了解更多信息。

## 个性化选项 {#personalization}

### `prehidingStyle` {#prehidingStyle}

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 字符串 | 否 | None |

{style="table-layout:auto"}

用于创建在从服务器加载个性化内容时隐藏网页内容区域的CSS样式定义。 如果未提供此选项，则SDK在加载个性化内容时不会尝试隐藏任何内容区域，这可能会导致“闪烁”。

例如，如果网页上的某个元素的ID为 `container`，在从服务器加载个性化内容时想要隐藏其默认内容，请使用以下预隐藏样式：

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

### `targetMigrationEnabled` {#targetMigrationEnabled}

从迁移单个页面时应使用此选项 [!DNL at.js] 到Web SDK。

使用此选项可使Web SDK能够读写旧版 `mbox` 和 `mboxEdgeCluster` 使用的Cookie [!DNL at.js]. 这有助于您在从使用Web SDK的页面移动到使用 [!DNL at.js] 库或反之。

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `false` |

## 受众选项

### `cookieDestinationsEnabled`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style="table-layout:auto"}

启用 [!DNL Audience Manager] Cookie目标，用于根据区段鉴别设置Cookie。

### `urlDestinationsEnabled`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style="table-layout:auto"}

启用 [!DNL Audience Manager] URL目标，允许根据区段鉴别触发URL。

## 标识选项

### `idMigrationEnabled` {#id-migration-enabled}

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style="table-layout:auto"}

如果为true，则SDK会读取并设置旧的AMCV Cookie。 当网站的某些部分可能仍使用Visitor.js时，此选项可帮助转换为使用Adobe Experience Platform Web SDK。

如果页面上定义了访客API，则SDK会查询访客API以获取ECID。 通过此选项，您可以使用Adobe Experience Platform Web SDK对页面进行双重标记，同时仍然具有相同的ECID。

### `thirdPartyCookiesEnabled`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style="table-layout:auto"}

启用Adobe第三方Cookie的设置。 SDK可以在第三方上下文中保留访客ID，以便能够在各个网站中使用相同的访客ID。 如果您有多个网站或者希望与合作伙伴共享数据，请使用此选项；但是，出于隐私原因，有时并不需要此选项。
