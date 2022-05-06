---
description: 作为Destination SDK的一部分，Adobe提供了开发人员工具，可帮助您配置和测试目标。 本页介绍如何测试目标配置。
title: 测试目标配置
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# 测试目标配置 {#developer-tools}

## 概述 {#overview}

作为Destination SDK的一部分，Adobe提供了开发人员工具，可帮助您配置和测试目标。 本页介绍如何测试目标配置。 有关如何创建消息转换模板的信息，请阅读 [创建和测试消息转换模板](./create-template.md).

至 **测试您的目标是否配置正确，并验证数据流向您配置的目标的完整性**，则使用 *目标测试工具*. 使用此工具，您可以通过向REST API端点发送消息来测试目标配置。

下图显示了如何在 [目标配置工作流](./configure-destination-instructions.md) 在Destination SDK中：

![目标测试步骤在目标配置工作流中所处位置的图形](./assets/test-destination-step.png)

## 目标测试工具 — 用途和先决条件 {#destination-testing-tool}

使用目标测试工具，通过向您在 [服务器配置](./server-and-template-configuration.md).

在使用该工具之前，请确保：
* 按照 [目标配置工作流](./configure-destination-instructions.md) 和
* 建立与目标的连接，详见 [如何获取目标实例ID](./destination-testing-api.md#get-destination-instance-id).

使用此工具，在配置了目标后，您可以：
* 测试目标配置是否正确；
* 验证数据流到您配置的目标的完整性。

### 使用方法 {#how-to-use}

>[!NOTE]
>
>有关完整的API参考文档，请阅读 [目标测试API操作](./destination-testing-api.md).

无论是否在请求中添加配置文件，您都可以对目标测试API端点进行调用。

如果您未在请求中添加任何用户档案，则Adobe将在内部为您生成这些用户档案，并将其添加到请求中。 如果要生成要在此请求中使用的用户档案，请参阅 [配置文件生成API参考示例](./sample-profile-generation-api.md). 您需要根据源XDM架构生成用户档案，如 [API参考](./sample-profile-generation-api.md#generate-sample-profiles-source-schema). 请注意，源架构为 [合并模式](https://experienceleague.adobe.com/docs/experience-platform/profile/union-schemas/union-schema.html?lang=en) 的沙盒。

响应包含目标请求处理的结果。 请求包括三个主要部分：
* 由Adobe为目标生成的请求。
* 从您的目的地收到的响应。
* 请求中发送的用户档案列表，无论这些用户档案是否 [由您在请求中添加](./destination-testing-api.md/#test-with-added-profiles)，或由Adobe生成(如果 [目标测试请求的正文为空](./destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>Adobe可以生成多个请求和响应对。 例如，如果向具有 `maxUsersPerRequest` 值为7时，将有一个包含7个用户档案的请求，另一个包含3个用户档案的请求。

**正文中包含profiles参数的示例请求**

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

**正文中不带用户档案参数的示例请求**


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

有关请求和响应参数的描述，请参阅 [目标测试API操作](./destination-testing-api.md).

## 后续步骤

测试目标并确认其配置正确后，请使用 [目标发布API](./destination-publish-api.md) 将配置提交到Adobe以供审核。
