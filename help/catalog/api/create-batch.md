---
keywords: Experience Platform；首頁；熱門主題；建立批次；目錄服務；api
solution: Experience Platform
title: 在API中建立批次
description: 您可以在Catalog API中向/batches端點發出POST要求來建立批次。
exl-id: 1d2cbca9-1cd6-4b89-9b77-3687268bd849
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 3%

---

# 建立批次

為了讓資料集內嵌資料，資料集必須有關聯的批次。 使用 `id` 資料集的值，您可以透過向以下專案發出POST請求來建立批次： `/batches` 中的端點 [!DNL Catalog] API。

**API格式**

```HTTP
POST /batches
```

**请求**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| 属性 | 描述 |
| --- | --- |
| `datasetId` | 此 `id` 批次將與之關聯的資料集的ID。 |

**响应**

成功的回應會傳回HTTP狀態201 （已建立）以及包含新建立批次詳細資訊的回應物件，包括其 `id`，系統產生的唯讀字串。

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```
