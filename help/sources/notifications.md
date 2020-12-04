---
keywords: Experience Platform;home;popular topics; notifications
description: 通过Adobe I/O事件，您可以订阅事件并使用webhooks接收有关流运行状态的通知。 这些通知包含有关流运行成功的信息或导致运行失败的错误。
solution: Experience Platform
title: 流运行通知
topic: overview
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---


# 流运行通知

Adobe Experience Platform允许从外部来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)收集数据。

[[!DNL Adobe Experience Platform Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) 用于收集和集中来自内部不同来源的客户数据 [!DNL Platform]。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

有了Adobe I/O事件，您可以订阅事件并使用Webhook接收有关流运行状态的通知。 这些通知包含有关流运行成功的信息或导致运行失败的错误。

此文档提供了如何订阅事件、注册Web挂接以及接收包含流运行状态信息的通知的步骤。

## 入门指南

本教程假定您已创建至少一个源连接，其流运行要监视。 如果尚未配置源连接，请开始，在返回本指 [南之前](./home.md) ，访问源概述以配置您选择的源。

此文档还需要了解webhook以及如何将webhook从一个应用程序连接到另一个应用程序。 有关Webhooks的 [[!DNL I/O Events] 介绍](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) ，请参阅文档。

## 为流运行通知注册Webhook

要接收流运行通知，您必须使用Adobe开发人员控制台来注册集成的网络 [!DNL Experience Platform] 挂接。

有关如何完成此 [操 [!DNL I/O Event] 作的详细步](../observability/notifications/subscribe.md) 骤，请按照教程订阅通知。

>[!IMPORTANT]
>
>在订阅过程中，请确保选择 **[!UICONTROL 平台通知]** 作为事件提供者，然后选择以下事件订阅:
>
>* **[!UICONTROL Experience Platform源的流运行成功]**
>* **[!UICONTROL Experience Platform源的流运行失败]**


## 接收流运行通知

连接Webhook并完成事件订阅后，您可以通过Webhook仪表板开始接收流运行通知。

通知会返回信息，如运行的摄取作业数、文件大小和错误。 通知还返回与JSON格式的流运行关联的有效负荷。 响应有效负荷可以分类 `sources_flow_run_success` 为或 `sources_flow_run_failure`。

>[!IMPORTANT]
>
>如果在流创建过程中启用了部分摄取，则仅当错误数低于在流创建过程中设置的错误阈值百分比时， `sources_flow_run_success` 包含成功摄取和失败摄取的流才会标记为。 如果成功的流运行包含错误，则这些错误仍将作为返回有效负荷的一部分包含在内。

### 成功

成功的响应会返回一组定义 `metrics` 特定流运行的特性，以及描 `activities` 述数据如何转换的集合。

```json
{
  "event_id": "aec55616-1715-487f-8044-ba648cc8ffee",
  "event": {
    "createdAt": 1597213529158,
    "updatedAt": 1597213530760,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "7127a4f0-def8-11e9-83ce-e79494b1c2a5",
    "sandboxName": "prod",
    "imsOrgId": "{IMS_ORG}",
    "id": "933cf9f4-cf01-4d75-bcf9-f4cf010d750a",
    "flowId": "1c6f1047-dcaf-48fe-af10-47dcaf08feaf",
    "providerRefId": "test1234",
    "etag": "\"5100ec97-0000-0200-0000-5f338b5b0000\"",
    "metrics": {
      "durationSummary": {
        "startedAtUTC": 1590512053,
        "completedAtUTC": 1590512053
      },
      "sizeSummary": {
        "inputBytes": 2048,
        "outputBytes": 1024
      },
      "recordSummary": {
        "inputRecordCount": 100,
        "outputRecordCount": 70
      },
      "fileSummary": {
        "inputFileCount": 10,
        "outputFileCount": 10
      },
      "statusSummary": {
        "status": "success"
      }
    },
    "activities": [
      {
        "id": "copyActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "startedAtUTC": 1590512053,
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 2048,
          "outputBytes": 1098
        },
        "recordSummary": {
          "inputRecordCount": 100,
          "outputRecordCount": 100
        },
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "adf/pipeline/id": "abcd",
            "adf/run/id": "1234"
          }
        },
        "sourceInfo": [
          {
            "id": "sourceConnectionId1",
            "type": "SourceConnection",
            "reference": {
              "type": "AdfRunId"
            }
          }
        ]
      },
      {
        "id": "promotionActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 1098,
          "outputBytes": 1024
        },
        "recordSummary": {},
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10,
          "extensions": {
            "manifest": {
              "fileInfo": "https://platform-int.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
            }
          }
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "batchId": "b1",
            "acp_request_id": "1234"
          }
        },
        "targetInfo": [
          {
            "id": "targetConnectionId1",
            "type": "TargetConnection",
            "reference": {
              "type": "batch"
            }
          }
        ]
      }
    ],
    "slaCreatedAt": 1597213531124,
    "processStartTime": 1597213531213,
    "header": {
      "_adobeio": {
        "imsOrgId": "{IMS_ORG}",
        "providerMetadata": "platform_notifications",
        "eventCode": "sources_flow_run_success"
      }
    },
    "transformedTime": 1597213531214
  }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `metrics` | 定义流运行中数据的特性。 |
| `activities` | 定义转换数据时执行的不同步骤和活动。 |
| `durationSummary` | 定义流运行的开始和结束时间。 |
| `sizeSummary` | 定义数据的卷（以字节为单位）。 |
| `recordSummary` | 定义数据的记录计数。 |
| `fileSummary` | 定义数据的文件计数。 |
| `fileInfo` | 一个URL，用于导致成功摄取的文件的概述。 |
| `statusSummary` | 定义流运行是成功还是失败。 |

### 失败

以下响应是流运行失败的示例，在处理复制的数据时出错。 从源复制数据时也可能出错。 失败的流运行包含有关导致运行失败的错误的信息，包括其错误和说明。

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{IMS_ORG}",
        "schema": {
          "name": "run-notification",
          "version": "1.0"
        },
        "provider": "FlowService",
        "_eventNotificationMeta": {
          "category": "Platform Notifications",
          "type": "sources_flow_run_failed"
        },
        "value": {
          "createdAt": 1597434147259,
          "updatedAt": 1597434157567,
          "createdBy": "{CREATED_BY}",
          "updatedBy": "{UPDATED_BY}",
          "createdClient": "{CREATED_CLIENT}",
          "updatedClient": "{UPDATED_CLIENT}",
          "sandboxId": "e49ebb00-d0fa-11e9-b164-ed6a398c8b35",
          "sandboxName": "prod",
          "imsOrgId": "{IMS_ORG}",
          "id": "d9024c32-2174-4271-824c-322174627101",
          "flowId": "cf4fce79-8822-456d-8fce-798822556dc6",
          "etag": "\"0c003dbf-0000-0200-0000-5f36e92d0000\"",
          "metrics": {
            "durationSummary": {
              "startedAtUTC": 1597434147190
            },
            "sizeSummary": {
              "inputBytes": -1
            },
            "fileSummary": {
              "inputFileCount": -1
            },
            "statusSummary": {
              "status": "failed",
              "errors": [
                {
                  "code": "CONNECTOR-2001-500",
                  "message": "Error in processing (parsing, validation or transformation) the copied data."
                }
              ]
            }
          },
          "activities": [
            {
              "id": "promotionActivity",
              "updatedAtUTC": 1597434157529,
              "durationSummary": {
                "startedAtUTC": 1597434147190,
                "completedAtUTC": 1597434157212
              },
              "sizeSummary": {
                "inputBytes": -1
              },
              "recordSummary": {},
              "fileSummary": {
                "inputFileCount": -1,
                "extensions": {
                  "manifest": {
                    "fileInfo": "https://platform-stage.adobe.io/data/foundation/export/batches/6f6a900f-e40d-4f0e-9bb9-b614436c3465/meta?path=input_files"
                  }
                }
              },
              "statusSummary": {
                "status": "failed",
                "errors": [
                  {
                    "code": "CONNECTOR-2001-500",
                    "message": "Error in processing (parsing, validation or transformation) the copied data."
                  }
                ],
                "extensions": {
                  "errors": [
                    {
                      "code": "133",
                      "message": "We are unable to locate any files uploaded for this batch. Please upload files to ingest."
                    }
                  ]
                }
              },
              "targetInfo": [
                {
                  "id": "e88737aa-27b8-4795-8737-aa27b8f7959e",
                  "type": "TargetConnection",
                  "reference": {
                    "type": "Batch",
                    "ids": [
                      "6f6a900f-e40d-4f0e-9bb9-b614436c3465"
                    ]
                  }
                }
              ]
            }
          ]
        }
      }
    ]
  }
]
```

| 属性 | 描述 |
| ---------- | ----------- |
| `fileInfo` | 一个URL，用于导致对成功和未成功摄取的文件进行概述。 |

>[!NOTE]
>
>有关错误 [消息](#errors) ，请参阅附录。

## 后续步骤

您现在可以订阅事件，它们允许您接收流运行状态的实时通知。 有关流运行和源的详细信息，请参阅 [源概述](./home.md)。

## 附录

以下各节提供了有关处理流运行通知的其他信息。

### 了解错误消息 {#errors}

从源复制数据或将复制的数据处理到时，可能会发生摄取错误 [!DNL Platform]。 有关特定错误的详细信息，请参阅下表。

| 错误 | 描述 |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | 从源复制数据时出错。 |
| `CONNECTOR-2001-500` | 将复制的数据处理到时出错 [!DNL Platform]。 此错误可能与分析、验证或转换相关。 |