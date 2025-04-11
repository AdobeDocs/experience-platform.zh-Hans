---
keywords: 自定义个性化；目标；experience platform自定义目标；
title: 自定义个性化连接
description: 此目标提供外部个性化、内容管理系统、广告服务器以及在您的网站上运行的其他应用程序，以便从Adobe Experience Platform检索受众信息。 此目标根据用户个人资料受众成员资格提供实时个性化。
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 0f70e072402bca055b96195ded91816810759fc2
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 9%

---


# 自定义个性化连接 {#custom-personalization-connection}

## 目标更改日志 {#changelog}

| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2023 年 5 月 | 功能和文档更新 | 自2023年5月起，**[!UICONTROL 自定义个性化]**&#x200B;连接支持[基于属性的个性化](../../ui/activate-edge-personalization-destinations.md#map-attributes)，通常可供所有客户使用。 |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>配置文件属性可能包含敏感数据。 要保护此数据，在为基于属性的个性化配置&#x200B;**[!UICONTROL 自定义Personalization]**&#x200B;目标时，必须使用[Edge Network服务器API](/help/server-api/overview.md)。 所有服务器API调用必须在[经过身份验证的上下文](../../../server-api/authentication.md)中进行。
>
><br>您可以添加一个服务器端集成，该集成利用您已经用于Web或Mobile SDK实施的相同数据流，从而通过[Edge Network Server API](/help/server-api/overview.md)检索配置文件属性。
>
><br>如果不遵循上述要求，则仅基于受众成员资格进行个性化。

## 概述 {#overview}

设置此目标以允许客户网站上运行的外部个性化平台、内容管理系统、广告服务器和其他应用程序从Adobe Experience Platform检索受众信息。

## 先决条件 {#prerequisites}

根据您的实施，此目标需要使用以下数据收集方法之一：

* 如果要从您的网站收集数据，请使用[Adobe Experience Platform Web SDK](/help/web-sdk/home.md)。
* 如果要从移动应用程序收集数据，请使用[Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)。
* 如果您未使用[Web SDK](/help/web-sdk/home.md)或[Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)，或者要根据配置文件属性个性化用户体验，请使用[Edge Network服务器API](../../../server-api/overview.md)。

>[!IMPORTANT]
>
>在创建自定义个性化连接之前，请阅读有关如何[将受众数据激活到边缘个性化目标](../../ui/activate-edge-personalization-destinations.md)的指南。 本指南将指导您跨多个Experience Platform组件完成相同页面和下一页面个性化用例所需的配置步骤。

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!DNL Profile request]** | 您正在请求在单个配置文件的自定义个性化目标中映射的所有受众。 可以为不同的[Adobe数据收集数据流](../../../datastreams/overview.md)设置不同的自定义个性化目标。 |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

## 连接到目标 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="关于数据流 ID"
>abstract="此选项确定受众将包含在哪个数据收集数据流中以响应页面。下拉菜单仅显示已启用目标配置的数据流。您必须先配置数据流，然后才能配置目标。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html#" text="了解如何配置数据流"

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL 名称]**：填写此目标的首选名称。
* **[!UICONTROL 描述]**：输入目标的描述。 例如，您可以提及要将此目标用于哪个营销活动。 此字段为可选字段。
* **[!UICONTROL 集成别名]**：此值作为JSON对象名称发送到Experience Platform Web SDK。
* **[!UICONTROL 数据流ID]**：这决定了页面的响应中将包含受众的数据收集数据流。 下拉菜单仅显示已启用目标配置的数据流。有关详细信息，请参阅[配置数据流](../../../datastreams/overview.md)。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将受众激活到此目标的说明，请阅读[激活配置文件和受众边缘个性化目标](../../ui/activate-edge-personalization-destinations.md)。

## 导出的数据 {#exported-data}

如果您使用Adobe Experience Platform中的[Tags](../../../tags/home.md)来部署Experience Platform Web SDK，请使用[发送事件完成](../../../tags/extensions/client/web-sdk/event-types.md)功能，您的自定义代码操作将具有`event.destinations`变量，您可以使用它查看导出的数据。

以下是`event.destinations`变量的示例值：

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

如果您没有使用[标记](/help/tags/home.md)来部署Experience Platform Web SDK，请使用[命令响应](/help/web-sdk/commands/command-responses.md)来查看导出的数据。

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

### 具有属性]的[!UICONTROL 自定义Personalization的示例响应

使用具有属性&#x200B;]**的**[!UICONTROL &#x200B;自定义Personalization时，API响应将与以下示例类似。

**[!UICONTROL 具有属性的自定义Personalization]**&#x200B;与&#x200B;**[!UICONTROL 自定义Personalization]**&#x200B;之间的区别在于API响应中包含`attributes`部分。

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

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](../../../data-governance/home.md)。
