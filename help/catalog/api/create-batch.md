---
keywords: Experience Platform；主页；热门主题；创建批处理；目录服务；API
solution: Experience Platform
title: 在API中创建批次
description: 您可以通过向Catalog API中的/batches端点发出POST请求来创建批处理。
exl-id: 1d2cbca9-1cd6-4b89-9b77-3687268bd849
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 3%

---

# 创建批次

为了让数据集摄取数据，它必须有一个关联的批次。 使用现有数据集的`id`值，您可以通过向[!DNL Catalog] API中的`/batches`端点发出POST请求来创建批次。

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
| `datasetId` | 批次将关联的数据集的`id`。 |

**响应**

成功的响应返回HTTP状态201 （已创建）和一个响应对象，该响应对象包含新创建的批次的详细信息，包括其`id`（系统生成的只读字符串）。

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
