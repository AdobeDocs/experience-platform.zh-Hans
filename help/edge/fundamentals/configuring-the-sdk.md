---
title: 配置Adobe Experience Platform Web SDK
description: 了解如何配置Adobe Experience Platform Web SDK。
seo-description: 了解如何配置Experience Platform Web SDK
keywords: configure;configuration;SDK;edge;Web SDK;configure;edgeConfigId;context;web;device;环境;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConnence;web sdk设置；prehidingStyle；不透明度；cookieDUrlDDestinationsEnabled;idMigrationEnabled;thirdPartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
translation-type: tm+mt
source-git-commit: 2895975b9c103e6afba7db221223b4ef2116caf3
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 8%

---

# 配置平台Web SDK

SDK的配置是使用`configure`命令完成的。

>[!IMPORTANT]
>
>`configure` 始终 ** 是第一个命令。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

在配置过程中可以设置许多选项。 所有选项均可在下面找到，并按类别分组。

## 常规选项

### `edgeConfigId`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 字符串 | 是 | None |

{style=&quot;table-layout:auto&quot;}

您分配的配置ID，它将SDK链接到相应的帐户和配置。 在单个页面中配置多个实例时，必须为每个实例配置不同的`edgeConfigId`。

### `context`

| **类型** | **必需** | **默认值** |
| ---------------- | ------------ | -------------------------------------------------- |
| 字符串数组 | 否 | `["web", "device", "environment", "placeContext"]` |

{style=&quot;table-layout:auto&quot;}

指示要自动收集的上下文类别，如[自动信息](../data-collection/automatic-information.md)中所述。 如果未指定此配置，则默认情况下使用所有类别。

### `debugEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `false` |

{style=&quot;table-layout:auto&quot;}

指示是否启用调试。 将此配置设置为`true`可启用以下功能：

| **功能** | **函数** |
| ---------------------- | ------------------ |
| 同步验证 | 验证正在根据模式收集的数据，并在以下标签下的响应中返回错误：`collect:error OR success` |
| 控制台日志记录 | 允许调试消息显示在浏览器的JavaScript控制台中 |

{style=&quot;table-layout:auto&quot;}

### `edgeDomain` {#edge-domain}

用您的第一方域填充此字段。 有关详细信息，请参阅[文档](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html)。

该域与位于www.`data.{customerdomain.com}`{customerdomain.com}。

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
| 布尔值 | 否 | `true` |

{style=&quot;table-layout:auto&quot;}

指示是否自动收集与链接单击关联的数据。 有关详细信息，请参阅[自动链接跟踪](../data-collection/track-links.md#automaticLinkTracking)。

### `onBeforeEventSend`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 函数 | 否 | ()=>未定义 |

{style=&quot;table-layout:auto&quot;}

在发送每个事件之前，配置调用的回调。 字段为`xdm`的对象将发送到回调。 要更改发送内容，请修改`xdm`对象。 在回调中，`xdm`对象已包含在事件命令中传递的数据以及自动收集的信息。 有关此回调的时间和示例的详细信息，请参阅[全局修改事件](tracking-events.md#modifying-events-globally)。

## 隐私选项

### `defaultConsent` {#default-consent}

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 对象 | 否 | `"in"` |

{style=&quot;table-layout:auto&quot;}

设置用户的默认同意。 如果尚未为用户保存同意首选项，请使用此设置。 其他有效值为`"pending"`和`"out"`。 此默认值不会保留到用户的用户档案。 仅当调用`setConsent`时，才更新用户的用户档案。
* `"in"`:设置此设置或未提供任何值时，工作将在未征得用户同意首选项的情况下继续进行。
* `"pending"`:设置此设置后，工作将排队，直到用户提供同意首选项。
* `"out"`:设置此设置后，将放弃工作，直到用户提供同意首选项。在提供用户的首选项后，工作会根据用户的首选项继续或中止。 有关详细信息，请参阅[支持同意](../consent/supporting-consent.md)。

## 个性化选项

### `prehidingStyle`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 字符串 | 否 | 无 |

{style=&quot;table-layout:auto&quot;}

用于创建CSS样式定义，当从服务器加载个性化内容时隐藏网页的内容区域。 如果未提供此选项，则在加载个性化内容时，SDK不会尝试隐藏任何内容区域，这可能会导致“闪烁”。

例如，如果网页上的某个元素的ID为`container`，在从服务器加载个性化内容时要隐藏其默认内容，请使用以下预隐藏样式：

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## 受众选项

### `cookieDestinationsEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style=&quot;table-layout:auto&quot;}

启用[!DNL Audience Manager] Cookie目标，允许根据区段资格设置Cookie。

### `urlDestinationsEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style=&quot;table-layout:auto&quot;}

启用[!DNL Audience Manager] URL目标，允许基于区段资格触发URL。

## 标识选项

### `idMigrationEnabled` {#id-migration-enabled}

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style=&quot;table-layout:auto&quot;}

如果为true，则SDK会读取并设置旧的AMCV Cookie。 此选项有助于过渡到使用Adobe Experience Platform Web SDK，而站点的某些部分可能仍使用访客.js。 如果页面上定义了访客 API，则SDK查询访客API用于ECID。 此选项允许您使用Adobe Experience Platform Web SDK创建双标签页面，但仍具有相同的ECID。

### `thirdPartyCookiesEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style=&quot;table-layout:auto&quot;}

启用Adobe第三方Cookie的设置。 SDK可以将访客ID保留在第三方上下文中，以允许在多个站点中使用相同的访客ID。 如果您有多个站点或希望与合作伙伴共享数据，请使用此选项；但是，有时出于隐私原因不需要此选项。
