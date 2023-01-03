---
keywords: Experience Platform；主页；热门主题；过滤器；过滤器；过滤数据；过滤数据；日期范围
solution: Experience Platform
title: 使用查询参数筛选目录数据
topic-legacy: developer guide
description: 目录服务API允许通过使用请求查询参数过滤响应数据。 “目录”的最佳实践之一是在所有API调用中使用过滤器，因为它们可减少API上的负载并帮助提高整体性能。
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2121'
ht-degree: 1%

---

# 过滤器 [!DNL Catalog] 使用查询参数的数据

的 [!DNL Catalog Service] API允许通过使用请求查询参数过滤响应数据。 的最佳实践 [!DNL Catalog] 是在所有API调用中使用过滤器，因为它们可减少API的负载并帮助提高整体性能。

本文档概述了最常用的筛选方法 [!DNL Catalog] 对象。 建议您在阅读 [目录开发人员指南](getting-started.md) 详细了解如何与 [!DNL Catalog] API。 有关 [!DNL Catalog Service]，请参阅 [[!DNL Catalog] 概述](../home.md).

## 限制返回的对象

的 `limit` 查询参数约束响应中返回的对象数。 [!DNL Catalog] 根据配置的限制自动对响应进行计费：

* 如果 `limit` 参数，则每个响应有效负载的最大对象数为20。
* 对于数据集查询(如果 `observableSchema` 使用 `properties` 查询参数中，返回的数据集数量上限为20个。
* 所有其他目录查询的全局限制为100个对象。
* 无效 `limit` 参数(包括 `limit=0`)会导致400级错误响应，其中列出了适当的范围。
* 作为查询参数传递的限制或偏移优先于作为标题传递的限制或偏移。

**API格式**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要检索的对象。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | 一个整数，表示要返回的对象数，介于1到100之间。 |

**请求**

以下请求在将响应限制为三个对象时检索数据集列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回数据集列表，但数量受 `limit` 查询参数。

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## 限制显示的属性

即使过滤使用 `limit` 参数，则返回的对象本身通常可能包含超出您实际需要的更多信息。 为了进一步减少系统负载，最好筛选响应以仅包含您需要的属性。

的 `properties` 参数筛选响应对象，以仅返回一组指定的属性。 参数可设置为返回一个或多个属性。

的 `properties` 参数仅接受顶级对象属性，这意味着对于以下示例对象，您可以对 `name`, `description`和 `subItem`，但不是 `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**API格式**

```http
GET /{OBJECT_TYPE}?properties={PROPERTY}
GET /{OBJECT_TYPE}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要检索的对象。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | 要包含在响应正文中的属性的名称。 |
| `{OBJECT_ID}` | 特定 [!DNL Catalog] 对象。 |

**请求**

以下请求会检索数据集列表。 以逗号分隔的属性名称列表，其中位于 `properties` 参数指示响应中要返回的属性。 A `limit` 参数，该参数可限制返回的数据集数量。 如果请求不包含 `limit` 参数，则响应最多包含20个对象。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回 [!DNL Catalog] 只显示请求属性的对象。

```json
{
    "Dataset1": {
        "name": "Dataset 1",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/bc82c518380478b59a95c63e0f843121",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "Dataset2": {},
    "Dataset3": {
        "name": {},
    },
    "Dataset4": {
        "name": "Dataset 4",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

根据上述响应，可推断出以下情况：

* 如果对象缺少任何请求的属性，则它将仅显示它包含的请求属性。(`Dataset1`)
* 如果对象不包含任何请求的属性，则它将显示为空对象。(`Dataset2`)
* 如果数据集包含属性但没有值，则它可能会将请求的属性返回为空对象。(`Dataset3`)
* 否则，数据集将显示所有请求属性的完整值。(`Dataset4`)

>[!NOTE]
>
>在 `schemaRef` 属性，版本号表示架构的最新次要版本。 请参阅 [模式版本控制](../../xdm/api/getting-started.md#versioning) ，以了解更多信息。

## 响应列表的偏移起始索引

的 `start` 查询参数使用从零开始的编号，将响应列表向前偏移指定的编号。 例如， `start=2` 将偏移响应以在第三个列出的对象上开始。

如果 `start` 参数与 `limit` 参数，则返回的对象数上限为20。

**API格式**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索的目录对象的类型。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | 一个整数，表示要偏移响应的对象数。 |

**请求**

以下请求检索数据集列表，并偏移到第五个对象(`start=4`)和将响应限制为两个返回的数据集(`limit=2`)。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应包含一个JSON对象，其中包含两个顶级项目(`limit=2`)，则每个数据集及其详细信息均对应一个（示例中已压缩了详细信息）。 响应被移四(`start=4`)，这意味着显示的数据集按时间顺序排列为5和6。

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## 按标记过滤

某些目录对象支持使用 `tags` 属性。 标记可以将信息附加到某个对象，然后稍后用于检索该对象。 要使用的标记以及如何应用这些标记的选择取决于您的组织流程。

使用标记时需要考虑以下一些限制：

* 当前支持标记的目录对象只有数据集、批次和连接。
* 标记名称对您的IMS组织是唯一的。
* Adobe流程可能会对某些行为使用标记。 这些标记的名称以“adobe”作为标准前缀。 因此，在声明标记名称时，应避免出现此约定。
* 以下标记名称是保留的，供在 [!DNL Experience Platform]，因此无法声明为贵组织的标记名称：
   * `unifiedProfile`:此标记名称是为要摄取的数据集保留的 [[!DNL Real-Time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`:此标记名称是为要摄取的数据集保留的 [[!DNL Identity Service]](../../identity-service/home.md).

以下是包含 `tags` 属性。 该属性中的标记采用键值对的形式，每个标记值都显示为包含单个字符串的数组：

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{ORG_ID}",
        "tags": {
            "sampleTag": [
                "123456"
            ],
            "secondTag": [
                "sample_tag_value"
            ]
        },
        "name": "Sample Dataset",
        "description": "Same dataset containing sample data.",
        "dule": {
            "identity": [
                "I1"
            ]
        },
        "statsCache": {},
        "state": "DRAFT",
        "lastBatchId": "ca12b29612bf4052872edad59573703c",
        "lastBatchStatus": "success",
        "lastSuccessfulBatch": "ca12b29612bf4052872edad59573703c",
        "namespace": "{NAMESPACE}",
        "createdUser": "{CREATED_USER}",
        "createdClient": "{CREATED_CLIENT}",
        "updatedUser": "{UPDATED_USER}",
        "version": "1.0.0",
        "created": 1541534444286,
        "updated": 1541534444286
    }
}
```

**API格式**

的值 `tags` 参数采用键值对的形式，使用格式 `{TAG_NAME}:{TAG_VALUE}`. 可以以逗号分隔列表的形式提供多个键值对。 提供多个标记时，假定为“与”关系。

参数支持通配符(`*`)。 例如，搜索字符串 `test*` 返回标记值以“test”开头的任何对象。 仅由通配符组成的搜索字符串可用于根据对象是否包含特定标记（无论其值如何）来筛选对象。

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要检索的对象。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | 要过滤的标记的名称。 |
| `{TAG_VALUE}` | 要过滤的标记的值。 支持通配符(`*`)。 |

**请求**

以下请求可检索数据集列表，并按一个具有特定值且存在第二个标记的标记进行筛选。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回包含的数据集列表 `sampleTag` 值为&quot;123456&quot;，且 `secondTag` 值。 除非另外指定限制，否则响应最多包含20个对象。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 1",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "Example tag value"
                ]
            },
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 2",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "A different tag value"
                ],
                "anotherTag": [
                    "2.0"
                ]
            },
            "dule": {},
            "statsCache": {}
    }
}
```

