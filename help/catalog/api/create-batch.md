---
keywords: Experience Platform；主页；热门主题；创建批处理；目录服务；API
solution: Experience Platform
title: 在API中创建批处理
topic-legacy: developer guide
description: 您可以通过向目录API中的/batches端点发出POST请求来创建批处理。
exl-id: 1d2cbca9-1cd6-4b89-9b77-3687268bd849
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 3%

---

# 创建批处理

为了使数据集能够摄取数据，它必须具有一个与其关联的批次。 使用 `id` 值时，您可以通过向POST请求创建批次 `/batches` 的端点 [!DNL Catalog] API。

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
| `datasetId` | 的 `id` 该批次将关联的数据集中。 |

**响应**

成功的响应会返回HTTP状态201（已创建）以及包含新创建批处理详细信息(包括其 `id`，系统生成的只读字符串。

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
