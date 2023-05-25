---
description: 本页举例说明了用于通过Adobe Experience Platform Destination SDK创建受众模板的API调用。
title: 创建受众模板
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 3%

---


# 创建受众模板

>[!IMPORTANT]
>
>**API端点**： `platform.adobe.io/data/core/activation/authoring/audience-templates`

对于使用Destination SDK创建的某些目标，您需要创建受众元数据配置，以便以编程方式在目标中创建、更新或删除区段元数据。 本页向您说明如何使用 `/authoring/audience-templates` 用于创建配置的API端点。

有关可通过此端点配置的功能的详细说明，请参阅 [受众元数据管理](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值包括 **区分大小写**. 为避免区分大小写错误，请完全按照文档中所示使用参数名称和值。

## 受众模板API操作快速入门 {#get-started}

在继续之前，请查看 [快速入门指南](../getting-started.md) 要成功调用API需要了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 创建受众模板 {#create}

您可以通过创建 `POST` 请求 `/authoring/audience-templates` 端点。

**API格式**

```http
POST /authoring/audience-templates
```

+++请求

以下请求创建一个新的受众模板，该模板由有效负载中提供的参数配置。 以下有效负载包含由接受的所有参数 `/authoring/audience-templates` 端点。 请注意，您无需在调用中添加所有参数，并且可根据您的API要求自定义模板。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "name":"string",
      "create":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "update":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "delete":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "validate":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "notify":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      }
   },
   "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| 属性 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `name` | 字符串 | 目标的受众元数据模板的名称。 此名称将显示在Experience Platform用户界面中任何特定于合作伙伴的错误消息中，其后是分析自的错误消息 `metadataTemplate.create.errorSchemaMap`. |
| `url` | 字符串 | API的URL和端点，用于创建、更新、删除或验证平台中的受众/区段。 两个行业示例是： `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` 和 `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | 字符串 | 在您的端点上用于以编程方式创建、更新、删除或验证目标中的区段/受众的方法。 例如： `POST`， `PUT`， `DELETE` |
| `headers.header` | 字符串 | 指定应添加到API调用的任何HTTP标头。 例如：`"Content-Type"` |
| `headers.value` | 字符串 | 指定应添加到API调用中的HTTP标头的值。 例如：`"application/x-www-form-urlencoded"` |
| `requestBody` | 字符串 | 指定应发送到API的消息正文的内容。 应添加到 `requestBody` 对象取决于API接受的字段。 有关示例，请参阅 [第一个模板示例](../functionality/audience-metadata-management.md#example-1) （位于受众元数据功能文档中）。 |
| `responseFields.name` | 字符串 | 指定在调用时API返回的任何响应字段。 有关示例，请参阅 [模板示例](../functionality/audience-metadata-management.md#examples) （位于受众元数据功能文档中）。 |
| `responseFields.value` | 字符串 | 指定API在调用时返回的任何响应字段的值。 |
| `responseErrorFields.name` | 字符串 | 指定在调用时API返回的任何响应字段。 有关示例，请参阅 [ 模板示例](../functionality/audience-metadata-management.md#examples) （位于受众元数据功能文档中）。 |
| `responseErrorFields.value` | 字符串 | 解析从目标发出的API调用响应中返回的任何错误消息。 这些错误消息将在Experience Platform用户界面中向用户显示。 |
| `validations.field` | 字符串 | 指示在对目标进行API调用之前是否应对任何字段运行验证。 例如，您可以使用 `{{validations.accountId}}` 验证用户的帐户ID。 |
| `validations.regex` | 字符串 | 指示字段应如何构建才能通过验证。 |

{style="table-layout:auto"}

+++

+++响应

成功响应会返回HTTP状态200以及新创建的受众模板的详细信息。

+++

## API错误处理

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中的。

## 后续步骤

阅读本文档后，您现在知道何时使用受众模板以及如何使用配置受众模板 `/authoring/audience-templates` API端点。 读取 [如何使用Destination SDK配置目标](../guides/configure-destination-instructions.md) 以了解此步骤在配置目标的过程中所处的位置。
