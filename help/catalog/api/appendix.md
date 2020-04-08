---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 目录服务开发人员指南附录
topic: developer guide
translation-type: tm+mt
source-git-commit: 409d98818888f2758258441ea2d993ced48caf9a

---


# 目录服务开发人员指南附录

本文档包含帮助您使用目录API的其他信息。

## 视图相关对象 {#view-interrelated-objects}

某些Catalog对象可以与其他Catalog对象相关联。 响应有效负荷中前缀的 `@` 任何字段都表示相关对象。 这些字段的值采用URI的形式，URI可用于单独的GET请求中以检索它们表示的相关对象。

查找特定数据集时在文档中返 [回的示例数据集包含一个具有以](look-up-object.md) 下URI值的字段 `files` : `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. 使用此URI `files` 作为新GET请求的路径可查看字段的内容。

**API格式**

```http
GET {OBJECT_URI}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_URI}` | 由相关对象字段（不包括符号）提供 `@` 的URI。 |

**请求**

以下请求使用示例数据集的属性提供的URI `files` 来检索数据集的关联文件的列表。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回相关对象的列表。 在此示例中，返回一列表数据集文件。

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## 在一次呼叫中发出多个请求

目录API的根端点允许在单个调用中发出多个请求。 请求有效负荷包含表示通常是单个请求的对象的数组，然后按顺序执行这些请求。

如果这些请求是对目录的修改或添加，并且任何更改都失败，则所有更改都将恢复。

**API格式**

```http
POST /
```

**请求**

以下请求将创建一个新数据集，然后为该数据集创建相关视图。 此示例演示了如何使用模板语言访问在先前调用中返回的值，以便在后续调用中使用。

例如，如果要引用从先前的子请求返回的值，则可以创建以下格式的引用：(其 `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>``{REQUEST_ID}` 中是用户为子请求提供的ID，如下所示)。 您可以使用这些模板引用先前子请求的响应对象正文中可用的任何属性。

>[!NOTE] 当执行的子请求只返回对对象的引用（Catalog API中大多数POST和PUT请求的默认值）时，此引用将别名设置为该值， `id` 并可用作 `<<{OBJECT_ID}.id>>`。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `id` | 用户提供的ID，该ID附加到响应对象，以便您能够匹配对响应的请求。 Catalog不存储此值，只是将其返回到响应中以供参考。 |
| `resource` | 相对于目录API根目录的资源路径。 协议和域不应是此值的一部分，并且应在前缀为“/”。 <br/><br/> 使用PATCH或DELETE作为子请求时， `method`在资源路径中包含对象ID。 请勿将资源路径与用户提供的 `id`路径混淆，该资源路径使用Catalog对象本身的ID(例如 `resource: "/dataSets/1234567890"`)。 |
| `method` | 与请求中所执行的操作相关的方法的名称（GET、PUT、POST、PATCH或DELETE）。 |
| `body` | JSON文档，通常作为POST、PUT或PATCH请求中的有效负荷传递。 GET或DELETE请求不需要此属性。 |

**响应**

成功的响应会返回一组对象，其中包含您为每个请 `id` 求分配的对象、单个请求的HTTP状态代码和响应 `body`。 由于三个范例请求都是为了创建新对象，因此每个对象的数组只包含新创建对象的ID，这也是目录中POST响应最成功的标准。 `body`

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

检查对多个请求的响应时要小心，因为您需要验证每个单个子请求的代码，而不只依赖父POST请求的HTTP状态代码。  单个子请求可以返回404（例如，对无效资源的GET请求），而总请求返回200。

## 其他请求标题

Catalog提供了多种标题约定，帮助您在更新过程中保持数据的完整性。

### If-Match

最好使用对象版本控制来防止当一个对象被多个用户几乎同时保存时发生的数据损坏类型。

更新对象时的最佳实践是首先对要更新的对象进行API调用视图(GET)。 包含在响应中（以及响应包含单个对象的任何调用）是包含 `E-Tag` 该对象版本的标题。 将对象版本添加为在更新（PUT或PATCH）调用中命名的请求标题，只有在版本仍然相同的情况下，更新才会成功，这有助于防止数据冲突。 `If-Match`

如果版本不匹配（自您检索到该对象后，该对象被其他进程修改），您将收到HTTP状态412（先决条件失败），指示已拒绝对目标资源的访问。

### Pragma

有时，您可能希望验证对象而不保存信息。 使用 `Pragma` 值为的标题可仅发 `validate-only` 送POST或PUT请求以进行验证，从而防止对数据所做的任何更改被保留。

## 数据压缩

压缩是一项Experience Platform服务，可将小文件中的数据合并到大文件中，而无需更改任何数据。 出于性能原因，有时将一组小文件合并为较大的文件，以便在查询时更快地访问数据是有益的。

当摄取的批次中的文件已压缩后，其关联的“目录”对象将更新以用于监视目的。