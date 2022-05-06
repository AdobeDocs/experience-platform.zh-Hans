---
keywords: Experience Platform；主页；热门主题；目录服务；目录API；附录
solution: Experience Platform
title: 目录服务API指南附录
topic-legacy: developer guide
description: 本文档包含其他信息，可帮助您在Adobe Experience Platform中使用目录API。
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 1%

---

# [!DNL Catalog Service] API指南附录

本文档包含其他信息，可帮助您使用 [!DNL Catalog] API。

## 查看相关对象 {#view-interrelated-objects}

部分 [!DNL Catalog] 对象可以与其他对象相关联 [!DNL Catalog] 对象。 前缀为 `@` 响应负载表示相关对象。 这些字段的值采用URI的形式，URI可用于单独的GET请求中以检索它们表示的相关对象。

在 [查找特定数据集](look-up-object.md) 包含a `files` 字段，其URI值如下： `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. 的内容 `files` 使用此URI作为新GET请求的路径，可以查看字段。

**API格式**

```http
GET {OBJECT_URI}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_URI}` | 由相关对象字段提供的URI(不包括 `@` 符号)。 |

**请求**

以下请求使用示例数据集提供的URI `files` 属性来检索数据集关联文件的列表。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回相关对象的列表。 在此示例中，会返回数据集文件的列表。

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

## 在一次调用中发出多个请求

的根端点 [!DNL Catalog] API允许在一次调用中发出多个请求。 请求有效负载包含一个对象数组，这些对象表示通常是单个请求，然后按顺序执行。

如果这些请求是对 [!DNL Catalog] 任何一项更改都会失败，所有更改都将还原。

**API格式**

```http
POST /
```

**请求**

以下请求会创建一个新数据集，然后为该数据集创建相关视图。 此示例演示如何使用模板语言访问在先前调用中返回的值，以供在后续调用中使用。

例如，如果要引用从上一个子请求返回的值，则可以创建以下格式的引用： `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (其中 `{REQUEST_ID}` 是用户提供的子请求的ID，如下所示)。 您可以使用这些模板引用先前子请求响应对象正文中可用的任何属性。

>[!NOTE]
>
>当执行的子请求仅返回对对象的引用(与目录API中大多数POST和PUT请求的默认值相同)时，此引用将别名为值 `id` 和可用作  `<<{OBJECT_ID}.id>>`.

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
| `id` | 用户提供的ID，附加到响应对象，以便您可以匹配对响应的请求。 [!DNL Catalog] 不存储此值，只是在响应中返回它以供参考。 |
| `resource` | 相对于的根的资源路径 [!DNL Catalog] API。 协议和域不应包含在此值中，并且应带有前缀“/”。 <br/><br/> 使用PATCH或DELETE作为子请求的 `method`，在资源路径中包含对象ID。 不要与用户提供的混淆 `id`，则资源路径使用的ID为 [!DNL Catalog] 对象本身(例如， `resource: "/dataSets/1234567890"`)。 |
| `method` | 与请求中发生的操作相关的方法(GET、PUT、POST、PATCH或DELETE)的名称。 |
| `body` | 通常作为POST、PUT或PATCH请求中的有效负载传递的JSON文档。 GET或DELETE请求不需要此属性。 |

**响应**

成功的响应会返回包含 `id` 分配给每个请求的HTTP状态代码，以及响应 `body`. 由于三个示例请求都是为创建新对象，因此 `body` 每个对象的是一个仅包含新创建对象ID的数组，例如中具有最成功POST响应的标准 [!DNL Catalog].

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

检查对多请求的响应时请务必小心，因为您需要验证每个子请求的代码，而不是仅依赖父POST请求的HTTP状态代码。  单个子请求可返回404(例如对无效资源的GET请求)，而整体请求返回200。

## 其他请求头

[!DNL Catalog] 提供了多种标题约定，可帮助您在更新期间保持数据的完整性。

### If-Match

最好使用对象版本控制来防止当一个对象被多个用户近乎同时保存时发生的数据类型损坏。

更新对象时的最佳实践是首先进行API调用以查看(GET)要更新的对象。 包含在响应中（以及响应中包含单个对象的任何调用）是 `E-Tag` 包含对象版本的标头。 将对象版本添加为名为的请求标头 `If-Match` 在您的更新(PUT或PATCH)调用中，仅当版本仍然相同时，才会导致更新成功，从而有助于防止数据冲突。

如果版本不匹配（自您检索到对象后，该对象被其他进程修改），您将收到HTTP状态412（先决条件失败），指示对目标资源的访问被拒绝。

### Pragma

有时，您可能希望验证对象而不保存信息。 使用 `Pragma` 值为 `validate-only` 允许您仅出于验证目的发送POST或PUT请求，以防止对数据进行任何更改。

## 数据压缩

压缩是 [!DNL Experience Platform] 将小文件中的数据合并到大文件中而无需更改任何数据的服务。 出于性能原因，有时将一组小文件合并为较大的文件，以便在查询时更快地访问数据是有益的。

在摄取的批处理中的文件已压缩后，会关联 [!DNL Catalog] 对象已更新以用于监控。
