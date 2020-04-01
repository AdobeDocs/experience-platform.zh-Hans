---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用查询参数过滤目录数据
topic: developer guide
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 使用查询参数过滤目录数据

Catalog Service API允许通过使用请求查询参数筛选响应数据。 Catalog的最佳实践之一是在所有API调用中使用过滤器，因为这些调用可减少API的负载并有助于提高整体性能。

本文档概述了在API中筛选Catalog对象的最常用方法。 建议您在阅读目录开发人员指南时引用此文档 [](getting-started.md) ，以进一步了解如何与目录API交互。 有关目录服务的更多常规信息，请参阅 [目录概述](../home.md)。

## 限制返回的对象

查询 `limit` 参数限制在响应中返回的对象数。 目录响应会根据配置的限制自动按量收费：

* 如果未 `limit` 指定参数，则每个响应有效负荷的最大对象数为20。
* 对于数据集查询，如 `observableSchema` 果使用查询参数请求， `properties` 则返回的最大数据集数为20。
* 所有其他目录查询的全局限制为100个对象。
* 无效 `limit` 的参数(包 `limit=0`括)会导致400级错误响应，这些错误响应描绘了适当的范围。
* 作为查询参数传递的限制或偏移优先于作为标题传递的限制或偏移。

**API格式**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索的Catalog对象的类型。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | 一个整数，表示要返回的对象数，范围从1到100。 |

**请求**

以下请求检索数据集的列表，同时限制对三个对象的响应。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回数据集列表，但仅限于查询参数指示的 `limit` 数量。

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

即使过滤使用该参数返回的对象数 `limit` 量，返回的对象本身也可能包含超出您实际需要的更多信息。 要进一步减少系统上的负载，最好过滤响应以仅包含所需的属性。

该参 `properties` 数过滤器响应对象以仅返回一组指定的属性。 该参数可以设置为返回一个或多个属性。

该参 `properties` 数仅接受顶级对象属性，这意味着对于以下示例对象，您可以对 `name`、 `description`和(但不 `subItem`对)应用过滤器 `sampleKey`。

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
| `{OBJECT_TYPE}` | 要检索的Catalog对象的类型。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | 要包含在响应主体中的属性的名称。 |
| `{OBJECT_ID}` | 要检索的特定Catalog对象的唯一标识符。 |

**请求**

以下请求检索数据集的列表。 在参数下提供的属性名称的逗号分隔列表 `properties` 表示要在响应中返回的属性。 还包 `limit` 含一个参数，该参数会限制返回的数据集数。 如果请求中不包含参 `limit` 数，则响应最多将包含20个对象。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回一列表目录对象，只显示所请求的属性。

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

根据上述响应，可推断出以下内容：

* 如果某个对象缺少任何请求的属性，则它将仅显示它包含的请求的属性。(`Dataset1`)
* 如果某个对象不包含任何请求的属性，则该对象将显示为空对象。(`Dataset2`)
* 如果数据集包含属性但没有值，则它可能将请求的属性返回为空对象。(`Dataset3`)
* 否则，数据集将显示所有请求的属性的完整值。(`Dataset4`)

## 响应列表的偏移起始索引

查询 `start` 参数使用从零开始的编号将响应列表向前偏移指定的数字。 例如，将 `start=2` 偏移对第三个列出对象上的开始的响应。

如果参 `start` 数未与参数配对，则返回的 `limit` 对象的最大数量为20。

**API格式**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索的Catalog对象的类型。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | 一个整数，它表示要将响应偏移的对象数。 |

**请求**

以下请求检索数据集的列表，偏移到第五个对象(`start=4`)并限制对两个返回的数据集(`limit=2`)的响应。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应包括一个JSON对象，其中包含两个顶级项目(`limit=2`)，每个数据集的一个项目及其详细信息（在示例中已压缩了详细信息）。 响应被移动了四(`start=4`)个，这意味着显示的数据集按时间顺序排列在第五和第六位。

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## 按标签过滤