## 按日期范围过滤

中的某些端点 [!DNL Catalog] API具有查询参数，允许进行范围查询（大多数情况下是日期）。

**API格式**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| 参数 | 描述 |
| --- | --- |
| `{TIMESTAMP }` | 以Unix Epoch时间表示的日期时间整数。 |

**请求**

以下请求可检索在2019年4月期间创建的批次列表。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包含 [!DNL Catalog] 属于指定日期范围的对象。 除非另外指定限制，否则响应最多包含20个对象。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 1",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 2",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## 按属性排序

的 `orderBy` 查询参数允许您根据指定的属性值对响应数据进行排序（排序）。 此参数需要“direction”(`asc` 升序或 `desc` 表示降序)，后跟冒号(`:`)，然后是一个属性以对结果进行排序。 如果未指定方向，则默认方向为升序方向。

以逗号分隔的列表形式提供多个排序属性。 如果第一个排序属性生成多个对象，这些对象包含该属性的相同值，则使用第二个排序属性对这些匹配对象进行进一步排序。

例如，请考虑以下查询： `orderBy=name,desc:created`. 结果根据第一个排序属性以升序排序， `name`. 如果多个记录共享相同 `name` 属性，则这些匹配记录随后按第二个排序属性排序， `created`. 如果没有返回的记录共享相同的 `name`, `created` 属性不会影响排序。


**API格式**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索的目录对象的类型。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 要按对结果进行排序的属性的名称。 |

**请求**

