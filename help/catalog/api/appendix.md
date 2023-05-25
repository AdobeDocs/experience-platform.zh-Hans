---
keywords: Experience Platform；主页；热门主题；目录服务；目录API；附录
solution: Experience Platform
title: 目录服务API指南附录
description: 本文档包含帮助您在Adobe Experience Platform中使用目录API的其他信息。
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 1%

---

# [!DNL Catalog Service] API指南附录

本文档包含帮助您使用 [!DNL Catalog] API。

## 查看相互关联的对象 {#view-interrelated-objects}

部分 [!DNL Catalog] 对象可以与其他 [!DNL Catalog] 对象。 任何前缀为 `@` 响应有效负载表示相关对象。 这些字段的值采用URI的形式，可以在单独的GET请求中使用，以检索它们表示的相关对象。

上的文档中返回的示例数据集 [查找特定数据集](look-up-object.md) 包含 `files` 具有以下URI值的字段： `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. 的内容 `files` 字段可以通过使用此URI作为新GET请求的路径来查看。

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
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
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

## 在一次调用中提出多个请求

的根端点 [!DNL Catalog] API允许在单个调用中提出多个请求。 请求有效负载包含一个对象数组，表示通常为各个请求的对象，然后按顺序执行。

如果这些请求是对的修改或添加 [!DNL Catalog] 任何一项更改都将失败，所有更改都将恢复。

**API格式**

```http
POST /
```

**请求**

以下请求创建一个新数据集，然后为该数据集创建相关视图。 此示例演示了如何使用模板语言来访问在先前调用中返回的值，以便在后续调用中使用。

例如，如果要引用从上一个子请求返回的值，可以创建以下格式的引用： `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (其中 `{REQUEST_ID}` 是用户为子请求提供的ID，如下所示)。 您可以使用这些模板引用上一个子请求的响应对象正文中可用的任何属性。

>[!NOTE]
>
>当执行的子请求仅返回对对象的引用(这是目录API中大多数POST和PUT请求的默认值)时，此引用将别名为值 `id` 和可以用作  `<<{OBJECT_ID}.id>>`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "id": "firstObjectId",
      "resource": "/dataSets",
      "method": "post",
      "body": {
        "type": "raw",
        "name": "First Dataset"
      }
    }, 
    {
      "id": "secondObjectId",
      "resource": "/datasetViews",
      "method": "post",
      "body": {
        "status": "enabled",
        "dataSetId": "<<firstObjectId.id>>"
      }
    }
  ]'
```

| 属性 | 描述 |
| --- | --- |
| `id` | 附加到响应对象的用户提供的ID，以便您可以将请求与响应进行匹配。 [!DNL Catalog] 不会存储此值，而只是将其返回响应以供参考。 |
| `resource` | 相对于根的资源路径 [!DNL Catalog] API。 协议和域不应包含在此值中，它的前缀应为“/”。 <br/><br/> 将PATCH或DELETE用作子请求的 `method`，在资源路径中包含对象ID。 不要与用户提供的混淆 `id`，则资源路径使用的ID [!DNL Catalog] 对象本身(例如， `resource: "/dataSets/1234567890"`)。 |
| `method` | 与请求中发生的操作相关的方法(GET、PUT、POST、PATCH或DELETE)的名称。 |
| `body` | 通常作为POST、PUT或PATCH请求中的有效负载传递的JSON文档。 GET或DELETE请求不需要此属性。 |

**响应**

成功的响应会返回一个对象数组，其中包含 `id` 您分配给每个请求的HTTP状态代码以及响应 `body`. 由于三个示例请求都是创建新对象，因此 `body` 每个对象都是一个仅包含新创建对象的ID的数组，这是中大多数成功POST响应的标准 [!DNL Catalog].

```json
[
    {
        "id": "firstObjectId",
        "code": 200,
        "body": [
            "@/dataSets/5be230aef5b02914cd52dbfa"
        ]
    },
    {
        "id": "secondObjectId",
        "code": 200,
        "body": [
            "@/dataSetViews/5be230aef5b02914cd52dbfb"
        ]
    }
]
```

检查对多个请求的响应时请务必谨慎，因为您将需要验证每个单独子请求的代码，而不是仅依赖父POST请求的HTTP状态代码。  单个子请求可能会返回404(例如，对无效资源的GET请求)，而整体请求返回200。

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