某些Catalog对象支持使用属 `tags` 性。 标记可以向对象附加信息，然后稍后用于检索该对象。 要使用哪些标记以及如何应用这些标记的选择取决于您的组织流程。

使用标记时需要考虑以下几个限制：

* 当前支持标记的唯一Catalog对象是数据集、批次和连接。
* 标记名称对于IMS组织是唯一的。
* Adobe流程可能会利用某些行为的标签。 这些标记的名称前缀有“adobe”作为标准。 因此，在声明标记名称时应避免此约定。
* 以下标记名称保留为可跨Experience Platform使用，因此不能声明为贵组织的标记名称：
   * `unifiedProfile`:此标记名称保留给实时客户用户档案要摄取 [的数据集](../../profile/home.md)。
   * `unifiedIdentity`:此标记名称为由 [Identity Service摄取的数据集保留](../../identity-service/home.md)。

以下是包含属性的数据集的示 `tags` 例。 该属性中的标记采用键值对的形式，每个标记值显示为一个包含单个字符串的数组：

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{IMS_ORG}",
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

参数的 `tags` 值采用键值对的形式，格式为 `{TAG_NAME}:{TAG_VALUE}`。 可以以逗号分隔的列表形式提供多个键值对。 当提供多个标记时，假定AND关系。

该参数支持标记值的通`*`配符()。 例如，搜索字符串 `test*` 返回标签值以“test”开头的任何对象。 仅包含通配符的搜索字符串可用于根据对象是否包含特定标记（无论其值如何）过滤对象。

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索的Catalog对象的类型。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | 要筛选的标记的名称。 |
| `{TAG_VALUE}` | 要筛选的标记的值。 支持通配符(`*`)。 |

**请求**

以下请求检索数据集的列表，由具有特定值的一个标签过滤，并且存在第二标签。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回包含值为“123456” `sampleTag` 的数据集的列表，且该数据集包含值为“123456”的AND `secondTag` 值为任何值。 除非还指定了限制，否则响应最多包含20个对象。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

## 按日期范围筛选

目录API中的某些端点具有查询参数，这些参数允许按范围进行查询，在日期情况下最为常见。

**API格式**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| 参数 | 描述 |
| --- | --- |
| `{TIMESTAMP }` | Unix Epoch时间中的日期时间整数。 |

**请求**

以下请求检索在2019年4月创建的批列表。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包含一列表在指定日期范围内的Catalog对象。 除非还指定了限制，否则响应最多包含20个对象。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

查询 `orderBy` 参数允许您根据指定的属性值对响应数据进行排序（排序）。 此参数需要一个“direction”(`asc` for asching or `desc` descending)，后跟一个冒号(`:`)，然后是一个属性以对结果进行排序。 如果未指定方向，则默认方向为升序。

可以以逗号分隔的列表提供多个排序属性。 如果第一个排序属性生成的多个对象包含该属性的相同值，则第二个排序属性随后用于对这些匹配的对象进行进一步排序。

例如，请考虑以下查询: `orderBy=name,desc:created`. 根据第一个排序属性，结果按升序排序 `name`。 如果多个记录共享相同的属 `name` 性，则这些匹配记录随后按第二个排序属性排序 `created`。 如果没有返回的记录共享相同 `name`内容， `created` 则属性不会影响排序。


**API格式**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索的Catalog对象的类型。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 要按结果排序的属性的名称。 |

**请求**

以下请求检索按其属性排序的数据集的列表 `name` 信息。 如果任何数据集共享 `name`相同，则这些数据集依次按其属性按降序 `updated` 排列。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包含一列表Catalog对象，这些对象根据参数进行排序 `orderBy` 。 除非还指定了限制，否则响应最多包含20个对象。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

## 按属性过滤

Catalog提供了两种按属性筛选的方法，下面各节进一步介绍了这些方法：

