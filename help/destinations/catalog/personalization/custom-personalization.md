---
keywords: 自定义个性化；目的地；experience platform自定义目标；
title: 自定义个性化连接
description: 此目标可提供外部个性化、内容管理系统、广告服务器以及网站上运行的其他应用程序，以便从Adobe Experience Platform中检索区段信息。 此目标基于用户配置文件区段成员资格提供实时个性化。
hide: true
hidefromtoc: true
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 7ac7f533bb8547865b53892d371059aa60d2232e
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---

# 自定义个性化连接 {#custom-personalization-connection}

## 概述 {#overview}

此目标提供了一种方法，可将区段信息从Adobe Experience Platform检索到外部个性化平台、内容管理系统、广告服务器以及在客户网站上运行的其他应用程序。

## 先决条件 {#prerequisites}

此集成由 [Adobe Experience Platform Web SDK](../../../edge/home.md) 或 [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). 您必须使用其中一个SDK才能使用此目标。

>[!IMPORTANT]
>
>在创建自定义个性化连接之前，请阅读有关如何 [为同一页面和下一页面个性化配置个性化目标](../../ui/configure-personalization-destinations.md). 本指南将引导您跨多个Experience Platform组件完成同页和下一页个性化用例所需的配置步骤。

## 导出类型和频度 {#export-type-frequency}

**用户档案请求**  — 您正在为单个用户档案请求在自定义个性化目标中映射的所有区段。 可以为不同的自定义个性化目标设置不同的自定义个性化目标 [Adobe数据收集数据流](../../../edge/datastreams/overview.md).

## 用例 {#use-cases}

的 [!DNL Custom personalization connection] 允许您使用自己的个性化合作伙伴平台(例如， [!DNL Optimizely], [!DNL Pega])，同时还利用Experience Platform边缘网络数据收集和分段功能，提供更深入的客户个性化体验。

下面介绍的用例包括网站个性化和目标网站广告。

要启用这些用例，客户需要一种快速、简化的方式，从Experience Platform中检索区段信息，并将此信息发送到他们在Experience PlatformUI中配置为自定义个性化连接的指定系统。

这些系统可以是跨客户Web和移动资产运行的外部个性化平台、内容管理系统、广告服务器以及其他应用程序。

### 同页个性化 {#same-page}

用户访问您网站的某个页面。 客户可以使用当前页面访问信息（例如，引荐URL、浏览器语言、嵌入式产品信息），通过非Adobe平台的自定义个性化连接(例如， [!DNL Pega], [!DNL Optimizely]等)。

### 下一页个性化 {#next-page}

用户访问您网站上的页面A。 根据此交互，用户已符合一组区段的资格条件。 然后，用户单击将页面A转到页面B的链接。用户在页面A的上一次交互期间有资格访问的区段，以及由当前网站访问确定的用户档案更新，将用于支持下一项操作/决策（例如，要向访客显示哪个广告横幅，或者，如果是A/B测试，则显示哪个页面版本）。

### 下一会话个性化 {#next-session}

用户访问您网站上的多个页面。 根据这些交互，用户已符合一组区段的条件。 然后，用户终止当前浏览会话。

次日，用户返回同一客户网站。 在与所有已访问网站页面的上一次交互期间，他们符合条件的区段，以及由当前网站访问确定的配置文件更新，将用于选择下一个操作/决策（例如，要向访客显示哪个广告横幅，或者，如果是A/B测试，则显示哪个页面版本）。

## 连接到目标 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="关于数据流ID"
>abstract="此选项确定区段在响应页面时将包含在哪些数据收集数据流中。 下拉菜单仅显示已启用目标配置的数据流。 必须先配置数据流，然后才能配置目标。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="了解如何配置数据流"

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:输入目标的描述。 例如，您可以提及您使用此目标的促销活动。 此字段为可选字段。
* **[!UICONTROL 集成别名]**:此值将作为JSON对象名称发送到Experience PlatformWeb SDK。
* **[!UICONTROL 数据流ID]**:这可确定区段将包含在页面响应中的数据收集数据流。 下拉菜单仅显示已启用目标配置的数据流。 请参阅 [配置数据流](../../../edge/datastreams/overview.md) 以了解更多详细信息。

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [将用户档案和区段激活到用户档案请求目标](../../ui/activate-profile-request-destinations.md) 有关将受众区段激活到此目标的说明。

## 导出的数据 {#exported-data}

如果您使用 [Adobe Experience Platform中的标记](../../../tags/home.md) 要部署Experience PlatformWeb SDK，请使用 [发送事件结束](../../../edge/extension/event-types.md) 功能和您的自定义代码操作将具有 `event.destinations` 变量，以便您查看导出的数据。

以下是 `event.destinations` 变量：

```
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         }
      ]
   }
]
```

如果您没有使用 [标记](../../../tags/home.md) 要部署Experience PlatformWeb SDK，请使用 [处理事件响应](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) 功能查看导出的数据。

可以解析来自Adobe Experience Platform的JSON响应，以查找您与Adobe Experience Platform集成的应用程序的相应集成别名。 区段ID可以作为定位参数传递到应用程序的代码中。 下面是一个特定于目标响应的示例。

```
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    if(result.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = result.destinations.filter(x => x.alias == “personalizationAlias”)
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == “adServerAlias”)
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，读取 [数据管理概述](../../../data-governance/home.md).
