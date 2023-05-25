---
description: 了解如何在发布流目标配置之前，使用目标测试API对其进行测试。
title: 流媒体目标测试API概述
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# 流媒体目标测试API概述

作为Destination SDK的一部分，Adobe提供开发人员工具来帮助您配置和测试目标。 本页介绍如何测试目标配置。 有关如何创建消息转换模板的信息，请阅读 [创建和测试消息转换模板](../../testing-api/streaming-destinations/create-template.md).

至 **测试目标是否正确配置，并验证流向已配置目标的数据流的完整性**，使用 *目标测试工具*. 使用此工具，您可以通过向REST API端点发送消息来测试目标配置。

下图说明了测试您的目标如何适应 [目标配置工作流](../../guides/configure-destination-instructions.md) Destination SDK：

![说明目标测试步骤在目标配置工作流程中的位置](../../assets/testing-api/test-destination-step.png)

## 目标测试工具 — 用途和先决条件 {#destination-testing-tool}

使用目标测试工具，通过向中提供的合作伙伴端点发送消息来测试目标配置。 [服务器配置](../../authoring-api/destination-server/create-destination-server.md).

在使用工具之前，请确保：
* 按照中概述的步骤配置目标 [目标配置工作流](../../authoring-api/destination-configuration/create-destination-configuration.md) 和
* 建立与目标的连接，如中所述 [如何获取目标实例ID](../../testing-api/streaming-destinations/destination-testing-api.md#get-destination-instance-id).

使用此工具，在配置目标后，您可以：
* 测试目标配置是否正确；
* 验证流向您配置的目标的数据流的完整性。

### 使用方法 {#how-to-use}

>[!NOTE]
>
>有关完整的API参考文档，请阅读 [目标测试API操作](../../testing-api/streaming-destinations/destination-testing-api.md).

您可以调用目标测试API端点，可以在请求中添加或不添加配置文件。

如果您未在请求中添加任何配置文件，Adobe将在内部为您生成这些配置文件，并将它们添加到请求中。 如果要生成要在此请求中使用的配置文件，请参阅 [示例配置文件生成API参考](../../testing-api/streaming-destinations/sample-profile-generation-api.md). 您需要根据源XDM架构生成配置文件，如 [API参考](../../testing-api/streaming-destinations/sample-profile-generation-api.md#generate-sample-profiles-source-schema). 请注意，源架构是 [合并模式](../../../../profile/ui/union-schema.md) 沙盒的标头。

响应包含目标请求处理的结果。 该请求包括三个主要部分：
* Adobe为目标生成的请求。
* 从目标收到的响应。
* 请求中发送的用户档案列表，无论这些用户档案是 [由您在请求中添加](../../testing-api/streaming-destinations/destination-testing-api.md#test-with-added-profiles)，或由Adobe生成，如果 [目标测试请求的正文为空](../../testing-api/streaming-destinations/destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>Adobe可以生成多个请求和响应对。 例如，如果向具有 `maxUsersPerRequest` 值为7，则将有一个包含7个配置文件的请求和另一个包含3个配置文件的请求。

**正文中包含配置文件参数的示例请求**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
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
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**正文中不含配置文件参数的示例请求**


```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw ''
```

**示例响应**

请注意， `results.httpCalls` 参数特定于您的REST API。

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
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
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

有关请求和响应参数的说明，请参阅 [目标测试API操作](../../testing-api/streaming-destinations/destination-testing-api.md).

## 后续步骤

测试目标并确认正确配置后，请使用 [目标发布API](../../publishing-api/create-publishing-request.md) 以将您的配置提交到Adobe以供审查。
