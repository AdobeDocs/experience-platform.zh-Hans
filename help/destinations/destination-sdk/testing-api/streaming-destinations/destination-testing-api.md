---
description: 了解如何使用目标测试API来测试您的流目标配置是否正确，以及验证流向您配置的目标的数据流的完整性。
title: 使用示例配置文件测试您的流目标
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---


# 使用示例配置文件测试您的流目标 {#template-api-operations}

>[!IMPORTANT]
>
>**API终结点**： `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

此页面列出并描述了可以使用`/authoring/testing/destinationInstance/` API端点执行的所有API操作，以测试目标配置是否正确，以及验证数据流到已配置目标的完整性。 有关此端点支持的功能的说明，请阅读[测试您的目标配置](streaming-destination-testing-overview.md)。

您可以向测试端点发出请求，无论是否向调用添加配置文件。 如果您未在请求中发送任何配置文件，Adobe将在内部为您生成这些配置文件，并将它们添加到请求中。

您可以使用[示例配置文件生成API](sample-profile-generation-api.md)创建配置文件以用于向目标测试API发出的请求。

## 如何获取目标实例ID {#get-destination-instance-id}

>[!IMPORTANT]
>
>* 要使用此API，您必须在Experience Platform UI中拥有到目标的现有连接。 阅读[连接到目标](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=zh-Hans)和[将配置文件和受众激活到目标](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=zh-Hans)以了解详细信息。
>* 建立与目标的连接后，获取在[浏览与目标](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=zh-Hans)的连接时您应在对此端点的API调用中使用的目标实例ID。
>  &#x200B;>![UI图像如何获取目标实例ID](../../assets/testing-api/get-destination-instance-id.png)

## 目标测试API操作快速入门 {#get-started}

在继续之前，请查看[入门指南](../../getting-started.md)以了解成功调用API所需了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 测试目标配置，而不将配置文件添加到调用 {#test-without-adding-profiles}

您可以通过向`authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}`端点发出POST请求并提供要测试的目标的目标实例ID来测试目标配置。

**API格式**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| 查询参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您正在测试的目标的目标实例ID。 |

**请求**

以下请求调用目标的REST API端点。 请求由`{DESTINATION_INSTANCE_ID}`查询参数配置。

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应会返回HTTP状态200以及来自目标的REST API端点的API响应。

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-vlnt6"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `aggregationKey` | 包含有关为目标配置的聚合策略的信息。 有关详细信息，请阅读[聚合策略](../../functionality/destination-configuration/aggregation-policy.md)文档。 |
| `traceId` | 操作的唯一标识符。 遇到错误时，您可以与Adobe团队共享此ID，以进行故障排除。 |
| `results.httpCalls.request` | 包含Adobe发送到目标的请求。 |
| `results.httpCalls.response` | 包含Adobe从目标收到的响应。 |
| `inputProfiles` | 包含在调用目标时导出的用户档案。 配置文件与您的源架构匹配。 |

{style="table-layout:auto"}

## 使用添加到调用的用户档案测试目标配置 {#test-with-added-profiles}

您可以通过向`authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}`端点发出POST请求并提供要测试的目标的目标实例ID来测试目标配置。

**API格式**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| 查询参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您正在测试的目标的目标实例ID。 |

**请求**

以下请求调用目标的REST API端点。 请求由有效负载中提供的参数和`{DESTINATION_INSTANCE_ID}`查询参数配置。

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}'
```

**响应**

成功的响应会返回HTTP状态200以及来自目标的REST API端点的API响应。

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}
```

## API错误处理 {#api-error-handling}

Destination SDK API端点遵循常规Experience Platform API错误消息原则。 请参阅平台疑难解答指南中的[API状态代码](../../../../landing/troubleshooting.md#api-status-codes)和[请求标头错误](../../../../landing/troubleshooting.md#request-header-errors)。

## 后续步骤

阅读本文档后，您现在知道如何测试您的目标。 您现在可以使用Adobe [自助式文档流程](../../docs-framework/documentation-instructions.md)为您的目标创建文档页面。
