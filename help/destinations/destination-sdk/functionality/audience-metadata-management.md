---
description: 使用受众元数据模板以编程方式创建、更新或删除目标中的受众。 Adobe提供了一个可扩展的受众元数据模板，您可以根据营销API的规范配置该模板。 在定义、测试和提交模板后，Adobe将使用该模板来构建对目标的调用API。
title: 受众元数据管理
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 0%

---


# 受众元数据管理

使用受众元数据模板以编程方式创建、更新或删除目标中的受众。 Adobe提供了一个可扩展的受众元数据模板，您可以根据营销API的规范配置该模板。 定义、测试和提交配置后，Adobe将使用该配置来构造指向目标的API调用。

您可以使用配置本文档中描述的功能 `/authoring/audience-templates` API端点。 读取 [创建元数据模板](../metadata-api/create-audience-template.md) 有关可在端点上执行的操作的完整列表。

## 何时使用受众元数据管理端点 {#when-to-use}

根据您的API配置，在Experience Platform中配置目标时，您可能需要也可能不需要使用受众元数据管理端点。 使用下面的决策树图表了解何时使用受众元数据端点以及如何为目标配置受众元数据模板。

![决策树图](../assets/functionality/audience-metadata-decision-tree.png)

## 受众元数据管理支持的用例 {#use-cases}

借助Destination SDK中的受众元数据支持，在配置Experience Platform目标时，您可以为Platform用户提供以下几个选项之一，以便他们映射和激活受众到您的目标。 您可以通过 [受众元数据配置](../functionality/destination-configuration/audience-metadata-configuration.md) 部分。

### 用例1 — 您有一个第三方API，用户无需输入映射ID

如果您具有用于创建/更新/删除受众或受众的API端点，则可以使用受众元数据模板来配置Destination SDK，以匹配受众创建/更新/删除端点的规范。 Experience Platform能够以编程方式创建/更新/删除受众，并将元数据同步回Experience Platform。

在Experience Platform用户界面(UI)中将受众激活到目标时，用户无需在激活工作流中手动填写受众映射ID字段。

### 用例2 — 用户需要首先在您的目标中创建受众，并需要手动输入映射ID

如果受众和其他元数据需要由合作伙伴或用户在您的目标中手动创建，则用户必须在激活工作流中手动填写受众映射ID字段，以在您的目标和Experience Platform之间同步受众元数据。

![输入映射Id](../assets/functionality/input-mapping-id.png)

### 用例3 — 您的目标接受Experience Platform的受众ID，用户无需手动输入映射ID

如果目标系统接受Experience Platform的受众ID，则可以在受众元数据模板中配置此模板。 用户在激活区段时无需填充受众映射ID。

## 通用且可扩展的受众模板 {#generic-and-extensible}

为了支持上面列出的用例，Adobe为您提供了一个通用模板，可以自定义该模板以根据API规范进行调整。

您可以使用通用模板执行以下操作 [创建新的受众模板](../metadata-api/create-audience-template.md) 如果您的API支持：

* HTTP方法：POST、GET、PUT、DELETE、PATCH
* 身份验证类型：OAuth 1、具有刷新令牌的OAuth 2、具有持有者令牌的OAuth 2
* 其功能包括：创建受众、更新受众、获取受众、删除受众、验证凭据

如果您的用例需要，Adobe工程团队可以与您一起使用自定义字段展开通用模板。

## 配置示例 {#configuration-examples}

本节包含三个通用受众元数据配置示例，以供您参考，以及对配置的主要部分的描述。 请注意三个示例配置中的url、标头、请求和响应正文之间的差异。 这是因为三个示例平台的营销API的规范不同。

请注意，在一些示例中，宏字段 `{{authData.accessToken}}` 或 `{{segment.name}}` 在URL中使用，而在其他示例中，在标头或请求正文中使用它们。 这确实取决于您的营销API规范。

| 模板部分 | 描述 |
|--- |--- |
| `create` | 包含对API进行HTTP调用、在平台中以编程方式创建区段/受众并将信息同步回Adobe Experience Platform所需的所有组件（URL、HTTP方法、标头、请求和响应正文）。 |
| `update` | 包含对API进行HTTP调用、以编程方式更新平台中的区段/受众并将信息同步回Adobe Experience Platform所需的所有组件（URL、HTTP方法、标头、请求和响应正文）。 |
| `delete` | 包含对API进行HTTP调用的所有必需组件（URL、HTTP方法、标头、请求和响应正文），以编程方式删除平台中的区段/受众。 |
| `validate` | 在调用合作伙伴API之前，运行模板配置中任何字段的验证。 例如，您可以验证是否正确输入了用户的帐户ID。 |
| `notify` | 仅适用于基于文件的目标。 包括所有必需的组件（URL、HTTP方法、标头、请求和响应正文），以便对API进行HTTP调用，通知您文件导出成功。 |

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

在中查找模板中所有参数的描述 [创建受众模板](../metadata-api/create-audience-template.md) API引用。

## 受众元数据模板中使用的宏

为了在Experience Platform与API之间传递受众ID、访问令牌、错误消息等信息，受众模板包含您可以使用的宏。 请阅读下面本页三个配置示例中使用的宏的说明：

| 宏 | 描述 |
|--- |--- |
| `{{segment.alias}}` | 允许您访问Experience Platform中的受众别名。 |
| `{{segment.name}}` | 允许您访问Experience Platform中的受众名称。 |
| `{{segment.id}}` | 允许您访问Experience Platform中的受众ID。 |
| `{{customerData.accountId}}` | 用于访问在目标配置中设置的帐户ID字段。 |
| `{{oauth2ServiceAccessToken}}` | 允许您根据OAuth 2配置动态生成访问令牌。 |
| `{{authData.accessToken}}` | 允许您将访问令牌传递到API端点。 使用 `{{authData.accessToken}}` 如果Experience Platform应使用未过期的令牌连接到您的目标，否则使用 `{{oauth2ServiceAccessToken}}` 以生成访问令牌。 |
| `{{body.segments[0].segment.id}}` | 返回所创建受众的唯一标识符，作为键的值 `externalAudienceId`. |
| `{{error.message}}` | 返回将在Experience PlatformUI中向用户显示的错误消息。 |

{style="table-layout:auto"}
