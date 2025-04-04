---
description: 此页说明如何使用/testing/destinationInstance API端点查看测试结果的完整详细信息。 此API端点返回的结果与使用流服务API监视数据流时获得的结果相同。
title: 查看详细的激活结果
exl-id: a7b27beb-825e-47fd-8939-f499c3298f68
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# 查看详细的激活结果 {#view-test-results}

## 概述 {#overview}

本页说明如何使用`/testing/destinationInstance` API端点查看基于文件的目标测试结果的完整详细信息。

如果您已[测试目标](file-based-destination-testing-api.md)并收到有效的API响应，则表明您的目标工作正常。

如果要查看有关激活流程的更多详细信息，可以使用[目标测试](file-based-destination-testing-api.md)端点响应中的`results`属性，如下所述。

>[!NOTE]
>
>此API终结点返回的结果与使用[流服务API](../../../api/update-destination-dataflows.md)监视数据流时获得的结果相同。

## 快速入门 {#getting-started}

在继续之前，请查看[入门指南](../../getting-started.md)以了解成功调用API所需了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 先决条件 {#prerequisites}

在使用`/testing/destinationInstance`端点之前，请确保您满足以下条件：

* 您有一个通过Destination SDK创建的基于文件的现有目标，您可以在[目标目录](../../../ui/destinations-workspace.md)中看到该目标。
* 您已在Experience Platform UI中为目标创建至少一个激活流程。
* 要成功发出API请求，您需要与要测试的目标实例对应的目标实例ID。 在Experience Platform UI中浏览与目标之间的连接时，从URL获取应在API调用中使用的目标实例ID。

  ![UI图像，显示如何从URL获取目标实例ID。](../../assets/testing-api/get-destination-instance-id.png)
* 您以前已[测试过目标配置](file-based-destination-testing-api.md)，并且收到了有效的API响应，其中包含`results`属性。 您将使用此`results`值进一步测试您的目标。

## 查看详细的目标测试结果 {#test-activation-results}

在您[验证目标配置](file-based-destination-testing-api.md)后，您可以查看详细的激活结果，方法是向`authoring/testing/destinationInstance/`端点发出GET请求，并提供您正在测试的目标的目标实例ID以及已激活受众的流运行ID。

在目标测试调用](file-based-destination-testing-api.md)的[响应中返回的`results`属性中，您可以找到需要使用的完整API URL。

**API格式**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| 路径参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 要为其生成样本配置文件的目标实例的ID。 有关如何获取此ID的详细信息，请参阅[先决条件](#prerequisites)部分。 |

| 查询字符串参数 | 描述 |
| -------- | ----------- |
| `flowRunIds` | 流运行与激活的受众相对应的ID。 您可以在目标测试调用](file-based-destination-testing-api.md)的[响应中返回的`results`属性中找到流运行ID。 |

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

响应包含激活流程的完整详细信息。 通过调用[流服务API](../../../api/update-destination-dataflows.md)以监视数据流，可以获得相同的响应。

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

Destination SDK API端点遵循常规Experience Platform API错误消息原则。 请参阅Experience Platform疑难解答指南中的[API状态代码](../../../../landing/troubleshooting.md#api-status-codes)和[请求标头错误](../../../../landing/troubleshooting.md#request-header-errors)。

## 后续步骤

阅读本文档后，您现在知道如何测试基于文件的目标配置并查看激活结果的完整详细信息。

如果您正在构建公共目标，您现在可以[将目标配置](../../guides/submit-destination.md)提交到Adobe以供审查。
