---
keywords: Experience Platform；首頁；熱門主題；流量服務；
title: 使用流程服務API的資料流草稿
description: 瞭解如何使用流量服務API將資料流設定為草稿狀態。
badge: label="新功能" type="Positive"
exl-id: aad6a302-1905-4a23-bc3d-39e76c9a22da
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# 使用Flow Service API的資料流草稿

使用流量服務API時，請提供以下專案將您的資料流儲存為草稿： `mode=draft` 建立流程呼叫期間的查詢引數。 草稿稍後可使用新資訊進行更新，並在準備就緒後發佈。 本教學課程涵蓋使用Flow Service API將資料流設定為草稿狀態的步驟。

## 快速入门

本教學課程需要您實際瞭解Adobe Experience Platform的下列元件：

* [來源](../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

### 先决条件

本教學課程要求您已經產生建立資料流所需的資產。 其中包括下列專案：

* 已驗證的基本連線
* 來源連線
* 目標XDM結構描述
* 目標資料集
* 目標連線
* 對應

如果您還沒有這些值，請從中選擇來源 [來源概觀中的目錄](../../home.md). 然後，依照該指定來源的指示產生所需的資產，以草擬資料流。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../landing/api-guide.md).

## 將資料流設定為草稿狀態

以下各節會概述將資料流設定為草稿、更新資料流、發佈資料流，以及最終刪除資料流的程式。

### 草稿資料流

若要將資料流設定為草稿，請向以下發出POST請求： `/flows` 端點 `mode=draft` 作為查詢引數。 這可讓您建立資料流並將其另存為草稿。

**API格式**

```http
POST /flows?mode=draft
```

| 参数 | 描述 |
| --- | --- |
| `mode` | 使用者提供的查詢引數，可決定資料流的狀態。 若要將資料流設定為草稿，請設定 `mode` 至 `draft`. |

**请求**

以下請求會建立草稿資料流。

```shell
  'https://platform-int.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "HTTP source dataflow for ACME data",
    "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
    ],
    "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
    ],
    "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
    }
  }'
```

**响应**

成功的回應會傳回 `id` 和對應的 `etag` 您的資料流的。

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### 更新資料流

若要更新您的草稿，請向發出PATCH請求 `/flows` 端點，同時提供您要更新的資料流ID。 在此步驟中，您還必須提供 `If-Match` 標頭引數，對應至 `etag` 要更新的資料流的ID。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**请求**

下列請求會將對應轉換新增至草擬的資料流。

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "69057131-0000-0200-0000-640f48320000"' \
  -d '[
        {
          "op": "add",
          "path": "/transformations",
          "value": [
              {
                  "name": "Mapping",
                  "params": {
                      "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
                      "mappingVersion": 0
                  }
              }
          ]
      }
  ]'
```

**响应**

成功的回應會傳回您的流量ID和 `etag`. 若要驗證變更，您可以向以下發出GET要求： `/flows` 端點，並提供您的流量ID。

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### 發佈資料流

準備好發佈草稿後，請向發出POST請求 `/flows` 端點，同時提供您要發佈的草稿資料流ID以及發佈的動作操作。

**API格式**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| 参数 | 描述 |
| --- | --- |
| `op` | 更新查詢資料流狀態的動作操作。 若要發佈草稿資料流，請設定 `op` 至 `publish`. |

**请求**

以下請求會發佈您的草稿資料流。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的回應會傳回ID和對應的 `etag` 您的資料流的。

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### 刪除資料流

若要刪除您的資料流，請向以下發出DELETE請求： `/flows` 端點，同時提供您要刪除的資料流ID。 如需有關如何使用流量服務API刪除資料流的詳細步驟，請閱讀以下指南中的 [刪除API中的資料流](./delete-dataflows.md).
