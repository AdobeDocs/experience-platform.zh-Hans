---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 创建数据集
topic: developer guide
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea

---


# 创建数据集

要使用Catalog API创建数据集，您必须知道数据集所基于的 `$id` Experience Data Model(XDM)模式的值。 获得模式ID后，可以通过向目录API中的端点发出POST请求来创 `/datasets` 建数据集。

>[!NOTE] 此文档仅介绍如何在目录中创建数据集对象。 有关如何创建、填充和监视数据集的完整步骤，请参阅以下教 [程](../datasets/create.md)。

**API格式**

```HTTP
POST /dataSets
```

**请求**

以下请求创建引用先前定义的模式的数据集。

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 要创建的数据集的名称。 |
| `schemaRef.id` | 数据集 `$id` 将基于的XDM模式的URI值。 |

>[!NOTE] 此示例将parce [文件格式](https://parquet.apache.org/documentation/latest/) 用于其属 `containerFormat` 性。 可在批量摄取开发人员指南中找到使用JSON文件格 [式的示例](../../ingestion/batch-ingestion/api-overview.md)。

**响应**

成功的响应会返回HTTP状态201（已创建）和一个响应对象，该对象由一个数组组成，该数组包含格式为新创建数据集的ID `"@/datasets/{DATASET_ID}"`。 数据集ID是系统生成的只读字符串，用于在API调用中引用数据集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
