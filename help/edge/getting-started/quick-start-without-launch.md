---
title: 使用纯javascript快速开始
seo-title: 'Adobe Experience PlatformWeb SDK快速开始 '
description: 使用开始Web SDK收集数据的快速Experience Platform指南
seo-description: 使用开始Web SDK收集数据的快速Experience Platform指南
keywords: 1st-party domain;CNAME;schema;create schema;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;install sdk;install web sdk;configure;configure web sdk;
translation-type: tm+mt
source-git-commit: f178da80d0902f76868986426600f3da426cf24d
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 5%

---


# Adobe Experience PlatformWeb SDK JavaScript快速开始指南

本指南引导您了解设置Adobe Experience PlatformWeb SDK的不同方法。 要使用此功能，您需要处于允许列表状态。 如果您希望进入等待列表，请联系您的认证软件经理(CSM)。

- 启用 [第一方域(CNAME)](https://docs.adobe.com/content/help/zh-Hans/core-services/interface/ec-cookies/cookies-first-party.html) 。 如果您已经拥有Analytics的CNAME，则应使用该CNAME。 在开发中测试无需CNAME即可正常工作，但在开始生产之前，您需要CNAME。
- 有权获得Adobe Experience Platform。  如果您尚未购买平台，Adobe将为您提供Experience Platform数据服务基础，以便在SDK中以有限方式使用，并且不收取额外费用。
- 使用最新版的访客ID服务。

## 准备模式

将 [!DNL Experience Platform Edge Network] 数据视为XDM。 XDM是一种数据格式，允许您定义模式。 模式定义 [!DNL Edge Network] 数据的格式。 要发送数据，您需要定义模式。

- [创建模式](../../xdm/tutorials/create-schema-ui.md)
- 将Adobe Experience Platform混 [!DNL Web SDK] 音添加到您创建的模式

以下视频旨在支持您为模式创建数据集、数据集和流源连接器。 [!DNL Web SDK]

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

## 创建配置ID

您可以在Adobe启动中使用 [边缘配置工具](../fundamentals/edge-configuration.md) ，创建配置ID，即使您没有使用标签管理功能。 这样，您便能够将数 [!DNL Edge Network] 据发送到各种解决方案。 有关如何查找每个选项的详细信息，请参阅 [边缘配置工具](../fundamentals/edge-configuration.md) 页。

>[!NOTE]
>
>您的组织必须具有此功能的允许列表。 请联系您的CSM以接受允许列表。

## 安装SDK

要安装SDK，请在HTML的标记中尽可能高地复制并粘贴以 `<head>` 下“基本代码”:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.1.0/alloy.min.js" async></script>
```

有关执行此操作的不同选项的更多详细信息，请 [参阅安装SDK](../fundamentals/installing-the-sdk.md)。

## 配置SDK

接下来，向SDK提供您的配置。 使用命令完 `configure` 成。 这应该是每个页面上调用的第一个命令。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93:dev",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

在此，您提供您在上面创建的配置ID以及您的组织ID。 这是唯二的必填字段。 但是，还有许多其 [他配置选项](../fundamentals/configuring-the-sdk.md)。

## 发送事件

调用configure命令后，您可以自由开始跟踪事件。

```javascript
alloy("sendEvent", {});
```

通常，您会向事件发送一些数据。 您可以这样发送XDM数据。 您发送的模式必须位于您在XDM中创建的数据中。

```javascript
alloy("sendEvent", {
  "xdm": {
    "web":{
      "webPageDetails":{
        "name":"Home Page"
      }
    }
  }
});
```

有关如何跟踪事件的更多详细信息，请参阅 [跟踪事件](../fundamentals/tracking-events.md)。

## 后续步骤

在数据流动后，您可以执行以下操作：

- [构建模式](https://docs.adobe.com/content/help/zh-Hans/experience-platform/xdm/schema/composition.html)
- [了解调试](../fundamentals/debugging.md)
- 了解如何 [个性化体验](../fundamentals/rendering-personalization-content.md)
- 了解如何将数据发送到多个解决方案
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
