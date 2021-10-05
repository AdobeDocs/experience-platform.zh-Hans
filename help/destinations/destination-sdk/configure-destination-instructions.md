---
description: 本页介绍如何使用目标SDK配置选项中的参考信息，使用目标SDK配置您的目标。
seo-description: This page describes how to use the reference information in Configuration options for the Destinations SDK to configure your destination using Destination SDK.
seo-title: How to use Destination SDK to configure your destination
title: 如何使用Destination SDK配置目标
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 32b61276f3fe81ffa82fec1debf335ea51020ccd
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---

# 如何使用Destination SDK配置目标

## 概述 {#overview}

本页介绍如何使用[目标SDK](./configuration-options.md)中的配置选项中的参考信息配置目标。 这些步骤按如下顺序排列。

## 先决条件 {#prerequisites}

在前进到下述步骤之前，请阅读[目标SDK快速入门](./getting-started.md)页面，以了解有关获取使用目标SDK API所需的Adobe I/O身份验证凭据和其他先决条件的信息。

## 使用目标SDK中的配置选项设置目标的步骤 {#steps}

![使用目标SDK端点的图示步骤](./assets/destination-sdk-steps.png)

## 步骤1:创建服务器和模板配置 {#create-server-template-configuration}

首先，使用`/destinations-server`端点创建服务器和模板配置（读取[API引用](./destination-server-api.md)）。 有关服务器和模板配置的详细信息，请参阅参考部分中的[服务器和模板规范](./configuration-options.md#server-and-template)。

下面显示了一个配置示例。 请注意，`requestBody.value`参数中的消息转换模板在步骤3 [创建转换模板](./configure-destination-instructions.md#create-transformation-template)中已处理。

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

下面显示了使用`/destinations` API端点创建的目标模板配置示例。 有关此模板的更多信息，请参阅[目标配置](./destination-configuration.md)。

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
         "maxBatchAgeInSecs":360,
         "maxNumEventsInBatch":100
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

您必须根据目标支持的负载创建一个模板，以将导出数据的格式从AdobeXDM格式转换为目标支持的格式。 请参阅[使用模板语言进行身份、属性和区段成员转换](./message-format.md#using-templating)部分中的模板示例，并使用Adobe提供的[模板创作工具](./create-template.md)。

## 步骤4:创建受众元数据配置 {#create-audience-metadata-configuration}

对于某些目标，目标SDK要求您配置受众元数据模板，以编程方式创建、更新或删除目标中的受众。 有关何时需要设置此配置以及如何设置此配置的信息，请参阅[受众元数据管理](./audience-metadata-management.md)。

## 步骤5:创建凭据配置/设置身份验证 {#set-up-authentication}

根据您在上述目标配置中指定的是`"authenticationRule": "CUSTOMER_AUTHENTICATION"`还是`"authenticationRule": "PLATFORM_AUTHENTICATION"`，可以使用`/destination`或`/credentials`端点设置目标的身份验证。

* **最常见的情况**:如果您已选 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 择并且目标支持OAuth 2身份验证方法，请读取 [OAuth 2身份验证](./oauth2-authentication.md)。
* 如果您选择了`"authenticationRule": "PLATFORM_AUTHENTICATION"`，请参阅参考文档中的[凭据配置](./credentials-configuration.md) 。

## 步骤6:测试目标 {#test-destination}

使用上面步骤中的模板设置目标后，可以使用[目标测试工具](./create-template.md)测试Adobe Experience Platform与目标之间的集成。

在测试目标的过程中，您必须使用Experience PlatformUI创建区段，然后才能将区段激活到目标。 有关如何在Experience Platform中创建区段的说明，请参阅以下两个资源：

* [创建区段文档页面](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [创建区段视频演练](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)


## 步骤7:发布目标 {#publish-destination}

配置并测试目标后，使用[目标发布API](./destination-publish-api.md)将配置提交给Adobe以供审核。

## 步骤8:记录目标 {#document-destination}

如果您是创建[产品化集成](./overview.md#productized-custom-integrations)的独立软件供应商(ISV)或系统集成商(SI)，请使用[自助服务文档流程](./docs-framework/documentation-instructions.md)为[Experience League目标目录](/help/destinations/catalog/overview.md)中的目标创建产品文档页面。
