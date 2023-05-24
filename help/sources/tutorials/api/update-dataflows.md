---
keywords: Experience Platform；首頁；熱門主題；流程服務；更新資料流程
solution: Experience Platform
title: 使用流量服務API更新資料流
type: Tutorial
description: 本教學課程涵蓋使用流量服務API更新資料流的步驟，包括其名稱、說明和排程。
exl-id: 367a3a9e-0980-4144-a669-e4cfa7a9c722
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 2%

---

# 使用流量服務API更新資料流

本教學課程涵蓋更新資料流的步驟，包括其基本資訊、排程及使用之對應集 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本教學課程要求您具備有效的流量ID。 如果您沒有有效的流量ID，請從「 」中選擇您選擇的聯結器 [來源概觀](../../home.md) 並依照在嘗試本教學課程之前概述的步驟進行。

本教學課程也要求您實際瞭解Adobe Experience Platform的下列元件：

* [來源](../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../landing/api-guide.md).

## 查詢資料流詳細資料

更新資料流的第一步，是使用資料流ID擷取資料流詳細資料。 您可以透過向以下網站發出GET要求，檢視現有資料流的目前詳細資料： `/flows` 端點。

**API格式**

```http
GET /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 唯一 `id` 您要擷取之資料流的值。 |

**请求**

以下請求會擷取有關您的流程ID的更新資訊。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功回應會傳回資料流的目前詳細資料，包括其版本、排程和唯一識別碼(`id`)。

```json
{
    "items": [
        {
            "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
            "createdAt": 1612310475905,
            "updatedAt": 1614122324830,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Database dataflow using BigQuery",
            "description": "collecting test1.Mytable from Google BigQuery",
            "flowSpec": {
                "id": "14518937-270c-4525-bdec-c2ba7cce3860",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "etag": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "sourceConnectionIds": [
                "b7581b59-c603-4df1-a689-d23d7ac440f3"
            ],
            "targetConnectionIds": [
                "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
                        "connectionSpec": {
                            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
                            "connectionSpec": {
                                "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "320f119a-5ac1-4ab1-88ea-eb19e674ea2e",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1612310466",
                "frequency": "week",
                "interval": "15",
                "backfill": "true"
            },
            "transformations": [
                {
                    "name": "Copy",
                    "params": {
                        "deltaColumn": {
                            "name": "Datefield",
                            "dateFormat": "YYYY-MM-DD",
                            "timezone": "UTC"
                        }
                    }
                },
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "0b090130b58b4819afc78b6dc98b484d",
                        "mappingVersion": "0"
                    }
                }
            ],
            "runs": "/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c/runs",
            "lastOperation": {
                "started": 1614122316652,
                "updated": 1614122324830,
                "percentCompleted": 100.0,
                "status": {
                    "value": "completed",
                    "errors": []
                },
                "ops": [
                    {
                        "op": "replace",
                        "path": "/scheduleParams/frequency",
                        "value": "week"
                    }
                ],
                "operation": "update"
            },
            "lastRunDetails": {
                "id": "a10cc80b-fbea-4c6b-873e-d7fd32f4d12d",
                "state": "success",
                "startedAtUTC": 1613079975512,
                "completedAtUTC": 1613080027511
            }
        }
    ]
}
```

## 更新資料流

PATCH若要更新資料流的執行排程、名稱和說明，請對 [!DNL Flow Service] API，同時提供您的流量ID、版本以及您要使用的新排程。

>[!IMPORTANT]
>
>此 `If-Match` 發出PATCH請求時需要標頭。 此標頭的值是您要更新的連線唯一版本。 每次成功更新資料流時，etag值都會隨之更新。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

下列請求會更新您的流程執行排程，以及資料流的名稱和說明。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/scheduleParams/frequency",
                "value": "day"
            },
            {
                "op": "replace",
                "path": "/name",
                "value": "Database Dataflow Feb2021"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "Database dataflow for testing update API"
            }
        ]'
```

| 属性 | 描述 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`， `replace`、和 `remove`. |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**响应**

成功的回應會傳回您的流量ID和更新的etag。 您可以向發出GET要求以驗證更新 [!DNL Flow Service] API，同時提供您的流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 更新對應

您可以透過向以下專案發出PATCH請求，更新現有資料流的對應集： [!DNL Flow Service] API並為您提供更新的值 `mappingId` 和 `mappingVersion`.

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

以下請求會更新資料流的對應集。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "50014cc8-0000-0200-0000-6036eb720000"' \
    -d '[
        {
            "op": "replace",
            "path": "/transformations/0",
            "value": {
                "name": "Mapping",
                "params": {
                    "mappingId": "c5f22f04e09f44498e528901546a83b1",
                    "mappingVersion": 2
                }
            }
        }
    ]'
```

| 属性 | 描述 |
| --- | --- |
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`， `replace`、和 `remove`. |
| `path` | 定義要更新的流程部分。 在此範例中， `transformations` 正在更新。 |
| `value.name` | 要更新的屬性名稱。 |
| `value.params.mappingId` | 用於更新資料流對應集的新對應ID。 |
| `value.params.mappingVersion` | 與更新後的對應ID相關聯的新對應版本。 |

**响应**

成功的回應會傳回您的流量ID和更新的etag。 您可以向發出GET要求以驗證更新 [!DNL Flow Service] API，同時提供您的流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

## 后续步骤

依照本教學課程，您已使用更新資料流的基本資訊、排程和對映集。 [!DNL Flow Service] API。 如需使用來源聯結器的詳細資訊，請參閱 [來源概觀](../../home.md).
