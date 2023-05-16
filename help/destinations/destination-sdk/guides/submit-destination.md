---
description: 本页提供您需要提交的所有信息，以便审核使用Destination SDK创作的已产品化目标。
title: 提交以供审核在Destination SDK中创作的按产品化目标
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: 8c8026b1180775dddd9517fc88727749678a5613
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# 提交以供审核在Destination SDK中创作的按产品化目标

## 概述 {#overview}

>[!IMPORTANT]
>
>* 只有提交产品化（公共）目标的合作伙伴才需要此处记录的流程。 如果您创建一个供自己使用的专用目标，则无需制作这些材料并与Adobe共享。
>
>* Adobe查看目标发布请求的标准响应时间为五个工作日。
>
>* 如果Adobe团队在初次提交后要求您对配置进行任何更新，则在进行更新后，您必须提交另一个目标发布请求。
>
>* 即使在Experience Platform目录中实现目标后，如果您需要对配置进行任何更新，则必须提交新的目标发布请求，以便将更新反映在配置中。


在将目标发布到 [Experience Platform目标目录](/help/destinations/catalog/overview.md)，则您必须向Adobe提供有关目标和您执行的测试的特定信息，以确保用户在将数据激活到您的平台时尽可能享有最佳体验。

本页列出了在提交或更新您使用Adobe Experience Platform Destination SDK创作的目标时需要提供的所有信息。 要在Adobe Experience Platform中成功提交目标，请向 <aepdestsdk@adobe.com> 包括：

* 您的目标可解决的用例描述。 仅当您提交新的目标配置时，才需要执行此操作。
* 提交目标的原因描述。 仅当您要更新现有目标配置时，才需要此设置。
* 使用测试目标API端点对您的目标执行HTTP调用后，测试结果。 请与Adobe共享对目标端点发起的API调用以及从目标端点收到的API响应。
* 基于文件的目标的其他要求：
   * 使用测试API后，共享请求和响应示例 [使用示例用户档案测试基于文件的目标](../testing-api/batch-destinations/file-based-destination-testing-api.md).
   * 附加由目标生成并导出到存储位置的样例文件。
   * 提交某种形式的验证，以证明您已成功将导出的文件从存储位置摄取到系统中。
* 验证您是否已使用 [目标发布API](../publishing-api/create-publishing-request.md).
* 文档PR（拉取请求），请按照 [自助文档流程](../docs-framework/documentation-instructions.md).
* 图像文件，将在Experience Platform目标目录中显示为目标卡的徽标。

您可以在以下部分中找到有关每个项目的详细信息：

## 用例描述 {#use-case-description}

描述您的目标为Experience Platform客户解决的用例。 您的描述可以类似于现有合作伙伴的用例：

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md):从客户列表创建受众、访问过您网站的人员或已在Pinterest上与您的内容进行交互的人员。
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases):DataX API适用于那些想要定位特定受众组的广告商，这些受众组在Verizon Media(VMG)中以电子邮件地址作为关键字，这样，他们就可以快速创建新区段，并使用VMG的近实时API推送所需的受众组。

## 更新原因 {#reason-for-update}

>[!NOTE]
>
>仅当您更新现有配置时，才需要此部分。

简要描述您的提交为现有目标解决的问题。 例如，在从测试版过渡到正式发布时，您的提交可能会更新目标的名称、描述和徽标。 或者，您的提交可能会修复在目标配置中发现的错误。

## 使用测试目标API后的测试结果 {#testing-api-response}

使用 [测试目标API](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) 端点来对您的目标执行HTTP调用。 这包括：

* 使用测试API，对目标端点发出的完整API请求（标头和正文）。
* 从目标端点收到的API响应。

例如，您的请求和响应可能与以下示例类似：

**请求**

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

**响应**

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

## 基于文件的目标的其他要求 {#additional-file-based-destination-requirements}

对于基于文件的目标，您必须提供其他验证，以确认您已正确设置目标。 确保包含以下项目：

### 测试API响应 {#testing-api-response-file-based}

使用测试API之后，包含请求和响应示例 [使用示例用户档案测试基于文件的目标](../testing-api/batch-destinations/file-based-destination-testing-api.md).

### 附加导出的文件 {#attach-exported-file}

在 [提交电子邮件](#download-sample-email)，请附加一个CSV文件，该文件已通过您设置的目标导出到您的存储位置。

### 成功摄取的证明 {#proof-of-successful-ingestion}

最后，您必须提供某种形式的证明，证明数据在导出到您提供的存储位置后已成功摄取到您的系统中。 请提供以下任意项目：

* 屏幕截图或简短的屏幕截图视频，您可以在该视频中手动从存储位置获取文件并将其摄取到系统中。
* 屏幕截图或简短的屏幕截图视频，您的系统UI会确认由Experience Platform生成的文件名已成功摄取到您的系统中。
* 您系统中Adobe的日志行可以与文件名或从Experience Platform生成的数据相关联。

## 证明您已提交目标发布请求 {#destination-publishing-request-proof}

成功测试目标后，必须使用 [目标发布API](../publishing-api/create-publishing-request.md) 将目标提交到Adobe以供审核和发布。

为您的目标提供发布请求的ID。 有关如何检索发布请求ID的信息，请阅读如何 [检索目标发布请求](../publishing-api/retrieve-publishing-request.md).

## 面向按产品化集成的目标文档PR（拉取请求） {#documentation-pr}

如果您是独立软件供应商(ISV)或系统集成商(SI)，创建 [产品化集成](../overview.md#productized-custom-integrations)，则必须使用 [自助文档流程](../docs-framework/documentation-instructions.md) 为您的目标创建产品文档页面。 在提交流程中，为目标文档提供拉取请求(PR)。

## 目标的徽标 {#logo}

目标目录包括每个目标卡的徽标。 在您的提交电子邮件中，包含带有目标徽标的图像。

映像要求包括：
* **格式**: `SVG`
* **大小**:小于2 MB

## 下载示例电子邮件 {#download-sample-email}

[下载](../assets/guides/sample-email-submit-destination.rtf) 示例电子邮件，其中包含您需要提供的所有信息以进行Adobe。
