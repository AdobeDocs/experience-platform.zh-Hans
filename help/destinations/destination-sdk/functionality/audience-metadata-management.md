---
description: 使用受众元数据模板以编程方式创建、更新或删除目标中的受众。 Adobe提供了一个可扩展的受众元数据模板，您可以根据营销API的规范配置该模板。 定义、测试和提交模板后，Adobe将使用该模板来构造对目标的调用。
title: 受众元数据管理
exl-id: 795e8adb-c595-4ac5-8d1a-7940608d01cd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 2%

---

# 受众元数据管理

使用受众元数据模板以编程方式创建、更新或删除目标中的受众。 Adobe提供了一个可扩展的受众元数据模板，您可以根据营销API的规范配置该模板。 定义、测试和提交配置后，Adobe将使用该配置来构造指向目标的API调用。

您可以使用`/authoring/audience-templates` API端点配置本文档中描述的功能。 读取[创建元数据模板](../metadata-api/create-audience-template.md)，以获取可在终结点上执行的操作的完整列表。

## 何时使用受众元数据管理端点 {#when-to-use}

根据您的API配置，在Experience Platform中配置目标时，您可能需要也可能不需要使用受众元数据管理端点。 使用下面的决策树图了解何时使用受众元数据端点以及如何为目标配置受众元数据模板。

![决策树图表](../assets/functionality/audience-metadata-decision-tree.png)

## 受众元数据管理支持的用例 {#use-cases}

借助Destination SDK中的受众元数据支持，在配置Experience Platform目标时，您可以为Experience Platform用户提供以下多个选项之一，以便他们映射并激活受众到您的目标。 您可以通过目标配置[受众元数据配置](../functionality/destination-configuration/audience-metadata-configuration.md)部分中的参数控制用户可用的选项。

### 用例1 — 您有一个第三方API，用户不需要输入映射ID

如果您有用于创建/更新/删除受众或受众的API端点，则可以使用受众元数据模板来配置Destination SDK，以匹配受众创建/更新/删除端点的规范。 Experience Platform能够以编程方式创建/更新/删除受众，并将元数据同步回Experience Platform。

在Experience Platform用户界面(UI)中将受众激活到目标时，用户无需在激活工作流中手动填写受众映射ID字段。

### 用例2 — 用户需要首先在您的目标中创建受众，并需要手动输入映射ID

如果受众和其他元数据需要由合作伙伴或用户在您的目标中手动创建，则用户必须手动填写激活工作流中的受众映射ID字段，以在您的目标和Experience Platform之间同步受众元数据。

![输入映射ID](../assets/functionality/input-mapping-id.png)

### 用例3 — 您的目标接受Experience Platform受众ID，用户无需手动输入映射ID

如果目标系统接受Experience Platform受众ID，则可以在受众元数据模板中对其进行配置。 用户在激活区段时无需填充受众映射ID。

## 通用且可扩展的受众模板 {#generic-and-extensible}

为了支持上面列出的用例，Adobe为您提供了一个通用模板，您可以根据自己的API规范来自定义该模板。

