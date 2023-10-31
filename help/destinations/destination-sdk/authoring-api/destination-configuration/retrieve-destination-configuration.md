---
description: 本页举例说明了用于通过Adobe Experience Platform Destination SDK检索目标配置的API调用。
title: 检索目标配置
exl-id: aaf4cfa0-3e90-4fcc-b506-b84ff62b3027
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---

# 检索目标配置

本页举例说明了API请求和有效负载，您可以使用这些API请求和有效负载检索有关现有目标配置的信息。 `/authoring/destination` API端点。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值包括 **区分大小写**. 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 目标配置API操作快速入门 {#get-started}

在继续之前，请查看 [快速入门指南](../../getting-started.md) 获取成功调用API所需了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 检索目标配置 {#retrieve}

您可以检索 [现有](create-destination-configuration.md) 目标配置，方法是 `GET` 请求 `/authoring/destination` 端点。

>[!TIP]
>
>**API端点**： `platform.adobe.io/data/core/activation/authoring/destinations`


**API格式**

使用以下API格式检索帐户的所有目标配置。

```http
GET /authoring/destinations
```

使用以下API格式检索由定义的特定目标配置 `{INSTANCE_ID}` 参数。

```http
GET /authoring/destinations/{INSTANCE_ID}
```

以下两个请求检索IMS组织的所有目标配置，或特定的目标配置，具体取决于您是否传递 `INSTANCE_ID` 请求中的参数。

选择下面的每个选项卡以查看相应的有效负载。

>[!BEGINTABS]

>[!TAB 检索所有目标配置]

+++请求

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++响应

成功的响应会返回HTTP状态200，其中包含您有权访问的目标配置列表，该列表基于 [!DNL IMS Org ID] 和您使用的沙盒名称之间的关联。 一 `instanceId` 对应于一个目标配置。

```json
{
   "items":[
      {
         "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
         "createdDate":"2020-10-28T06:14:09.784471Z",
         "lastModifiedDate":"2021-06-28T06:14:09.784471Z",
         "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
         "sandboxName":"prod",
         "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
               "pattern":"^[A-Za-z]+$"
            }
         ],
         "uiAttributes":{
            "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
            "category":"mobile",
            "connectionType":"Server-to-server",
            "frequency":"Streaming"
         },
         "identityNamespaces":{
            "external_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true,
               "acceptedGlobalNamespaces":{
                  "Email":{

                  }
               }
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
         "schemaConfig":{
            "profileFields":[
               {
                  "name":"a_custom_attribute",
                  "title":"a_custom_attribute",
                  "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
                  "type":"string",
                  "isRequired":false,
                  "readOnly":false,
                  "hidden":false
               }
            ],
            "profileRequired":true,
            "segmentRequired":true,
            "identityRequired":true
         },
         "aggregation":{
            "aggregationType":"BEST_EFFORT",
            "bestEffortAggregation":{
               "maxUsersPerRequest":10,
               "splitUserById":false
            }
         },
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "destConfigId":"410631b8-f6b3-4b7c-82da-7998aa3f327c",
         "backfillHistoricalProfileData":true
      }
   ]
}
```

+++

>[!TAB 检索特定目标配置]

+++请求

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 参数 | 描述 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要检索的目标配置的ID。 |

+++

+++响应

成功的响应返回HTTP状态200，其中包含与对应的目标配置的详细信息 `{INSTANCE_ID}` 在调用中提供。

```json
{
   "items":[
      {
         "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
         "createdDate":"2020-10-28T06:14:09.784471Z",
         "lastModifiedDate":"2021-06-28T06:14:09.784471Z",
         "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
         "sandboxName":"prod",
         "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
               "pattern":"^[A-Za-z]+$"
            }
         ],
         "uiAttributes":{
            "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
            "category":"mobile",
            "connectionType":"Server-to-server",
            "frequency":"Streaming"
         },
         "identityNamespaces":{
            "external_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true,
               "acceptedGlobalNamespaces":{
                  "Email":{

                  }
               }
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
         "schemaConfig":{
            "profileFields":[
               {
                  "name":"a_custom_attribute",
                  "title":"a_custom_attribute",
                  "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
                  "type":"string",
                  "isRequired":false,
                  "readOnly":false,
                  "hidden":false
               }
            ],
            "profileRequired":true,
            "segmentRequired":true,
            "identityRequired":true
         },
         "aggregation":{
            "aggregationType":"BEST_EFFORT",
            "bestEffortAggregation":{
               "maxUsersPerRequest":10,
               "splitUserById":false
            }
         },
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "destConfigId":"410631b8-f6b3-4b7c-82da-7998aa3f327c",
         "backfillHistoricalProfileData":true
      }
   ]
}
```

+++

>[!ENDTABS]

## API错误处理 {#error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../../landing/troubleshooting.md#request-header-errors) ，位于平台疑难解答指南中。

## 后续步骤

阅读本文档后，您现在知道如何通过Destination SDK检索目标配置 `/authoring/destinations` API端点。

要了解有关可使用此端点执行的操作的更多信息，请参阅以下文章：

* [创建目标配置](create-destination-configuration.md)
* [更新目标配置](update-destination-configuration.md)
* [删除目标配置](delete-destination-configuration.md)
