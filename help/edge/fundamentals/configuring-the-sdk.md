---
title: 配置Adobe Experience Platform Web SDK
description: 了解如何配置Adobe Experience Platform Web SDK。
seo-description: 了解如何配置Experience PlatformWeb SDK
keywords: 配置；配置；SDK;Edge;Web SDK；配置；edgeConfigId；上下文；Web；设备；placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;Web SDK设置；prehidingStyle;ocookieDestinationsEnable;urlDestinationsEnabled;idMigCookiesEnabled；第三方Cookies
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: 549203c8ddc94e00cf4e4ba432f367ddc371cb27
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 14%

---

# 配置平台Web SDK

使用`configure`命令完成了SDK的配置。

>[!IMPORTANT]
>
>`configure` 始终 ** 是第一个调用的命令。

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
>**边缘配置已重新命名为数据流。数据流ID与配置ID相同。**

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 字符串 | 是 | None |

{style=&quot;table-layout:auto&quot;}

您分配的配置ID，用于将SDK关联到相应的帐户和配置。 在单个页面中配置多个实例时，必须为每个实例配置不同的`edgeConfigId`。

### `context`

| **类型** | **必需** | **默认值** |
| ---------------- | ------------ | -------------------------------------------------- |
| 字符串数组 | 否 | `["web", "device", "environment", "placeContext"]` |

{style=&quot;table-layout:auto&quot;}

指示要自动收集的上下文类别，如[自动信息](../data-collection/automatic-information.md)中所述。 如果未指定此配置，则默认使用所有类别。

### `debugEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔型 | 否 | `false` |

{style=&quot;table-layout:auto&quot;}

指示是否启用调试。 将此配置设置为`true`可启用以下功能：

| **功能** | **函数** |
| ---------------------- | ------------------ |
| 同步验证 | 验证根据架构收集的数据，并在响应中通过以下标签返回错误：`collect:error OR success` |
| 控制台日志记录 | 允许在浏览器的JavaScript控制台中显示调试消息 |

{style=&quot;table-layout:auto&quot;}

### `edgeDomain` {#edge-domain}

使用第一方域填充此字段。 有关更多详细信息，请参阅[文档](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=zh-Hans)。

该域与位于www的网站的`data.{customerdomain.com}`类似。{customerdomain.com}。

### `orgId`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 字符串 | 是 | 无 |

{style=&quot;table-layout:auto&quot;}

您分配的[!DNL Experience Cloud]组织ID。 在页面内配置多个实例时，必须为每个实例配置不同的`orgId`。

## 数据收集

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔型 | 否 | `true` |

{style=&quot;table-layout:auto&quot;}

指示是否自动收集与链接点击量关联的数据。 有关更多信息，请参阅[自动链接跟踪](../data-collection/track-links.md#automaticLinkTracking)。 如果链接包含下载属性或链接以文件扩展名结尾，则也会将其标记为下载链接。 下载链接限定符可以配置正则表达式。 默认值为 `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 函数 | 否 | ()=>未定义 |

{style=&quot;table-layout:auto&quot;}

在发送每个事件之前，配置为其调用的回调。 字段为`xdm`的对象将发送到回调中。 要更改所发送的内容，请修改`xdm`对象。 在回调中，`xdm`对象已经具有在event命令中传递的数据以及自动收集的信息。 有关此回调的时间和示例的更多信息，请参阅[全局修改事件](tracking-events.md#modifying-events-globally)。

## 隐私选项

### `defaultConsent` {#default-consent}

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 对象 | 否 | `"in"` |

{style=&quot;table-layout:auto&quot;}

设置用户的默认同意。 如果尚未为用户保存同意首选项，则使用此设置。 其他有效值为`"pending"`和`"out"`。 此默认值不会持久保留在用户的配置文件中。 仅当调用`setConsent`时，才会更新用户的配置文件。
* `"in"`:如果设置此设置或未提供任何值，则在未使用用户同意首选项的情况下继续工作。
* `"pending"`:设置此设置后，工作将排入队列，直到用户提供同意首选项为止。
* `"out"`:设置此设置后，将丢弃工作，直到用户提供同意首选项为止。在提供用户的首选项后，根据用户的首选项继续或中止工作。 有关更多信息，请参阅[支持同意](../consent/supporting-consent.md)。

## 个性化选项

### `prehidingStyle`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 字符串 | 否 | 无 |

{style=&quot;table-layout:auto&quot;}

用于创建CSS样式定义，当从服务器加载个性化内容时，该定义会隐藏网页的内容区域。 如果未提供此选项，则SDK在加载个性化内容时不会尝试隐藏任何内容区域，这可能会导致“闪烁”。

例如，如果网页上的某个元素的ID为`container`（您希望在从服务器加载个性化内容时隐藏其默认内容），请使用以下预隐藏样式：

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## 受众选项

### `cookieDestinationsEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔型 | 否 | `true` |

{style=&quot;table-layout:auto&quot;}

启用[!DNL Audience Manager] Cookie目标，以便根据区段鉴别来设置Cookie。

### `urlDestinationsEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔型 | 否 | `true` |

{style=&quot;table-layout:auto&quot;}

启用[!DNL Audience Manager] URL目标，以便根据区段鉴别触发URL。

## 身份选项

### `idMigrationEnabled` {#id-migration-enabled}

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔型 | 否 | `true` |

{style=&quot;table-layout:auto&quot;}

如果为true，则SDK会读取并设置旧的AMCV Cookie。 此选项有助于过渡到使用Adobe Experience Platform Web SDK，而网站的某些部分可能仍使用Visitor.js。 如果页面上定义了访客API，SDK将查询访客API以获取ECID。 此选项允许您使用Adobe Experience Platform Web SDK创建双标记页面，但仍然具有相同的ECID。

### `thirdPartyCookiesEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔型 | 否 | `true` |

{style=&quot;table-layout:auto&quot;}

启用Adobe第三方Cookie的设置。 SDK可以在第三方上下文中保留访客ID，以便允许在网站之间使用相同的访客ID。 如果您有多个网站，或者希望与合作伙伴共享数据，请使用此选项；但是，有时出于隐私原因不需要此选项。
