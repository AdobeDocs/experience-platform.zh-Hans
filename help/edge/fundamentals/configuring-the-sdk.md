---
title: 配置Adobe Experience Platform Web SDK
description: 了解如何配置Adobe Experience Platform Web SDK。
seo-description: 了解如何配置Experience Platform Web SDK
keywords: configure;configuration;SDK;edge;Web SDK;configure;edgeConfigId;context;web;device;环境;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConnence;web sdk设置；prehidingStyle；不透明度；cookieDUrlDDestinationsEnabled;idMigrationEnabled;thirdPartyCookiesEnabled;
translation-type: tm+mt
source-git-commit: f78da58ba7a593d9c161030833d9b69e2ba57c9a
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 10%

---


# 配置平台Web SDK

SDK的配置是使用`configure`命令完成的。

>[!IMPORTANT]
>
>`configure` 应 ** 该始终是第一个命令

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
| 字符串 | 是 | 无 |

您分配的配置ID，它将SDK链接到相应的帐户和配置。  在单个页面中配置多个实例时，必须为每个实例配置不同的`edgeConfigId`。

### `context`

| **类型** | **必需** | **默认值** |
| ---------------- | ------------ | -------------------------------------------------- |
| 字符串数组 | 否 | `["web", "device", "environment", "placeContext"]` |

指示要自动收集的上下文类别，如[自动信息](../data-collection/automatic-information.md)中所述。  如果未指定此配置，则默认情况下使用所有类别。

### `debugEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `false` |

指示是否应启用调试。 将此配置设置为`true`可启用以下功能：

| **功能** | **函数** |
| ---------------------- | ------------------ |
| 同步验证 | 验证正在根据模式收集的数据，并在以下标签下的响应中返回错误：`collect:error OR success` |
| 控制台日志记录 | 允许调试消息显示在浏览器的JavaScript控制台中 |

### `edgeDomain` {#edge-domain}

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ------------------ |
| 字符串 | 否 | `beta.adobedc.net` |
| 字符串 | 否 | `omtrdc.net` |

用于与Adobe服务交互的域。 仅当您有第一方域(CNAME)，用于代理对Adobe边缘基础结构的请求时，才使用。

### `orgId`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 字符串 | 是 | 无 |

您分配的[!DNL Experience Cloud]组织ID。  在页面内配置多个实例时，必须为每个实例配置不同的`orgId`。

## 数据收集

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

指示是否应自动收集与链接点击关联的数据。 有关详细信息，请参阅[自动链接跟踪](../data-collection/track-links.md#automaticLinkTracking)。

### `onBeforeEventSend`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 函数 | 否 | ()=>未定义 |

设置此项可配置在发送每个事件之前调用的回调。  字段为`xdm`的对象将发送到回调。  修改`xdm`对象以更改发送的内容。  在回调中，`xdm`对象已在事件命令中传递了数据，并自动收集了信息。 有关此回调的时间和示例的详细信息，请参阅[全局修改事件](tracking-events.md#modifying-events-globally)。

## 隐私选项

### `defaultConsent` {#default-consent}

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 对象 | 否 | `"in"` |

设置用户的默认同意。 当尚未为用户保存同意首选项时，会使用此选项。 其他有效值为`"pending"`和`"out"`。 此默认值不会保留到用户的用户档案。 仅当调用setConnence时，用户的用户档案才会更新。
* `"in"`:如果设置了此设置或未提供任何值，则工作将在没有用户同意首选项的情况下继续进行。
* `"pending"`:设置此项后，工作将排队，直到用户提供同意首选项。
* `"out"`:设置此项后，工作将被丢弃，直到用户提供同意首选项。在提供用户的首选项后，工作会根据用户的首选项继续或中止。 有关详细信息，请参阅[支持同意](../consent/supporting-consent.md)。

## 个性化选项

### `prehidingStyle`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 字符串 | 否 | 无 |

用于创建CSS样式定义，当从服务器加载个性化内容时隐藏网页的内容区域。 如果未提供此选项，则在加载个性化内容时，SDK不会尝试隐藏任何内容区域，这可能会导致“闪烁”。

例如，如果您的网页上有一个ID为`container`的元素，在从服务器加载个性化内容时，您希望隐藏其默认内容，则预隐藏样式的示例如下：

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## 受众选项

### `cookieDestinationsEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

启用[!DNL Audience Manager] Cookie目标，允许根据区段资格设置Cookie。

### `urlDestinationsEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

启用[!DNL Audience Manager] URL目标，允许基于区段资格触发URL。

## 标识选项

### `idMigrationEnabled` {#id-migration-enabled}

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | true |

如果为true，则SDK将读取并设置旧的AMCV Cookie。 这有助于过渡到使用Adobe Experience Platform Web SDK，而站点的某些部分可能仍在使用访客.js。 此外，如果页面上定义了访客 API，则SDK将为ECID查询访客 API。 这使您能够使用Adobe Experience Platform Web SDK将两个标签页放在一起，并且仍具有相同的ECID。

### `thirdPartyCookiesEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | true |

启用Adobe第三方Cookie的设置。 SDK能够将访客ID保留在第三方上下文中，以允许在多个站点中使用相同的访客ID。 如果您有多个站点或希望与合作伙伴共享数据，则此功能非常有用；但是，有时出于隐私考虑，这是不必要的。
