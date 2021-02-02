---
keywords: Experience Platform；主页；热门主题；数据集；数据集；创建数据集；创建数据集；启用数据集
solution: Experience Platform
title: 创建数据集
topic: developer guide
description: 此文档介绍如何在“目录”中创建数据集对象。
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 1%

---


# 创建数据集

要使用[!DNL Catalog] API创建数据集，您必须知道数据集所基于的[!DNL Experience Data Model](XDM)模式的`$id`值。 获得模式ID后，您可以通过向[!DNL Catalog] API中的`/datasets`端点发出POST请求来创建数据集。

>[!NOTE]
>
>此文档仅涵盖如何在[!DNL Catalog]中创建数据集对象。 有关如何创建、填充和监视数据集的完整步骤，请参阅以下[教程](../datasets/create.md)。

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
| `schemaRef.id` | 数据集将基于的XDM模式的URI `$id`值。 |

>[!NOTE]
>
>此示例将[Apache Parke](https://parquet.apache.org/documentation/latest/)文件格式用于其`containerFormat`属性。 使用JSON文件格式的示例可在[批处理摄取开发人员指南](../../ingestion/batch-ingestion/api-overview.md)中找到。

**响应**

成功的响应返回HTTP状态201（已创建）和一个响应对象，该对象由一个数组组成，该数组包含格式为`"@/datasets/{DATASET_ID}"`的新创建数据集的ID。 数据集ID是由系统生成的只读字符串，用于在API调用中引用数据集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
