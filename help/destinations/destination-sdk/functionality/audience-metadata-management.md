---
description: 使用受众元数据模板以编程方式创建、更新或删除目标中的受众。 Adobe提供了一个可扩展的受众元数据模板，您可以根据营销API的规范配置该模板。 定义、测试和提交模板后，Adobe会使用该模板来构建到您目标的API调用。
title: 受众元数据管理
source-git-commit: e69bd819fb8ef6c2384a2b843542d1ddcea0661f
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 0%

---


# 受众元数据管理

使用受众元数据模板以编程方式创建、更新或删除目标中的受众。 Adobe提供了一个可扩展的受众元数据模板，您可以根据营销API的规范配置该模板。 定义、测试和提交配置后，Adobe将使用该配置来构建到目标的API调用。

您可以使用 `/authoring/audience-templates` API端点。 读取 [创建元数据模板](../metadata-api/create-audience-template.md) 有关可对端点执行的操作的完整列表。

## 何时使用受众元数据管理端点 {#when-to-use}

根据您的API配置，在Experience Platform中配置目标时，您可能需要使用受众元数据管理端点，也可能不需要使用。 使用下面的决策树图可了解何时使用受众元数据端点以及如何为目标配置受众元数据模板。

![决策树图](../assets/functionality/audience-metadata-decision-tree.png)

## 受众元数据管理支持的用例 {#use-cases}

借助Destination SDK中的受众元数据支持，在配置Experience Platform目标时，您可以在Platform用户映射区段并激活区段到目标时，为其提供以下几个选项之一。 您可以通过 [受众元数据配置](../functionality/destination-configuration/audience-metadata-configuration.md) 目标配置的部分。

### 用例1 — 您具有第三方API，用户无需输入映射ID

如果您有用于创建/更新/删除区段或受众的API端点，则可以使用受众元数据模板配置Destination SDK，以匹配区段创建/更新/删除端点的规范。 Experience Platform可以以编程方式创建/更新/删除区段，并将元数据同步回Experience Platform。

在Experience Platform用户界面(UI)中将区段激活到目标时，用户无需在激活工作流中手动填写区段映射ID字段。

### 用例2 — 用户需要先在目标中创建区段，并且需要手动输入映射ID

如果区段和其他元数据需要由合作伙伴或用户在您的目标中手动创建，则用户必须在激活工作流中手动填写区段映射ID字段，以在您的目标和Experience Platform之间同步区段元数据。

![输入映射ID](../assets/functionality/input-mapping-id.png)

### 用例3 — 您的目标接受Experience Platform区段ID，用户无需手动输入映射ID

如果您的目标系统接受Experience Platform区段ID，则可以在受众元数据模板中配置此ID。 激活区段时，用户无需填充区段映射ID。

## 通用且可扩展的受众模板 {#generic-and-extensible}

为了支持上面列出的用例，Adobe为您提供了一个通用模板，可通过自定义来调整API规范。

您可以使用通用模板 [创建新受众模板](../metadata-api/create-audience-template.md) 如果您的API支持：

* HTTP方法：POST、GET、PUT、DELETE、PATCH
* 身份验证类型：OAuth 1、具有刷新令牌的OAuth 2、具有载体令牌的OAuth 2
* 函数：创建受众、更新受众、获取受众、删除受众、验证凭据

如果您的用例需要，Adobe工程团队可以与您合作，扩展带有自定义字段的通用模板。

## 配置示例 {#configuration-examples}

本节包含三个供您参考的通用受众元数据配置示例，以及配置主要部分的描述。 请注意三个示例配置中的url、标头、请求和响应正文有何不同。 这是由于三个示例平台营销API的不同规范所致。

请注意，在某些示例中，宏字段如 `{{authData.accessToken}}` 或 `{{segment.name}}` 在URL中使用，在其他示例中，在标头或请求正文中使用。 这真的取决于您的营销API规范。

| 模板部分 | 描述 |
|--- |--- |
| `create` | 包括对您的API进行HTTP调用、以编程方式在您的平台中创建区段/受众，并将信息同步回Adobe Experience Platform的所有必需组件（URL、HTTP方法、标头、请求和响应正文）。 |
| `update` | 包括对您的API进行HTTP调用、以编程方式更新平台中的区段/受众，以及将信息同步回Adobe Experience Platform的所有必需组件（URL、HTTP方法、标头、请求和响应正文）。 |
| `delete` | 包括对您的API进行HTTP调用以编程方式删除平台中的区段/受众的所有必需组件（URL、HTTP方法、标头、请求和响应正文）。 |
| `validate` | 在调用合作伙伴API之前，对模板配置中的任何字段运行验证。 例如，您可以验证是否正确输入了用户的帐户ID。 |
| `notify` | 仅适用于基于文件的目标。 包括对您的API进行HTTP调用以通知文件导出成功的所有必需组件（URL、HTTP方法、标头、请求和响应正文）。 |

{style="table-layout:auto"}

### 流示例1 {#example-1}

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```

### 流示例2 {#example-2}

```json
{
   "instanceId":"12c78017-5af3-4d4e-8f9c-d330c547c482",
   "createdDate":"2021-07-20T13:27:37.029490Z",
   "lastModifiedDate":"2021-07-20T18:53:03.622306Z",
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
}
```

### 流示例3 {#example-3}

```json
{
   "instanceId":"12a3238f-b509-4a40-b8fb-0a5006e7901d",
   "createdDate":"2021-07-20T13:30:30.843054Z",
   "lastModifiedDate":"2021-07-21T16:33:05.787472Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v2/dmpSegments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{authData.accessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "name":"{{segment.name}}",
               "type":"USER",
               "account":"{{customerData.accountId}}",
               "accessPolicy":"PRIVATE",
               "destinations":[
                  {
                     "destination":"MOVIESTAR"
                  }
               ],
               "sourcePlatform":"ADOBE"
            }
         },
         "responseFields":[
            {
               "value":"{{headers.x-moviestar-id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{authData.accessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "patch":{
                  "$set":{
                     "name":"{{segment.name}}"
                  }
               }
            }
         },
         "responseErrorFields":[
            {
               "value":"{{message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{authData.accessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{message}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar audience template - Third example"
   }
}
```


### 基于文件的示例 {#example-file-based}

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "notify":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```

在 [创建受众模板](../metadata-api/create-audience-template.md) API引用。

## 受众元数据模板中使用的宏

要在Experience Platform和API之间传递信息（如区段ID、访问令牌、错误消息等），受众模板包含可使用的宏。 请阅读下文对本页上三个配置示例中使用的宏的描述：

| 宏 | 描述 |
|--- |--- |
| `{{segment.alias}}` | 用于在Experience Platform中访问区段别名。 |
| `{{segment.name}}` | 用于在Experience Platform中访问区段名称。 |
| `{{segment.id}}` | 允许您在Experience Platform中访问区段ID。 |
| `{{customerData.accountId}}` | 允许您访问在目标配置中设置的帐户ID字段。 |
| `{{oauth2ServiceAccessToken}}` | 允许您根据OAuth 2配置动态生成访问令牌。 |
| `{{authData.accessToken}}` | 允许您将访问令牌传递到API端点。 使用 `{{authData.accessToken}}` 如果Experience Platform应使用未过期的令牌连接到您的目标，请使用 `{{oauth2ServiceAccessToken}}` 以生成访问令牌。 |
| `{{body.segments[0].segment.id}}` | 返回已创建受众的唯一标识符，作为键的值 `externalAudienceId`. |
| `{{error.message}}` | 返回将在Experience PlatformUI中向用户显示的错误消息。 |

{style="table-layout:auto"}
