---
keywords: Experience Platform;home;popular topics;Catalog service;catalog api;appendix
solution: Experience Platform
title: 目录服务开发人员指南附录
topic: developer guide
description: 此文档包含帮助您使用Adobe Experience Platform的Catalog API的其他信息。
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---


# [!DNL Catalog Service] 开发人员指南附录

此文档包含帮助您使用API的其他 [!DNL Catalog] 信息。

## 视图相关对象 {#view-interrelated-objects}

某些 [!DNL Catalog] 对象可以与其他对象相 [!DNL Catalog] 关联。 响应有效负荷中前缀 `@` 的任何字段都表示相关对象。 这些字段的值采用URI的形式，URI可在单独的GET请求中使用，以检索它们表示的相关对象。

查找特定数据集时在文档 [中返回的示例数据集](look-up-object.md) ，包 `files` 含具有以下URI值的字段： `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. 可以使用 `files` 此URI作为新GET请求的路径来查看字段的内容。

**API格式**

```http
GET {OBJECT_URI}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_URI}` | 由相关对象字段（不包括符号）提供 `@` 的URI。 |

**请求**

以下请求使用示例数据集的属性提 `files` 供的URI来检索数据集关联文件的列表。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回相关对象的列表。 在此示例中，返回列表数据集文件。

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

API的根端点 [!DNL Catalog] 允许在单个调用中发出多个请求。 请求有效负荷包含表示通常是单个请求的对象的数组，然后按顺序执行。

如果这些请求是对的修改或添加， [!DNL Catalog] 并且任何一项更改都失败，则所有更改都将恢复。

**API格式**

```http
POST /
```

**请求**

以下请求会创建新数据集，然后为该数据集创建相关视图。 此示例演示如何使用模板语言访问先前调用中返回的值，以便在后续调用中使用。

例如，如果要引用从以前的子请求返回的值，则可以创建以下格式的引用： `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (其中 `{REQUEST_ID}` 是用户为子请求提供的ID，如下所示)。 您可以使用这些模板来引用先前子请求响应对象正文中可用的任何属性。

>[!NOTE]
>
>当执行的子请求仅返回对对象的引用(在目录API中大多数POST和PUT请求的默认值)时，此引用将别名 `id` 化为值并可用作 `<<{OBJECT_ID}.id>>`。

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
| `id` | 用户提供的ID，该ID附加到响应对象，以便您能够匹配对响应的请求。 [!DNL Catalog] 不存储此值，只是将其返回到响应中以供参考。 |
| `resource` | 相对于API根的资源路 [!DNL Catalog] 径。 协议和域不应是此值的一部分，它应前缀为“/”。 <br/><br/> 将PATCH或DELETE用作子请求时， `method`在资源路径中包含对象ID。 请勿将资源路径与用户提 `id`供的内容混淆，资源路径使 [!DNL Catalog] 用对象本身的ID(例如 `resource: "/dataSets/1234567890"`)。 |
| `method` | 与请求中所执行的操作相关的方法的名称(GET、PUT、POST、PATCH或DELETE)。 |
| `body` | 通常在POST、PUT或PATCH请求中作为有效负荷传递的JSON文档。 GET或DELETE请求不需要此属性。 |

**响应**

成功的响应会返回一组对象，其中 `id` 包含您分配给每个请求的对象、单个请求的HTTP状态代码以及响应 `body`。 由于三个示例请求都是为了创建新对象，因此每个对象的 `body` 数组只包含新创建对象的ID，而标准POST响应中的ID最成功 [!DNL Catalog]。

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

检查对多个请求的响应时要小心，因为您需要验证每个单个子请求的代码，而不是只依赖父POST请求的HTTP状态代码。  单个子请求可返回404(例如对无效资源的GET请求)，而总请求返回200。

## 其他请求标头

[!DNL Catalog] 提供了多种标题约定，帮助您在更新过程中保持数据的完整性。

### If-Match

最好使用对象版本控制来防止在多个用户几乎同时保存对象时发生的数据损坏类型。

更新对象时的最佳实践是首先对要更新的对象进行API调用视图(GET)。 包含在响应中（以及响应包含单个对象的任何调用） `E-Tag` 是包含该对象版本的标题。 将对象版本添加为在更新(PUT或PATCH `If-Match` )调用中命名的请求标头，将导致只有在版本仍然相同的情况下更新才能成功，从而有助于防止数据冲突。

如果版本不匹配（自您检索到该对象后，该对象被其他进程修改），您将收到HTTP状态412（先决条件失败），表示已拒绝访问目标资源。

### Pragma

有时，您可能希望验证对象而不保存信息。 使用 `Pragma` 值为的标头 `validate-only` 可仅发送POST或PUT请求以进行验证，从而防止对数据所做的任何更改被保留。

## 数据压缩

压缩是一种将 [!DNL Experience Platform] 小文件中的数据合并到大文件中，而不更改任何数据的服务。 出于性能原因，有时将一组小文件合并为较大的文件，以便在查询时能够更快地访问数据。

当摄取的批次中的文件已压缩时，其关联对 [!DNL Catalog] 象将更新以用于监视。