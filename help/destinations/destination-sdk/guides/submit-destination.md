---
description: 本页提供了在使用Destination SDK创作产品化目标时提交该目标以供审阅所需的所有信息。
title: 提交已生产的目的地以供审查
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---

# 提交已生产的目的地以供审查

## 概述 {#overview}

>[!IMPORTANT]
>
>* 此处记录的流程仅适用于提交生产（公共）目标的合作伙伴。 如果您正在创建一个供您自己使用的专用目标，则无需制作这些材料并将其与Adobe共享。
>
>* Adobe审查目标发布请求的标准响应时间为5个工作日。
>
>* 如果Adobe团队要求您在首次提交后对配置进行任何更新，则您必须在进行更新后提交另一个目标发布请求。
>
>* 即使目标在Experience Platform目录中处于活动状态，但是如果需要对配置进行任何更新，则必须提交新的目标发布请求，才能将更新反映在配置中。
>
>* 对于要更新的新目标和现有目标，审核时间线和所需对象是相同的。

在将目标发布到[Experience Platform目标目录](/help/destinations/catalog/overview.md)之前，您必须向Adobe提供有关目标以及您执行的测试的特定信息，以确保用户在将数据激活到您的平台时享有最佳体验。

本页列出了在提交或更新使用Adobe Experience Platform Destination SDK创作的目标时需要提供的所有信息。 要在Adobe Experience Platform中成功提交目标，请向<aepdestsdk@adobe.com>发送一封电子邮件，其中包括：

* 目标解决的使用案例描述。 只有在提交新的目标配置时才需要此操作。
* 目标提交原因的描述。 只有在更新现有目标配置时才需要此项。
* 使用测试目标API端点对目标执行HTTP调用后的测试结果。 请与Adobe共享对您的目标端点进行的API调用以及从目标端点接收的API响应。
* 一个屏幕录制，用于显示连接到您的目标并完成激活步骤的用户体验。
* 基于文件的目标的其他要求：
   * 使用测试API共享请求和响应示例以[使用示例配置文件测试基于文件的目标](../testing-api/batch-destinations/file-based-destination-testing-api.md)。
   * 附加由目标生成并导出到存储位置的样例文件。
   * 提交某种形式的证明，证明您已成功将导出的文件从存储位置摄取到系统中。
* 证明您已使用[目标发布API](../publishing-api/create-publishing-request.md)提交目标的目标发布请求。
* 文档PR（拉取请求），按照[自助文档流程](../docs-framework/documentation-instructions.md)中所述的说明操作。
* 在Experience Platform目标目录中显示为您的目标卡徽标的图像文件。

您可以在以下部分中找到有关每个项目的详细信息：

## 用例描述 {#use-case-description}

描述您的目标为Experience Platform客户解决的用例。 您的描述可能与现有合作伙伴的用例类似：

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md)：根据您的客户列表、访问过您网站的人或已在Pinterest上与您的内容交互的人创建受众。
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases)： DataX API可用于广告商，这些广告商希望定位以Verizon Media (VMG)中电子邮件地址作为关键字的特定受众组，它们可以使用VMG近乎实时的API快速创建新受众并推送所需的受众组。

## 更新原因 {#reason-for-update}

>[!NOTE]
>
>仅当更新现有配置时，才需要此部分。

简要介绍您的提交解决现有目标的问题。 例如，在您从测试版过渡到正式发布时，您提交的内容可能会更新目标的名称、描述和徽标。 或者，您的提交可能会修复在目标配置中发现的一个错误。

## 使用测试目标API后的测试结果 {#testing-api-response}

在使用[测试目标API](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)端点执行到目标的HTTP调用后提供测试结果。 这包括：

* 使用测试API向目标端点发出完整API请求（标头和正文）。
* 从目标端点接收的API响应。

例如，您的请求和响应可能类似于以下示例：

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

对于基于文件的目标，您必须提供其他证据，证明您已正确设置目标。 确保包括以下项目：

### 测试API响应 {#testing-api-response-file-based}

使用测试API后包括请求和响应示例，以使用示例配置文件[测试基于文件的目标](../testing-api/batch-destinations/file-based-destination-testing-api.md)。

### 附加导出的文件 {#attach-exported-file}

在您的[提交电子邮件](#download-sample-email)中，附上由您设置的目标导出到存储位置的CSV文件。

### 摄取成功的证明 {#proof-of-successful-ingestion}

最后，您必须提供某种形式的证明，以证明将数据导出到您提供的存储位置后，数据已成功引入到系统中。 请提供以下任意项目：

* 屏幕截图或简短的屏幕截图视频，您可以在其中手动从存储位置获取文件并将其摄取到系统中。
* 屏幕截图或简短的屏幕截图视频，其中系统的UI用于确认Experience Platform生成的文件名已成功摄取到系统中。
* 记录系统中有Adobe可与文件名或从Experience Platform生成的数据关联的行。

## 证明您已提交目标发布请求 {#destination-publishing-request-proof}

成功测试目标后，必须使用[目标发布API](../publishing-api/create-publishing-request.md)将目标提交到Adobe进行审查和发布。

提供目标发布请求的ID。 有关如何检索发布请求ID的信息，请阅读如何[检索目标发布请求](../publishing-api/retrieve-publishing-request.md)。

## 产品集成的目标文档PR（拉取请求） {#documentation-pr}

如果您是创建[产品化集成](../overview.md#productized-custom-integrations)的独立软件供应商(ISV)或系统集成商(SI)，则必须使用[自助服务文档流程](../docs-framework/documentation-instructions.md)为您的目标创建产品文档页面。 在提交过程中，提供目标文档的拉取请求(PR)。

## 目标徽标 {#logo}

目标目录包含每个目标卡的徽标。 在提交电子邮件中，加入带有目标徽标的图像。

图像要求包括：
* **格式**： `SVG`
* **大小**：小于2MB

## 下载示例电子邮件 {#download-sample-email}

[下载](../assets/guides/sample-email-submit-destination.rtf)示例电子邮件，其中包含您需要提供给Adobe的所有信息。