* [使用简单的过滤器](#using-simple-filters):通过特定属性是否与特定值匹配进行筛选。
* [使用属性参数](#using-the-property-parameter):使用条件表达式根据属性是否存在，或者某个属性的值是否与其他指定值或常规表达式匹配、近似或比较来进行筛选。

### 使用简单的过滤器 {#using-simple-filters}

简单过滤器允许您根据特定属性值筛选响应。 简单的过滤器采用以下形式 `{PROPERTY_NAME}={VALUE}`。

例如，查询只返 `name=exampleName` 回其属性包 `name` 含值为“exampleName”的对象。 相反，查询只 `name=!exampleName` 返回属性不为“exampleName `name` ”的 **对** 象。

此外，简单过滤器支持查询单个属性的多个值的能力。 当提供多个值时，响应返回其属性与所提供列表 **中的任** 何值相匹配的对象。 通过将字符预定在查询中，可 `!` 以反转多值列表，只返回属性值不在提供的列表中的 **** (例如， `name=!exampleName,anotherName`)对象。

**API格式**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索的Catalog对象的类型。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 要筛选其值的属性的名称。 |
| `{VALUE}` | 一个属性值，它确定要包括(或排除，具体取决于查询)的结果。 |

**请求**

以下请求检索数据集的列表，筛选为仅包含其属性值为“exampleName”或“anotherName”的 `name` 数据集。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包含一列表数据集，不包括任何以“exampleName”或“ `name` anotherName”为单位的数据集。 除非还指定了限制，否则响应最多包含20个对象。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

### 使用参 `property` 数 {#using-the-property-parameter}

与简单 `property` 的查询相比，过滤器参数为基于属性的过滤提供了更大的灵活性。 除了基于某个属性是否具有特定值进行筛选外，该参数还可以使用其他比较运算符(如“more-than”( `property` )和“less-than”(`>``<`))以及常规表达式按属性值进行筛选。 它还可以按属性是否存在进行筛选，而不管其值如何。

该参 `property` 数只接受顶级对象属性，这意味着对于以下示例对象，您可以按属性筛选 `name`、 `description`和，但 `subItem`不能筛选 `sampleKey`。

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
| `{OBJECT_TYPE}` | 要检索的Catalog对象的类型。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | 一个条件表达式，它指示要查询的属性以及如何评估其值。 示例如下。 |

该参数的值支 `property` 持几种不同的条件表达式。 下表概述了支持的表达式的基本语法：

| 符号 | 描述 | 示例 |
| --- | --- | --- |
| (无) | 声明不带运算符的属性名称将只返回属性所在的对象，而不管其值如何。 | `property=name` |
| ! | 将“`!`”前缀为参数值 `property` 将只返回属性不存在的 **对象** 。 | `property=!name` |
| ~ | 仅返回其属性值（字符串）与在代字符()符号后提供的常规表达式相匹配`~`的对象。 | `property=name~^example` |
| == | 仅返回其属性值与在等于多次符号(`==`)后提供的字符串完全匹配的对象。 | `property=name==exampleName` |
| != | 仅返回其属性值与 **Not** -equals符号(`!=`)后提供的字符串不匹配的对象。 | `property=name!=exampleName` |
| &lt; | 仅返回其属性值小于（但不等于）规定金额的对象。 | `property=version<1.0.0` |
| &lt;= | 仅返回其属性值小于（或等于）规定金额的对象。 | `property=version<=1.0.0` |
| > | 仅返回其属性值大于（但不等于）规定金额的对象。 | `property=version>1.0.0` |
| >= | 仅返回其属性值大于（或等于）规定金额的对象。 | `property=version>=1.0.0` |

>[!NOTE] 该 `name` 属性支持使用通配符( `*`作为整个搜索字符串或通配符的一部分)。 通配符匹配空字符，这样搜索字符串 `te*st` 将匹配值“test”。 将星号加倍(`**`)，即可转义星号。 搜索字符串中的多次星号表示单个星号作为文本字符串。

**请求**

以下请求将返回版本号大于1.0.3的任何数据集。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包含版本号大于1.0.3的数据集列表。除非还指定了限制，否则响应最多包含20个对象。

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

使用“和号”(`&`)，您可以将多个过滤器组合到一个请求中。 当向请求添加附加条件时，将假定AND关系。

**API格式**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
