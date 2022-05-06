---
keywords: Experience Platform；主页；热门主题；数据集；数据集；创建数据集；创建数据集；启用数据集
solution: Experience Platform
title: 在API中创建数据集
topic-legacy: developer guide
description: 本文档介绍如何在目录服务API中创建数据集对象。
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# 在API中创建数据集

要使用 [!DNL Catalog] API，您必须知道 `$id` 值 [!DNL Experience Data Model] (XDM)数据集所基于的架构。 获得架构ID后，您可以通过向 `/datasets` 的端点 [!DNL Catalog] API。

>[!NOTE]
>
>本文档仅介绍如何在 [!DNL Catalog]. 有关如何创建、填充和监视数据集的完整步骤，请参阅以下内容 [教程](../datasets/create.md).

**API格式**

```HTTP
POST /dataSets
```

**请求**

以下请求会创建一个引用先前定义架构的数据集。

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 要创建的数据集的名称。 |
| `schemaRef.id` | URI `$id` 数据集将基于的XDM架构的值。 |
| `schemaRef.contentType` | 指示架构的格式和版本。 请参阅 [模式版本控制](../../xdm/api/getting-started.md#versioning) ，以了解更多信息。 |

>[!NOTE]
>
>此示例使用 [Apache Parquet](https://parquet.apache.org/docs/) 其文件格式 `containerFormat` 属性。 在 [批量获取开发人员指南](../../ingestion/batch-ingestion/api-overview.md).

**响应**

成功的响应会返回HTTP状态201（已创建）和一个响应对象，该对象包含一个数组，其中包含以格式新创建数据集的ID `"@/datasets/{DATASET_ID}"`. 数据集ID是由系统生成的只读字符串，用于在API调用中引用数据集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
