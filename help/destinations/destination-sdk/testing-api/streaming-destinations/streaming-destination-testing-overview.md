---
description: 了解如何在发布流目标配置之前，使用目标测试API对其进行测试。
title: 流式目标测试API概述
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# 流式目标测试API概述

作为Destination SDK的一部分，Adobe提供开发人员工具来帮助您配置和测试目标。 本页介绍如何测试目标配置。 有关如何创建消息转换模板的信息，请阅读[创建和测试消息转换模板](../../testing-api/streaming-destinations/create-template.md)。

要&#x200B;**测试目标是否正确配置以及验证流向所配置目标**&#x200B;的数据流的完整性，请使用&#x200B;*目标测试工具*。 使用此工具，您可以通过向REST API端点发送消息来测试目标配置。

下图说明了测试目标如何适应Destination SDK中的[目标配置工作流](../../guides/configure-destination-instructions.md)：

![目标测试步骤适合目标配置工作流的图形](../../assets/testing-api/test-destination-step.png)

## 目标测试工具 — 用途和先决条件 {#destination-testing-tool}

使用目标测试工具，通过向[服务器配置](../../authoring-api/destination-server/create-destination-server.md)中提供的合作伙伴端点发送消息来测试目标配置。

在使用工具之前，请确保：

* 按照[目标配置工作流](../../authoring-api/destination-configuration/create-destination-configuration.md)中所述的步骤配置目标，并且
* 建立与目标的连接，如[如何获取目标实例ID](../../testing-api/streaming-destinations/destination-testing-api.md#get-destination-instance-id)中所述。

使用此工具，在配置目标后，您可以：

* 测试目标配置是否正确；
* 验证流向您配置的目标的数据流的完整性。

### 使用方法 {#how-to-use}

>[!NOTE]
>
>有关完整的API参考文档，请阅读[目标测试API操作](../../testing-api/streaming-destinations/destination-testing-api.md)。

您可以调用目标测试API端点，可以在请求中添加或不添加配置文件。

如果您未在请求中添加任何配置文件，Adobe将在内部为您生成这些配置文件，并将它们添加到请求中。 如果要生成配置文件以在此请求中使用，请参阅[示例配置文件生成API参考](../../testing-api/streaming-destinations/sample-profile-generation-api.md)。 您需要基于源XDM架构生成配置文件，如[API引用](../../testing-api/streaming-destinations/sample-profile-generation-api.md#generate-sample-profiles-source-schema)中所示。 请注意，源架构是您正在使用的沙盒的[合并架构](../../../../profile/ui/union-schema.md)。

响应包含目标请求处理的结果。 该请求包括三个主要部分：

* Adobe为目标生成的请求。
* 从目标收到的响应。
* 在请求中发送的用户档案列表，无论这些用户档案是您在[请求中添加的](../../testing-api/streaming-destinations/destination-testing-api.md#test-with-added-profiles)，还是Adobe生成的（如果[目标测试请求正文为空](../../testing-api/streaming-destinations/destination-testing-api.md#test-without-adding-profiles)）。

>[!NOTE]
>
>Adobe可以生成多个请求和响应对。 例如，如果您将10个配置文件发送到一个具有`maxUsersPerRequest`值7的目标，则将有一个包含7个配置文件的请求，另一个包含3个配置文件的请求。

**正文中具有配置文件参数的示例请求**

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

**正文中没有配置文件参数的示例请求**


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

请注意，`results.httpCalls`参数的内容特定于您的REST API。

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

有关请求和响应参数的说明，请参阅[目标测试API操作](../../testing-api/streaming-destinations/destination-testing-api.md)。

## 后续步骤

测试目标并确认配置正确后，使用[目标发布API](../../publishing-api/create-publishing-request.md)将配置提交到Adobe以供审查。
