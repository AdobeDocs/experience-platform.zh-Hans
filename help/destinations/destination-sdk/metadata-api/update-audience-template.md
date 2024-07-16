---
description: 本页举例说明了用于通过Adobe Experience Platform Destination SDK更新受众模板的API调用。
title: 更新受众模板
exl-id: 8185a015-256d-46a7-af33-8475832fb6c1
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 1%

---

# 更新受众模板

>[!IMPORTANT]
>
>**API终结点**： `platform.adobe.io/data/core/activation/authoring/audience-templates`

此页面展示了可用于通过`/authoring/audience-templates` API端点更新受众模板的API请求和有效负荷。

有关可通过此端点配置的功能的详细说明，请参阅[受众元数据管理](../functionality/audience-metadata-management.md)。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;****。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 受众模板API操作快速入门 {#get-started}

在继续之前，请查看[入门指南](../getting-started.md)以了解成功调用API所需了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 更新受众模板 {#create}

您可以通过向`/authoring/audience-templates`终结点发出包含已更新有效负载的`PUT`请求来更新[现有](create-audience-template.md)受众模板。

要获取现有的受众模板及其对应的`{INSTANCE_ID}`，请参阅有关[检索受众模板](retrieve-audience-template.md)的文章。

**API格式**

```http
PUT /authoring/audience-templates/{INSTANCE_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要更新的受众模板的ID。 要获取现有的受众模板及其对应的`{INSTANCE_ID}`，请参阅[检索受众模板](retrieve-audience-template.md)。 |

以下请求更新现有的受众元数据模板，该模板由有效负载中提供的参数配置。

+++请求

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1.0/{{customerData.accountId}}/customaudiences?fields=name,description,account_id&subtype=CUSTOM&name={{segment.name}}&customer_file_source={{segment.metadata.customer_file_source}}&access_token={{authData.accessToken}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?field=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}&&name={{segment.name}}&description={{segment.description}}&customer_file_source={{segment.metadata.customer_file_source}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?fields=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "validate":{
         "url":"https://api.moviestar.com/v1.0/permissions?access_token={{authData.accessToken}}",
         "httpMethod":"GET",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.data[0].permission}}",
               "name":"Id"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      }
   }
}'
```

+++

+++响应

成功的响应返回HTTP状态200以及已更新受众模板的详细信息。

+++

## API错误处理

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅平台疑难解答指南中的[API状态代码](../../../landing/troubleshooting.md#api-status-codes)和[请求标头错误](../../../landing/troubleshooting.md#request-header-errors)。

## 后续步骤

阅读本文档后，您现在知道何时使用受众模板以及如何使用`/authoring/audience-templates` API端点更新受众模板。 阅读[如何使用Destination SDK配置目标](../guides/configure-destination-instructions.md)，以了解此步骤在配置目标的过程中所处的位置。
