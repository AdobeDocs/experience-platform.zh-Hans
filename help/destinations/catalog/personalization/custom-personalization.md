---
keywords: 自定义个性化；目的地；experience platform自定义目标；
title: 自定义个性化连接（测试版）
description: 此目标可提供外部个性化、内容管理系统、广告服务器以及网站上运行的其他应用程序，以便从Adobe Experience Platform中检索区段信息。 此目标根据用户配置文件的区段成员资格提供实时1:1和个性化。
source-git-commit: 0635828cf3f637e67d2cabda860ca452e61892d4
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 自定义个性化连接（测试版） {#custom-personalization-connection}

## 概述 {#overview}

>[!IMPORTANT]
>
>Adobe Experience Platform中的自定义个性化连接当前处于测试阶段。 文档和功能可能会发生更改。

此目标提供了一种方法，可将区段信息从Adobe Experience Platform检索到外部个性化平台、内容管理系统、广告服务器以及在客户网站上运行的其他应用程序。

## 先决条件 {#prerequisites}

此集成由[Adobe Experience Platform Web SDK](../../../edge/home.md)提供支持。 您必须使用此SDK才能使用此目标。

## 导出类型 {#export-type}

**配置文件请求**  — 您正在为单个配置文件请求在自定义个性化目标中映射的所有区段。可以为不同的[Adobe数据收集数据流](../../../edge/fundamentals/datastreams.md)设置不同的自定义个性化目标。

## 用例 {#use-cases}

此目标与广告服务器和非Adobe个性化应用程序共享受众，以便实时确定用户应在网站上看到的广告。

### 用例#1

**个性化主页**

一个房屋租赁和销售网站希望根据Adobe Experience Platform的区段资格对其主页进行个性化。 公司可以选择哪些受众应获得个性化体验，并将这些体验映射到为其非Adobe个性化应用程序设置的自定义个性化目标，以将其作为定位标准。

**有针对性的网站广告**

为其广告服务器使用单独的自定义个性化目标，同一网站可以使用Adobe Experience Platform中的不同区段集作为定位标准来定位网站广告。

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:输入目标的描述。例如，您可以提及您使用此目标的促销活动。 此字段为可选字段。
* **[!UICONTROL 集成别名]**:此值将作为JSON对象名称发送到Experience PlatformWeb SDK。
* **[!UICONTROL 数据流ID]**:这可确定区段将包含在页面响应中的数据收集数据流。下拉菜单仅显示已启用目标配置的数据流。 有关更多详细信息，请参阅[配置数据流](../../../edge/fundamentals/datastreams.md)。

## 将区段激活到此目标 {#activate}

有关将受众区段激活到此目标的说明，请阅读[将配置文件和区段激活到配置文件请求目标](../../ui/activate-profile-request-destinations.md)。

## 导出的数据 {#exported-data}

如果您使用[Adobe标记](../../../tags/home.md)来部署Experience PlatformWeb SDK，请使用[发送事件结束](../../../edge/extension/event-types.md)功能，并且您的自定义代码操作将具有一个`event.destinations`变量，您可以使用该变量查看导出的数据。

如果您没有使用[Adobe标记](../../../tags/home.md)来部署Experience PlatformWeb SDK，请使用[处理事件](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events)响应功能来查看导出的数据。

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
}).then(function(results) {
    if(results.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = results.destinations.filter(x => x.alias == “personalizationAlias”)
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = results.destinations.filter(x => x.alias == “adServerAlias”)
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

处理数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据管理的详细信息，请阅读[数据管理概述](../../../data-governance/home.md)。
