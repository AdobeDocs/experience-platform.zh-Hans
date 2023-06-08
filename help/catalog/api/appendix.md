---
keywords: Experience Platform；主页；热门主题；目录服务；目录API；附录
solution: Experience Platform
title: 目录服务API指南附录
description: 本文档包含帮助您在Adobe Experience Platform中使用目录API的其他信息。
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 24db94b959d1bad925af1e8e9cbd49f20d9a46dc
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 1%

---

# [!DNL Catalog Service] API指南附录

本文档包含帮助您使用 [!DNL Catalog] API。

## 查看相互关联的对象 {#view-interrelated-objects}

部分 [!DNL Catalog] 对象可以与其他 [!DNL Catalog] 对象。 任何前缀为 `@` 响应有效负载表示相关对象。 这些字段的值采用URI的形式，可以在单独的GET请求中使用，以检索它们表示的相关对象。

上的文档中返回的示例数据集 [查找特定数据集](look-up-object.md) 包含 `files` 具有以下URI值的字段： `"@/datasetFiles?datasetId={DATASET_ID}"`. 的内容 `files` 字段可以通过使用此URI作为新GET请求的路径来查看。

**API格式**

```http
GET {OBJECT_URI}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_URI}` | 由相关对象字段提供的URI(不包括 `@` 符号)。 |

**请求**

以下请求使用的URI提供了示例数据集的 `files` 属性，用于检索数据集的关联文件列表。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/datasetFiles?datasetId={DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回相关对象的列表。 在此示例中，返回数据集文件的列表。

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573256315368,
        "updated": 1573256315368
    },
    "148ac690-0280-11ea-8d23-8571a35dce49-1": {
        "id": "148ac690-0280-11ea-8d23-8571a35dce49-1",
        "batchId": "148ac690-0280-11ea-8d23-8571a35dce49",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573255982433,
        "updated": 1573255982433
    },
    "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1": {
        "id": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1",
        "batchId": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## 其他请求标头

[!DNL Catalog] 提供了多种标头约定，以帮助您在更新期间保持数据的完整性。

### If-Match

最好使用对象版本控制，以防止当多个用户几乎同时保存某个对象时发生的数据损坏类型。

更新对象的最佳实践包括首先进行API调用以查看(GET)要更新的对象。 包含在响应中（以及响应中包含单个对象的任何调用）是 `E-Tag` 包含对象版本的标头。 将对象版本添加为名为的请求标头 `If-Match` 只有在版本仍然相同的情况下，更新(PUT或PATCH)调用才会导致更新成功，有助于防止数据冲突。

如果版本不匹配（对象在检索后已被另一进程修改），您将收到HTTP状态412（前提条件失败），指示对目标资源的访问已被拒绝。

### Pragma

有时，您可能希望在不保存信息的情况下验证对象。 使用 `Pragma` 值为的标题 `validate-only` 允许您仅出于验证目的发送POST或PUT请求，从而防止保留对数据所做的任何更改。

## 数据压缩

压缩是一个 [!DNL Experience Platform] 一种服务，可将小文件中的数据合并到大文件中，而不需更改任何数据。 出于性能原因，有时将一组小文件合并为大文件会很有用，以便在查询时提供对数据的更快访问。

压缩了所摄取批次中的文件时，其关联的 [!DNL Catalog] 更新对象以进行监视。
