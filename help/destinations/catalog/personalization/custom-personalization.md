---
keywords: 自定义个性化；目标；experience platform自定义目标；
title: 自定义个性化连接
description: 此目标提供外部个性化、内容管理系统、广告服务器以及在您的网站上运行的其他应用程序，以便从Adobe Experience Platform检索受众信息。 此目标根据用户个人资料受众成员资格提供实时个性化。
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 10%

---


# 自定义个性化连接 {#custom-personalization-connection}

## 目标更改日志 {#changelog}

| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2023 年 5 月 | 功能和文档更新 | 截至2023年5月， **[!UICONTROL 自定义个性化]** 连接支持 [基于属性的个性化](../../ui/activate-edge-personalization-destinations.md#map-attributes) 面向所有客户。 |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>配置文件属性可能包含敏感数据。 为了保护此数据， **[!UICONTROL 自定义个性化]** 目标要求您使用 [边缘网络服务器API](/help/server-api/overview.md) 在为基于属性的个性化配置目标时。 所有服务器API调用必须在 [已验证的上下文](../../../server-api/authentication.md).
>
><br>如果您已在使用Web SDK或Mobile SDK进行集成，则可以通过添加服务器端集成来通过服务器API检索属性。
>
><br>如果不遵循上述要求，则将仅基于受众会员资格进行个性化。

## 概述 {#overview}

此目标提供了一种方法，可将受众信息从Adobe Experience Platform检索到外部个性化平台、内容管理系统、广告服务器以及在客户网站上运行的其他应用程序。

## 先决条件 {#prerequisites}

此集成由 [Adobe Experience Platform Web SDK](../../../edge/home.md) 或 [Adobe Experience Platform移动SDK](https://developer.adobe.com/client-sdks/documentation/). 您必须使用这些SDK之一才能使用此目标。

>[!IMPORTANT]
>
>在创建自定义个性化连接之前，请阅读有关如何执行操作的指南 [将受众数据激活到边缘个性化目标](../../ui/activate-edge-personalization-destinations.md). 本指南将指导您跨多个Experience Platform组件完成同页和下一页个性化用例所需的配置步骤。

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 受支持 | 描述 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!DNL Profile request]** | 您正在请求在单个配置文件的自定义个性化目标中映射的所有受众。 可以为不同的设置不同的自定义个性化目标 [Adobe数据收集数据流](../../../datastreams/overview.md). |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

## 连接到目标 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="关于数据流 ID"
>abstract="此选项确定受众将包含在哪个数据收集数据流中以响应页面。下拉菜单仅显示已启用目标配置的数据流。您必须先配置数据流，然后才能配置目标。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=zh-Hans" text="了解如何配置数据流"

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

同时 [设置](../../ui/connect-destination.md) 此目标必须提供以下信息：

* **[!UICONTROL 名称]**：填写此目标的首选名称。
* **[!UICONTROL 描述]**：输入目标的描述。 例如，您可以提及要将此目标用于哪个营销活动。 此字段为可选字段。
* **[!UICONTROL 集成别名]**：此值作为JSON对象名称发送到Experience PlatformWeb SDK。
* **[!UICONTROL 数据流ID]**：此值确定在对页面的响应中将包含受众的数据收集数据流。 下拉菜单仅显示已启用目标配置的数据流。请参阅 [配置数据流](../../../datastreams/overview.md) 以了解更多详细信息。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [激活用户档案和受众边缘个性化目标](../../ui/activate-edge-personalization-destinations.md) 有关将受众激活到此目标的说明。

## 导出的数据 {#exported-data}

如果您使用 [Adobe Experience Platform中的标记](../../../tags/home.md) 要部署Experience PlatformWeb SDK，请使用 [发送事件完成](../../../tags/extensions/client/web-sdk/event-types.md) 功能和自定义代码操作将具有 `event.destinations` 变量中，可用于查看导出的数据。

以下是的示例值 `event.destinations` 变量：

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

如果您没有使用 [标记](../../../tags/home.md) 要部署Experience PlatformWeb SDK，请使用 [处理来自事件的响应](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) 功能以查看导出的数据。

可以解析来自Adobe Experience Platform的JSON响应，以查找您与Adobe Experience Platform集成的应用程序的相应集成别名。 受众ID可以作为定位参数传递到应用程序的代码中。 以下是目标响应特有的内容示例。

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
        var personalizationDestinations = result.destinations.filter(x => x.alias == "personalizationAlias")
        if(personalizationDestinations.length > 0) {
             // Code to pass the audience IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the audience IDs into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### 的示例响应 [!UICONTROL 使用属性进行自定义个性化]

使用时 **[!UICONTROL 使用属性进行自定义个性化]**，则API响应将与以下示例类似。

两者之间的差异 **[!UICONTROL 使用属性进行自定义个性化]** 和 **[!UICONTROL 自定义个性化]** 是包含 `attributes` 部分。

```json
[
    {
        "type": "profileLookup",
        "destinationId": "7bb4cb8d-8c2e-4450-871d-b7824f547130",
        "alias": "personalizationAlias",
        "attributes": {
             "countryCode": {
                   "value" : "DE"
              },
             "membershipStatus": {
                   "value" : "PREMIUM"
              }
         },         
        "segments": [
            {
                "id": "399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            },
            {
                "id": "499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            }
        ]
    }
]
```

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据管理概述](../../../data-governance/home.md).
