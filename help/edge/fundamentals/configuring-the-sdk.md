---
title: 配置SDK
seo-title: 配置Adobe Experience PlatformWeb SDK
description: 了解如何配置Experience PlatformWeb SDK
seo-description: 了解如何配置Experience PlatformWeb SDK
keywords: 配置；配置；SDK;edge;Web SDK；配置；edgeConfigId;context;web;device;环境;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConnence;web sdk设置；prehidingStyle;opaty;cookieDDUrlDeDeDesDesDEntEnageEnEnEnabled;DestinationsEnabled;idMigrationEnabled;thirdPartyCookiesEnabled;
translation-type: tm+mt
source-git-commit: 3ac00fda2c0a43437fb212dcba7e98c63503b9c4
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 11%

---


# 配置SDK

SDK的配置是使用`configure`命令完成的。

>[!IMPORTANT]
>
>`configure` 应 ** 该永远是第一个命令。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

在配置过程中可以设置许多选项。 所有选项均可在下面找到，按类别分组。

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

指示要自动收集的上下文类别，如[自动信息](../data-collection/automatic-information.md)中所述。  如果未指定此配置，则默认情况下将使用所有类别。

### `debugEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `false` |

指示是否应启用调试。 将此配置设置为`true`将启用以下功能：

| **功能** | **函数** |
| ---------------------- | ------------------ |
| 同步验证 | 验证根据模式收集的数据，并在以下标签下的响应中返回错误：`collect:error OR success` |
| 控制台日志记录 | 允许调试消息显示在浏览器的JavaScript控制台中 |

### `edgeDomain`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ------------------ |
| 字符串 | 否 | `beta.adobedc.net` |
| 字符串 | 否 | `omtrdc.net` |

用于与Adobe服务交互的域。 仅当您有第一方域(CNAME)来代理对Adobe边缘基础结构的请求时，才使用此方法。

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

指示是否应自动收集与链接单击关联的数据。 有关详细信息，请参阅[自动链接跟踪](../data-collection/track-links.md#automaticLinkTracking)。

### `onBeforeEventSend`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 函数 | 否 | ()=>未定义 |

设置此设置可配置在发送每个事件之前调用的回调。  字段为`xdm`的对象将发送到回调。  修改`xdm`对象以更改发送内容。  在回调中，`xdm`对象已在事件命令中传递数据，并自动收集信息。 有关此回调的时间和示例的详细信息，请参阅[全局修改事件](tracking-events.md#modifying-events-globally)。

## 隐私选项

### `defaultConsent` {#default-consent}

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 对象 | 否 | `"in"` |

设置用户的默认同意。 当尚未为用户保存同意首选项时，将使用此选项。 另一个有效值为`"pending"`。 设置此项后，工作将排队，直到用户提供同意首选项。 提供用户首选项后，工作将根据用户的首选项继续或中止。 有关详细信息，请参阅[支持同意](../consent/supporting-consent.md)。

## 个性化选项

### `prehidingStyle`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 字符串 | 否 | 无 |

用于创建CSS样式定义，该定义在从服务器加载个性化内容时隐藏网页的内容区域。 如果未提供此选项，则加载个性化内容时SDK不会尝试隐藏任何内容区域，这可能导致“闪烁”。

例如，如果网页上的元素ID为`container`，在从服务器加载个性化内容时，您希望隐藏其默认内容，则预隐藏样式的示例如下：

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## 受众选项

### `cookieDestinationsEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

启用[!DNL Audience Manager] cookie目标，允许根据区段资格设置cookie。

### `urlDestinationsEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

启用[!DNL Audience Manager] URL目标，它允许基于段资格触发URL。

## 标识选项

### `idMigrationEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | true |

如果为真，则SDK将阅读并设置旧版AMCV cookie。 这有助于过渡到使用Adobe Experience PlatformWeb SDK，而站点的某些部分可能仍在使用访客.js。 此外，如果页面上定义了访客API，则SDK将查询ECID的访客API。 这使您能够使用AEP Web SDK对两个标签页添加标签，同时仍具有相同的ECID。

### `thirdPartyCookiesEnabled`

| **类型** | **必需** | **默认值** |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | 真 |

启用Adobe第三方Cookie的设置。 SDK能够将访客ID保留在第三方上下文中，从而允许在多个站点上使用相同的访客ID。 如果您有多个站点或希望与合作伙伴共享数据，则此功能非常有用；但是，有时出于隐私原因而不需要这样做。