如果您的API支持：[&#128279;](../metadata-api/create-audience-template.md)

* HTTP方法：POST、GET、PUT、DELETE、PATCH
* 身份验证类型：OAuth 1、具有刷新令牌的OAuth 2、具有持有者令牌的OAuth 2
* 其功能包括：创建受众、更新受众、获取受众、删除受众、验证凭据

如果您的用例需要，Adobe工程团队可以与您一起使用自定义字段展开通用模板。


## 支持的模板事件 {#supported-events}

下表描述了受众元数据模板支持的事件。

| 模板部分 | 描述 |
|--- |--- |
| `create` | 包括所有必需的组件（URL、HTTP方法、标头、请求和响应正文），以便对API进行HTTP调用，在平台中以编程方式创建区段/受众，并将信息同步回Adobe Experience Platform。 |
| `update` | 包括所有必需的组件（URL、HTTP方法、标头、请求和响应正文），以便对API进行HTTP调用，以编程方式更新平台中的区段/受众，并将信息同步回Adobe Experience Platform。 |
| `delete` | 包括所有必需的组件（URL、HTTP方法、标头、请求和响应正文），以便对API进行HTTP调用，以编程方式删除平台中的区段/受众。 |
| `validate` | 在对合作伙伴API进行调用之前，对模板配置中的任何字段运行验证。 例如，您可以验证是否正确输入了用户的帐户ID。 |
| `notify` | 仅适用于基于文件的目标。 包括所有必需组件（URL、HTTP方法、标头、请求和响应正文），以便对您的API进行HTTP调用，通知您文件导出成功。 |
| `createDestination` | 包括所有必需的组件（URL、HTTP方法、标头、请求和响应正文），以便对API进行HTTP调用，在平台中以编程方式创建数据流并将信息同步回Adobe Experience Platform。 |
| `updateDestination` | 包含对API进行HTTP调用、以编程方式更新平台中的数据流并将信息同步回Adobe Experience Platform所需的所有组件（URL、HTTP方法、标头、请求和响应正文）。 |
| `deleteDestination` | 包括所有必需的组件（URL、HTTP方法、标头、请求和响应正文），以便对API进行HTTP调用，以编程方式从平台中删除数据流。 |

{style="table-layout:auto"}

## 配置示例 {#configuration-examples}

本节包含常规受众元数据配置的示例，以供您参考。

请注意三个示例配置之间的URL、标头和请求正文有何不同。 这是因为三个示例平台的营销API的规范不同。

请注意，在一些示例中，URL中使用了`{{authData.accessToken}}`或`{{segment.name}}`等宏字段，而在其他示例中，标头或请求正文中使用这些宏字段。 其使用取决于您的营销API规范。

+++流示例1

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

+++

+++流示例2

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

+++

+++流示例3

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

+++

+++基于文件的示例

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

+++

在[创建受众模板](../metadata-api/create-audience-template.md) API引用中查找模板中所有参数的描述。

## 受众元数据模板中使用的宏 {#macros}

为了在Experience Platform与API之间传递受众ID、访问令牌、错误消息等信息，受众模板包含您可以使用的宏。 请阅读下面本页三个配置示例中使用的宏的说明：

| 宏 | 描述 |
|--- |--- |
| `{{segment.alias}}` | 允许您访问Experience Platform中的受众别名。 |
| `{{segment.name}}` | 允许您访问Experience Platform中的受众名称。 |
| `{{segment.id}}` | 允许您访问Experience Platform中的受众ID。 |
| `{{customerData.accountId}}` | 允许您访问在目标配置中设置的帐户ID字段。 |
| `{{oauth2ServiceAccessToken}}` | 允许您根据OAuth 2配置动态生成访问令牌。 |
| `{{authData.accessToken}}` | 允许您将访问令牌传递到API端点。 如果Experience Platform应使用未过期的令牌连接到您的目标，请使用`{{authData.accessToken}}`，否则请使用`{{oauth2ServiceAccessToken}}`生成访问令牌。 |
| `{{body.segments[0].segment.id}}` | 返回已创建受众的唯一标识符作为键`externalAudienceId`的值。 |
| `{{error.message}}` | 返回将在Experience Platform UI中向用户显示的错误消息。 |
| `{{{segmentEnrichmentAttributes}}}` | 允许您访问特定受众的所有扩充属性。  `create`、`update`和`delete`事件支持此宏。 丰富属性仅适用于[自定义上传受众](destination-configuration/schema-configuration.md#external-audiences)。请参阅[批受众激活指南](../../ui/activate-batch-profile-destinations.md#select-enrichment-attributes)，了解扩充属性选择的工作方式。 |
| `{{destination.name}}` | 返回目标的名称。 |
| `{{destination.sandboxName}}` | 返回配置目标的Experience Platform沙盒的名称。 |
| `{{destination.id}}` | 返回目标配置的ID。 |
| `{{destination.imsOrgId}}` | 返回配置目标的IMS组织ID。 |
| `{{destination.enrichmentAttributes}}` | 允许您访问映射到目标的所有受众的所有扩充属性。 `createDestination`、`updateDestination`和`deleteDestination`事件支持此宏。 丰富属性仅适用于[自定义上传受众](destination-configuration/schema-configuration.md#external-audiences)。请参阅[批受众激活指南](../../ui/activate-batch-profile-destinations.md#select-enrichment-attributes)，了解扩充属性选择的工作方式。 |
| `{{destination.enrichmentAttributes.<namespace>.<segmentId>}}` | 允许您访问映射到目标的特定外部受众的扩充属性。 丰富属性仅适用于[自定义上传受众](destination-configuration/schema-configuration.md#external-audiences)。请参阅[批受众激活指南](../../ui/activate-batch-profile-destinations.md#select-enrichment-attributes)，了解扩充属性选择的工作方式。 |

{style="table-layout:auto"}
