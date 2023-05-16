---
description: 本页说明了用于通过Adobe Experience Platform Destination SDK创建受众模板的API调用。
title: 创建受众模板
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 3%

---


# 创建受众模板

>[!IMPORTANT]
>
>**API端点**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

对于使用Destination SDK创建的某些目标，您需要创建受众元数据配置，以编程方式在目标中创建、更新或删除区段元数据。 本页将向您展示如何使用 `/authoring/audience-templates` 用于创建配置的API端点。

有关可通过此端点配置的功能的详细说明，请参阅 [受众元数据管理](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均为 **区分大小写**. 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 受众模板API操作快速入门 {#get-started}

在继续之前，请查看 [入门指南](../getting-started.md) 有关成功调用API所需的重要信息，包括如何获取所需的目标创作权限和所需标头。

## 创建受众模板 {#create}

您可以通过创建 `POST` 请求 `/authoring/audience-templates` 端点。

**API格式**

```http
POST /authoring/audience-templates
```

+++请求

以下请求会创建新受众模板，该模板由有效负载中提供的参数进行配置。 以下负载包括接受的所有参数 `/authoring/audience-templates` 端点。 请注意，您不必在调用中添加所有参数，并且该模板可根据您的API要求进行自定义。

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
| `name` | 字符串 | 目标的受众元数据模板的名称。 此名称将显示在Experience Platform用户界面中任何特定于合作伙伴的错误消息中，然后显示从中解析的错误消息 `metadataTemplate.create.errorSchemaMap`. |
| `url` | 字符串 | API的URL和端点，用于创建、更新、删除或验证平台中的受众/区段。 两个行业示例： `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` 和 `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | 字符串 | 您端点上用于以编程方式创建、更新、删除或验证目标中的区段/受众的方法。 例如： `POST`, `PUT`, `DELETE` |
| `headers.header` | 字符串 | 指定应添加到API调用中的任何HTTP标头。 例如：`"Content-Type"` |
| `headers.value` | 字符串 | 指定应添加到API调用中的HTTP标头值。 例如：`"application/x-www-form-urlencoded"` |
| `requestBody` | 字符串 | 指定应发送到API的消息正文的内容。 应添加到的参数 `requestBody` 对象取决于API接受的字段。 有关示例，请参阅 [第一个模板示例](../functionality/audience-metadata-management.md#example-1) （在受众元数据功能文档中）。 |
| `responseFields.name` | 字符串 | 指定API在调用时返回的任何响应字段。 有关示例，请参阅 [模板示例](../functionality/audience-metadata-management.md#examples) （在受众元数据功能文档中）。 |
| `responseFields.value` | 字符串 | 指定API在调用时返回的任何响应字段的值。 |
| `responseErrorFields.name` | 字符串 | 指定API在调用时返回的任何响应字段。 有关示例，请参阅 [ 模板示例](../functionality/audience-metadata-management.md#examples) （在受众元数据功能文档中）。 |
| `responseErrorFields.value` | 字符串 | 解析在从您的目标进行API调用响应时返回的任何错误消息。 这些错误消息将在Experience Platform用户界面中显示给用户。 |
| `validations.field` | 字符串 | 指示在对目标进行API调用之前是否应对任何字段运行验证。 例如，您可以使用 `{{validations.accountId}}` 验证用户的帐户ID。 |
| `validations.regex` | 字符串 | 指示字段的结构方式，以便验证通过。 |

{style="table-layout:auto"}

+++

+++响应

成功响应会返回HTTP状态200，其中包含新创建受众模板的详细信息。

+++

## API错误处理

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中。

## 后续步骤

阅读本文档后，您现在可以了解何时使用受众模板以及如何使用配置受众模板 `/authoring/audience-templates` API端点。 读取 [如何使用Destination SDK配置目标](../guides/configure-destination-instructions.md) 以了解此步骤在配置目标过程中的适用位置。
