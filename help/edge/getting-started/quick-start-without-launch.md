---
title: 使用纯javascript快速开始
seo-title: 'Adobe Experience Platform Web SDK快速开始 '
description: 使用Experience Platform Web SDK收集数据的快速开始指南
seo-description: 使用Experience Platform Web SDK收集数据的快速开始指南
translation-type: tm+mt
source-git-commit: 7c5d4306f9964553cf48a208166fce265dcdd94d
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 3%

---


# 欢迎

本指南引导您通过不同方式设置Adobe Experience Platform Web SDK。 要能够使用此功能，您需要将其列入白名单。 如果您想继续等待列表，请联系您的客户经理。

- 启用 [第一方域(CNAME)](https://docs.adobe.com/content/help/zh-Hans/core-services/interface/ec-cookies/cookies-first-party.html) 。 如果您已经拥有Analytics的CNAME，则应使用该CNAME。 在开发中测试无需CNAME即可正常工作，但在开始生产之前您需要CNAME
- 有权使用Adobe Experience Platform Data Platform。  如果您尚未购买Platform，我们将为您提供Experience Platform Data Services Foundation，以便在SDK中以有限方式使用，不收取任何额外费用。
- 正在使用最新版的访客ID服务

## 创建配置ID

您可以使用Adobe Launch中的 [边缘配置工具](../fundamentals/edge-configuration.md) ，创建配置ID，即使您没有使用标签管理功能。 这样，边缘网络就可以将数据发送到各种解决方案。 有关如何查找每个选项的详细信息，请参阅 [边缘配置工具](../fundamentals/edge-configuration.md) 页。

>[!NOTE]
>
>您的组织必须列入此功能的白名单。 请联系您的CSM，让列表参与最终的白名单。

## 准备模式

Experience Platform Edge Network将数据作为XDM。 XDM是一种数据格式，允许您定义模式。 模式定义边缘网络希望数据的格式。 要发送数据，您需要定义模式。

- [创建模式](../../xdm/tutorials/create-schema-ui.md)
- 将Adobe Experience Platform Web SDK混合添加到您创建的模式

## 安装SDK

要安装SDK，请在HTML的标记中尽可能高地复制并粘贴以 `<head>` 下“基本代码”:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

有关执行此操作的不同选项的更多详细信息，请 [参阅安装SDK](../fundamentals/installing-the-sdk.md)。

## 配置SDK

接下来，向SDK提供您的配置。 使用命令完 `configure` 成。 这应该是每个页面上调用的第一个命令。

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93:dev",
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

- [构建模式](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- [了解调试](../fundamentals/debugging.md)
- 了解如何 [个性化体验](../fundamentals/rendering-personalization-content.md)
- 了解如何将数据发送到多个解决方案
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
