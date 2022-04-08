---
description: 本页列出并描述了使用Destination SDK配置流目标的步骤。
title: 使用Destination SDK配置流目标
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 51417bee5dba7a96d3a7a7eb507fc95711fad4a5
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# 使用Destination SDK配置流目标

## 概述 {#overview}

本页介绍如何使用 [目标SDK中的配置选项](./configuration-options.md) 和其他Destination SDK功能和API参考文档中的 [流目标](/help/destinations/destination-types.md#streaming-destinations). 这些步骤按如下顺序排列。

## 先决条件 {#prerequisites}

在前进到下述步骤之前，请阅读 [Destination SDK入门](./getting-started.md) 页面，以了解有关获取使用Adobe I/OAPI所需的Destination SDK身份验证凭据以及其他先决条件的信息。

## 使用Destination SDK中的配置选项设置目标的步骤 {#steps}

![使用Destination SDK端点的图示步骤](./assets/destination-sdk-steps.png)

## 步骤1:创建服务器和模板配置 {#create-server-template-configuration}

首先，使用 `/destinations-server` 端点（读取） [API参考](destination-server-api.md))。 有关服务器和模板配置的详细信息，请参阅 [服务器和模板规范](server-and-template-configuration.md) 在参考部分中。

下面显示了一个配置示例。 请注意， `requestBody.value` 参数在步骤3中进行说明， [创建转换模板](./configure-destination-instructions.md#create-transformation-template).

```json
POST platform.adobe.io/data/core/activation/authoring/destination-servers

{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"insert after you create a template in step 3"
      },
      "contentType":"application/json"
   }
}
```

## 步骤2:创建目标配置 {#create-destination-configuration}

下面显示了目标模板的配置示例，该配置是使用 `/destinations` API端点。 有关此配置的更多信息，请参阅 [目标配置](./destination-configuration.md).

要将步骤1中的服务器和模板配置连接到此目标配置，请将服务器和模板配置的实例ID添加为 `destinationServerId` 这里。

>[!IMPORTANT]
>
>要创建正确配置的目标，您需要 *必须* 在 `identityNamespaces`，如下所示。 如果未配置目标标识，则用户将无法继续通过 [映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 激活工作流的URL。

```json
POST platform.adobe.io/data/core/activation/authoring/destinations
 
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },   
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```

## 步骤3:创建消息转换模板 — 使用模板语言指定消息输出格式 {#create-transformation-template}

您必须根据目标支持的负载创建一个模板，以将导出数据的格式从AdobeXDM格式转换为目标支持的格式。 请参阅部分中的模板示例 [对身份、属性和区段成员资格转换使用模板语言](./message-format.md#using-templating) 并使用 [模板创作工具](./create-template.md) 由Adobe提供。

构建适合您的消息转换模板后，将其添加到在步骤1中创建的服务器和模板配置中。

## 步骤4:创建受众元数据配置 {#create-audience-metadata-configuration}

对于某些目标，Destination SDK要求您配置受众元数据配置，以编程方式创建、更新或删除目标中的受众。 请参阅 [受众元数据管理](./audience-metadata-management.md) 有关何时需要设置此配置以及如何进行此配置的信息。

如果您使用受众元数据配置，则必须将其连接到在步骤2中创建的目标配置。 将受众元数据配置的实例ID添加到目标配置中，如 `audienceTemplateId`.

## 步骤5:设置身份验证 {#set-up-authentication}

取决于您是否指定 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 或 `"authenticationRule": "PLATFORM_AUTHENTICATION"` 在上述目标配置中，您可以使用 `/destination` 或 `/credentials` 端点。

* **最常见案例**:如果已选择 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 在目标配置中，您的目标支持OAuth 2身份验证方法，请阅读 [OAuth 2身份验证](./oauth2-authentication.md).
* 如果已选择 `"authenticationRule": "PLATFORM_AUTHENTICATION"`，请参阅 [身份验证配置](./authentication-configuration.md#when-to-use).

## 步骤6:测试目标 {#test-destination}

使用上一步中的配置端点设置目标后，您可以使用 [目标测试工具](./test-destination.md) 以测试Adobe Experience Platform与您的目标之间的集成。

在测试目标的过程中，您必须使用Experience PlatformUI创建区段，然后才能将区段激活到目标。 有关如何在Experience Platform中创建区段的说明，请参阅以下两个资源：

* [创建区段文档页面](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [创建区段视频演练](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## 步骤7:发布目标 {#publish-destination}

配置和测试目标后，请使用 [目标发布API](./destination-publish-api.md) 将配置提交到Adobe以供审核。

## 步骤8:记录目标 {#document-destination}

如果您是独立软件供应商(ISV)或系统集成商(SI)，创建 [产品化集成](./overview.md#productized-custom-integrations)，则使用 [自助文档流程](./docs-framework/documentation-instructions.md) 要在 [Experience Platform目标目录](/help/destinations/catalog/overview.md).
