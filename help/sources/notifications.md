---
keywords: Experience Platform；首頁；熱門主題；通知
description: 透過訂閱Adobe I/O事件，您可以使用Webhook接收有關來源連線之流量執行狀態的通知。 這些通知包含有關流程執行成功或導致執行失敗的錯誤的資訊。
solution: Experience Platform
title: 流程執行通知
exl-id: 0f1cde97-3030-4b8e-be08-21f64e78b794
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# 流程執行通知

Adobe Experience Platform可從外部來源擷取資料，同時讓您能夠使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 用於收集及集中客戶資料，這些資料來自內的各種不同來源 [!DNL Platform]. 此服務提供可連線所有支援來源的使用者介面和RESTful API。

透過Adobe I/O事件，您可以訂閱事件並使用Webhook接收有關流量執行狀態的通知。 這些通知包含有關流程執行成功或導致執行失敗的錯誤的資訊。

本檔案提供訂閱事件、註冊Webhook及接收包含流量執行狀態資訊之通知的步驟。

## 快速入门

本教學課程假設您已建立至少一個來源連線，其流程執行您要監視。 如果您尚未設定來源連線，請先造訪 [來源概觀](./home.md) 以在返回本指南之前設定您選擇的來源。

本檔案還需要實際瞭解webhook以及如何將webhook從一個應用程式連線到另一個應用程式。 請參閱 [[!DNL I/O Events] 檔案](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) 以瞭解webhook。

## 註冊webhook以取得資料流執行通知

若要接收資料流執行通知，您必須使用Adobe Developer Console將webhook註冊到 [!DNL Experience Platform] 整合。

請依照上的教學課程進行 [訂閱[！DNL I/O Event]通知](../observability/alerts/subscribe.md) 以取得如何完成此作業的詳細步驟。

>[!IMPORTANT]
>
>在訂閱程式期間，請確定您選取 **[!UICONTROL 平台通知]** 作為事件提供者，並選取下列事件訂閱：
>
>* **[!UICONTROL Experience Platform來源的流程執行成功]**
>* **[!UICONTROL Experience Platform來源的流程執行失敗]**


## 接收流程執行通知

在您的webhook已連線且事件訂閱完成時，您可以開始透過webhook儀表板接收流程執行通知。

通知會傳回執行內嵌工作數、檔案大小和錯誤等資訊。 通知也會傳回與您以JSON格式執行的流程相關聯的裝載。 回應裝載可分類為 `sources_flow_run_success` 或 `sources_flow_run_failure`.

>[!IMPORTANT]
>
>如果在流程建立過程中啟用了部分擷取，則包含成功和失敗擷取的流程將標籤為 `sources_flow_run_success` 僅當錯誤數低於流程建立處理期間設定的錯誤臨界值百分比時。 如果成功的流量執行包含錯誤，這些錯誤仍會包含在傳回裝載中。

### 成功

成功的回應會傳回一組 `metrics` 定義特定流程執行的特性，以及 `activities` 概述資料如何轉換。

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
    "imsOrgId": "{ORG_ID}",
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
              "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
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
        "imsOrgId": "{ORG_ID}",
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
| `metrics` | 定義資料流執行中的資料特性。 |
| `activities` | 定義轉換資料所執行的不同步驟和活動。 |
| `durationSummary` | 定義流程執行的開始和結束時間。 |
| `sizeSummary` | 定義資料量（位元組）。 |
| `recordSummary` | 定義資料的記錄計數。 |
| `fileSummary` | 定義資料的檔案計數。 |
| `fileInfo` | 導向成功擷取檔案概觀的URL。 |
| `statusSummary` | 定義流程執行是成功還是失敗。 |

### 失败

以下回應是失敗的流程執行範例，在處理複製的資料時發生錯誤。 從來源複製資料時也可能發生錯誤。 失敗的流程執行包含造成執行失敗的錯誤相關資訊，包括其錯誤和說明。

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{ORG_ID}",
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
          "imsOrgId": "{ORG_ID}",
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
| `fileInfo` | 此URL會導向成功擷取及未成功擷取的檔案概觀。 |

>[!NOTE]
>
>請參閱 [附錄](#errors) 以取得錯誤訊息的詳細資訊。

## 后续步骤

您現在可以訂閱事件，以接收有關流量執行狀態的即時通知。 如需流量執行和來源的詳細資訊，請參閱 [來源概觀](./home.md).

## 附录

以下小節提供處理流程執行通知的其他資訊。

### 瞭解錯誤訊息 {#errors}

從來源複製資料或將複製的資料處理至時，可能會發生內嵌錯誤 [!DNL Platform]. 請參閱下表以取得有關特定錯誤的詳細資訊。

| 错误 | 描述 |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | 從來源複製資料時發生錯誤。 |
| `CONNECTOR-2001-500` | 將複製的資料處理至時發生錯誤 [!DNL Platform]. 此錯誤可能涉及解析、驗證或轉換。 |
