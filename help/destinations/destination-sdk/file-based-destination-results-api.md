---
description: 本页介绍如何使用/testing/destinationInstance API端点查看测试结果的完整详细信息。 此API端点会返回与使用流服务API监视数据流时获得的结果相同的结果。
title: 查看详细的激活结果
source-git-commit: 5b62203113dd55dad8adeb96cbcc2d46b3420c3a
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---


# 查看详细的激活结果 {#view-test-results}

## 概述 {#overview}

本页介绍如何使用 `/testing/destinationInstance` 用于查看基于文件的目标测试结果的完整详细信息的API端点。

如果您已经 [已测试目标](file-based-destination-testing-api.md) 并且收到了有效的API响应，则表明您的目标运行正常。

如果要查看有关激活流程的更多详细信息，可以使用 `results` 属性 [目标测试](file-based-destination-testing-api.md) 端点响应，如下所述。

>[!NOTE]
>
>此API端点会返回与使用 [流量服务API](../api/update-destination-dataflows.md) 监视数据流。

## 快速入门 {#getting-started}

在继续之前，请查看 [入门指南](./getting-started.md) 有关成功调用API所需的重要信息，包括如何获取所需的目标创作权限和所需标头。

## 先决条件 {#prerequisites}

在使用 `/testing/destinationInstance` 端点，确保满足以下条件：

* 您已通过Destination SDK创建了一个基于文件的现有目标，您可以在 [目标目录](../ui/destinations-workspace.md).
* 您已在Experience PlatformUI中为目标至少创建了一个激活流程。
* 要成功发出API请求，您需要与要测试的目标实例对应的目标实例ID。 在Platform UI中浏览与目标的连接时，从URL获取应在API调用中使用的目标实例ID。

   ![显示如何从URL获取目标实例ID的UI图像。](assets/get-destination-instance-id.png)
* 您之前 [已测试目标配置](file-based-destination-testing-api.md)，并收到了有效的API响应，该响应包括 `results` 属性。 您将使用此 `results` 值以进一步测试目标。

## 查看详细的目标测试结果 {#test-activation-results}

一旦 [已验证目标配置](file-based-destination-testing-api.md)，则可以通过向发出GET请求来查看详细的激活结果 `authoring/testing/destinationInstance/` 端点和提供您正在测试的目标的目标实例ID，以及已激活区段的流运行ID。

您可以在 `results` 中返回的属性 [目标测试调用的响应](file-based-destination-testing-api.md).

**API格式**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| 路径参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 要为其生成示例用户档案的目标实例的ID。 请参阅 [先决条件](#prerequisites) 部分以了解有关如何获取此ID的详细信息。 |

| 查询字符串参数 | 描述 |
| -------- | ----------- |
| `flowRunIds` | 与激活的区段对应的流量运行ID。 您可以在 `results` 中返回的属性 [目标测试调用的响应](file-based-destination-testing-api.md). |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=30d34875-e7ba-4520-ab6e-5705e01dfb16,86c00ad7-443c-459a-855d-0e8cbee43c4f,12305c58-42a9-4230-8fad-1661ee49cb70' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应包含激活流程的完整详细信息。 您可以通过调用 [流量服务API](../api/update-destination-dataflows.md) 监视数据流。

```json
{
   "items":[
      {
         "id":"18efd5d2-40ae-4f5c-afd1-37a39a45183a",
         "flowId":"a02071ad-f3a4-496c-a2b1-468812301d5d",
         "flowSpec":{
            "id":"25473b67-0801-418a-ab49-ed74ebf88137",
            "version":"1.0"
         },
         "metrics":{
            "durationSummary":{
               "startedAtUTC":1646652235124,
               "completedAtUTC":1646652270439
            },
            "latencySummary":null,
            "sizeSummary":{
               "inputBytes":122,
               "outputBytes":122
            },
            "recordSummary":{
               "inputRecordCount":1,
               "outputRecordCount":1,
               "createdRecordCount":1,
               "skippedRecordCount":0,
               "sourceSummaries":[
                  {
                     "id":"76e4b969-9700-4557-8330-0a8390afbdde",
                     "entitySummaries":[
                        {
                           "inputRecordCount":1,
                           "skippedRecordCount":0,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ],
               "targetSummaries":[
                  {
                     "id":"b43607b6-0dca-43b3-a0bc-ecdea4fa6aa9",
                     "entitySummaries":[
                        {
                           "outputRecordCount":1,
                           "createdRecordCount":1,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ]
            },
            "fileSummary":{
               "inputFileCount":1,
               "outputFileCount":1
            },
            "statusSummary":{
               "status":"success"
            }
         },
         "activities":[
            {
               "id":"c4f238e3-7334-4933-8b56-64d7ea43ea54",
               "name":"Activation Batch XdmProcessor Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652235124,
                  "completedAtUTC":1646652255157
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "inputBytes":122,
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "inputFileCount":1,
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     "incremental.batchId":"",
                     "snapshot.batchId":"",
                     "snapshot.datasetId":"",
                     "incremental.datasetId":""
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            },
            {
               "id":"51d82b36-6b8f-11eb-9439-0242ac130002",
               "name":"Activation Batch Publisher Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652270326,
                  "completedAtUTC":1646652270439
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            }
         ],
         "predecessors":null
      }
   ],
   "_links":{
      
   }
}
```

## API错误处理 {#api-error-handling}

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中。

## 后续步骤

阅读本文档后，您现在知道如何测试基于文件的目标配置并查看激活结果的完整详细信息。

如果您正在构建公共目标，您现在可以 [提交目标配置](../destination-sdk/submit-destination.md) Adobe以供审阅。