以下请求会检索按其排序的数据集列表 `name` 属性。 如果有任何数据集共享相同 `name`，则这些数据集将依其 `updated` 属性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包含 [!DNL Catalog] 根据 `orderBy` 参数。 除非另外指定限制，否则响应最多包含20个对象。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "0405",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## 按属性筛选

[!DNL Catalog] 提供了两种按属性筛选的方法，有关这些方法的详情，请参阅以下各节：

* [使用简单过滤器](#using-simple-filters):按特定属性是否与特定值匹配进行筛选。
* [使用属性参数](#using-the-property-parameter):使用条件表达式根据属性存在与否，或者某个属性的值是否与其他指定值或正则表达式匹配、近似或比较来进行筛选。

### 使用简单过滤器 {#using-simple-filters}

通过简单过滤器，您可以根据特定属性值过滤响应。 简单过滤器采用 `{PROPERTY_NAME}={VALUE}`.

例如，查询 `name=exampleName` 仅返回对象 `name` 属性包含值“exampleName”。 相反，查询 `name=!exampleName` 仅返回对象 `name` 属性 **not** &quot;exampleName&quot;。

此外，简单过滤器支持查询单个属性的多个值的功能。 提供多个值后，响应会返回其属性匹配的对象 **any** 的值。 您可以通过预装 `!` 字符添加到列表，仅返回其属性值为 **not** (例如， `name=!exampleName,anotherName`)。

**API格式**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要检索的对象。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 要过滤其值的属性的名称。 |
| `{VALUE}` | 一个属性值，用于确定要包含（或排除，具体取决于查询）的结果。 |

**请求**

以下请求会检索数据集列表，这些数据集经过筛选后仅包含其 `name` 属性的值为“exampleName”或“anotherName”。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应包含数据集列表，不包括其 `name` 为“exampleName”或“anotherName”。 除非另外指定限制，否则响应最多包含20个对象。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "exampleName",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "anotherName",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

### 使用 `property` 参数 {#using-the-property-parameter}

的 `property` 与简单过滤器相比，查询参数更灵活地用于基于属性的过滤。 除了根据属性是否具有特定值进行筛选外， `property` 参数可以使用其他比较运算符(例如“多于”(`>`)和“小于”(`<`)以及正则表达式来按属性值进行筛选。 此外，您还可以按属性是否存在进行筛选，而不考虑其值。

的 `property` 参数仅接受顶级对象属性，这意味着对于以下示例对象，您可以按属性筛选 `name`, `description`和 `subItem`，但不是 `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**API格式**

```http
GET /{OBJECT_TYPE}?property={CONDITION}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要检索的对象。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | 一个条件表达式，指示要查询的属性以及如何计算其值。 示例如下所示。 |

的值 `property` 参数支持多种不同类型的条件表达式。 下表概述了支持表达式的基本语法：

| 符号 | 描述 | 示例 |
| --- | --- | --- |
| (None) | 声明没有运算符的属性名称只会返回存在属性的对象，而不考虑其值。 | `property=name` |
| ! | 为“`!`&quot;到 `property` 参数仅返回属性所执行的对象 **not** 存在。 | `property=!name` |
| ~ | 仅返回其属性值（字符串）与在标题(`~`)符号。 | `property=name~^example` |
| == | 仅返回其属性值与双等号(`==`)。 | `property=name==exampleName` |
| != | 仅返回属性值为的对象 **not** 匹配在not-equals符号(`!=`)。 | `property=name!=exampleName` |
| &lt; | 仅返回其属性值小于（但不等于）规定金额的对象。 | `property=version<1.0.0` |
| &lt;= | 仅返回其属性值小于（或等于）规定金额的对象。 | `property=version<=1.0.0` |
| > | 仅返回其属性值大于（但不等于）规定金额的对象。 | `property=version>1.0.0` |
| >= | 仅返回属性值大于（或等于）规定金额的对象。 | `property=version>=1.0.0` |

>[!NOTE]
>
>的 `name` 属性支持使用通配符 `*`，作为整个搜索字符串或作为其一部分。 通配符匹配空字符，以便搜索字符串 `te*st` 将匹配值“test”。 将星号加倍(`**`)。 搜索字符串中的双星号表示作为文字字符串的单个星号。

**请求**

以下请求将返回版本号大于1.0.3的任何数据集。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包含版本号大于1.0.3的数据集列表。除非还指定了限制，否则响应最多包含20个对象。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{ORG_ID}",
            "name": "sampleDataset",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.6",
            "imsOrg": "{ORG_ID}",
            "name": "exampleDataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.4",
            "imsOrg": "{ORG_ID}",
            "name": "anotherDataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## 合并多个过滤器

使用与号(`&`)，则可以在一个请求中组合使用多个过滤器。 向请求添加附加条件时，会采用“与”关系。

**API格式**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
