---
keywords: Experience Platform；主页；热门主题；过滤器；过滤器；过滤器数据；过滤器数据；日期范围
solution: Experience Platform
title: 使用查询参数筛选目录数据
description: 目录服务API允许通过使用请求查询参数筛选响应数据。 Catalog的部分最佳实践是在所有API调用中使用过滤器，因为它们可减少API的负载并帮助提高整体性能。
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 24db94b959d1bad925af1e8e9cbd49f20d9a46dc
workflow-type: tm+mt
source-wordcount: '2099'
ht-degree: 1%

---

# 筛选条件 [!DNL Catalog] 使用查询参数的数据

此 [!DNL Catalog Service] API允许通过使用请求查询参数筛选响应数据。 最佳做法的一部分 [!DNL Catalog] 是在所有API调用中使用过滤器，因为它们会减轻API的负载并帮助提高整体性能。

本文档概述了最常见的筛选方法 [!DNL Catalog] API中的对象。 建议您在阅读 [目录开发人员指南](getting-started.md) 以详细了解如何与 [!DNL Catalog] API。 有关以下内容的更多常规信息： [!DNL Catalog Service]，请参见 [[!DNL Catalog] 概述](../home.md).

## 限制返回的对象

此 `limit` query参数限制响应中返回的对象数。 [!DNL Catalog] 将根据配置的限制自动计量响应：

* 如果 `limit` 未指定参数，每个响应有效负载的最大对象数为20。
* 对于数据集查询，如果 `observableSchema` 是使用 `properties` 查询参数中返回的最大数据集数为20。
* 所有其他目录查询的全局限制为100个对象。
* 无效 `limit` 参数(包括 `limit=0`)会生成概述正确范围的400级错误响应。
* 作为查询参数传递的限制或偏移优先于作为标头传递的限制或偏移。

**API格式**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要检索的对象。 有效对象包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | 一个整数，表示要返回的对象的数量，从1到100不等。 |

**请求**

以下请求检索数据集列表，同时将响应限制为三个对象。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应将返回数据集列表，该列表以 `limit` 查询参数。

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

即使使用过滤返回的对象数 `limit` 参数，则返回的对象本身通常可以包含比您实际需要更多的信息。 为了进一步降低系统负载，最佳实践是筛选响应以仅包含您需要的属性。

此 `properties` 参数筛选响应对象，以仅返回一组指定的属性。 可将参数设置为返回一个或多个属性。

此 `properties` 参数可以接受任何级别对象属性。 `sampleKey` 可以使用提取 `?properties=subItem.sampleKey`.

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
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要检索的对象。 有效对象包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | 要包含在响应正文中的属性的名称。 |
| `{OBJECT_ID}` | 特定对象的唯一标识符 [!DNL Catalog] 正在检索的对象。 |

**请求**

以下请求检索数据集列表。 下提供的以逗号分隔的属性名称列表 `properties` 参数指示响应中返回的属性。 A `limit` 参数也会被包含，从而限制返回的数据集数量。 如果请求不包含 `limit` 参数，响应最多可包含20个对象。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回一个列表，其中 [!DNL Catalog] 仅显示所请求属性的对象。

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

根据上述响应，可以推断出以下情况：

* 如果对象缺少任何请求的属性，则它只会显示所请求的属性。(`Dataset1`)
* 如果对象不包含任何请求的属性，则将显示为空对象。(`Dataset2`)
* 如果数据集包含某个属性但没有值，则该数据集可能会将请求的属性作为空对象返回。(`Dataset3`)
* 否则，数据集将显示所有请求属性的完整值。(`Dataset4`)

>[!NOTE]
>
>在 `schemaRef` 属性，版本号表示架构的最新次要版本。 请参阅以下部分： [架构版本控制](../../xdm/api/getting-started.md#versioning) 有关更多信息，请参阅XDM API指南。

## 响应列表的偏移起始索引

此 `start` 查询参数使用从零开始的编号，将响应列表向前偏移指定的编号。 例如， `start=2` 会将响应偏移到在列出的第三个对象上启动。

如果 `start` 参数未与 `limit` 参数，返回的最大对象数为20。

**API格式**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索的目录对象的类型。 有效对象包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | 一个整数，表示响应偏移的对象数。 |

**请求**

以下请求检索数据集列表，偏移到第五个对象(`start=4`)并将响应限制为两个返回的数据集(`limit=2`)。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应中包含一个包含两个顶级项(`limit=2`)，每个数据集一个及其详细信息（示例中精简了详细信息）。 响应被偏移了四次(`start=4`)，这意味着所示数据集按时间顺序排在第5和第6位。

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## 按标记筛选

某些目录对象支持使用 `tags` 属性。 标记可以将信息附加到对象，然后稍后用于检索该对象。 要使用的标记以及如何应用这些标记取决于您的组织流程。

使用标记时，需要考虑一些限制：

* 当前支持标记的目录对象只有数据集、批次和连接。
* 标记名称对您的组织是唯一的。
* Adobe过程可能会为特定行为使用标记。 这些标记的名称以“adobe”作为标准前缀。 因此，在声明标记名称时，应避免使用此约定。
* 以下标记名称是保留名称，以供跨以下标记使用 [!DNL Experience Platform]，因此不能声明为组织的标记名称：
   * `unifiedProfile`：此标记名称是为要引入的数据集而保留的 [[!DNL Real-Time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`：此标记名称是为要引入的数据集而保留的 [[!DNL Identity Service]](../../identity-service/home.md).

以下是包含 `tags` 属性。 该属性中的标记采用键值对的形式，每个标记值显示为包含单个字符串的数组：

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

的值 `tags` 参数采用键值对的形式，格式为 `{TAG_NAME}:{TAG_VALUE}`. 可以以逗号分隔列表的形式提供多个键值对。 如果提供了多个标记，则假定为AND关系。

参数支持通配符(`*`)作为标记值。 例如，搜索字符串 `test*` 返回标记值以“test”开头的任何对象。 仅由通配符组成的搜索字符串可用于根据对象是否包含特定标记来筛选对象，而不管其值如何。

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要检索的对象。 有效对象包括： <ul><li>`batches`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | 要作为筛选依据的标记的名称。 |
| `{TAG_VALUE}` | 要作为筛选依据的标记的值。 支持通配符(`*`)。 |

**请求**

以下请求检索数据集列表，按具有特定值的一个标记和存在的第二个标记进行筛选。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回包含的数据集列表 `sampleTag` 值为“123456”，并且 `secondTag` 具有任意值。 除非还指定了限制，否则响应最多包含20个对象。

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
    }
}
```

## 按日期范围筛选

中的某些端点 [!DNL Catalog] API具有允许范围查询的查询参数，最常见的是日期查询。

**API格式**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| 参数 | 描述 |
| --- | --- |
| `{TIMESTAMP }` | 以Unix纪元时间表示的日期时间整数。 |

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

成功的响应包含一个 [!DNL Catalog] 指定日期范围内的对象。 除非还指定了限制，否则响应最多包含20个对象。

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
    }
}
```

## 按属性排序

此 `orderBy` 查询参数允许您根据指定的属性值对响应数据排序（排序）。 此参数需要“direction”(`asc` 升序或 `desc` 降序)，后跟冒号(`:`)，然后是作为结果排序依据的属性。 如果未指定方向，则默认方向为升序。

可以在逗号分隔的列表中提供多个排序属性。 如果第一个排序属性生成的多个对象包含该属性的相同值，则第二个排序属性用于进一步排序这些匹配的对象。

例如，请考虑以下查询： `orderBy=name,desc:created`. 结果根据第一个排序属性按升序排序。 `name`. 当多个记录共享相同时 `name` 属性，然后按第二个排序属性对匹配的记录进行排序， `created`. 如果没有返回的记录共享相同的 `name`，则 `created` 属性未纳入排序的考虑范围。


**API格式**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索的目录对象的类型。 有效对象包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 要作为结果排序依据的属性的名称。 |

**请求**

以下请求检索按其排序的数据集列表 `name` 属性。 如果任何数据集共享相同的 `name`，则这些数据集将依次由其 `updated` 属性降序。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包含一个 [!DNL Catalog] 根据 `orderBy` 参数。 除非还指定了限制，否则响应最多包含20个对象。

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
    }
}
```

## 按属性筛选

[!DNL Catalog] 提供了两种按属性过滤的方法，下面几节将进一步概述这些方法：

* [使用简单过滤器](#using-simple-filters)：按特定属性是否与特定值匹配进行筛选。
* [使用属性参数](#using-the-property-parameter)：使用条件表达式根据某个属性是否存在，或者如果某个属性的值匹配、接近或比较另一个指定的值或正则表达式，进行筛选。

### 使用简单过滤器 {#using-simple-filters}

通过简单过滤器，可根据特定属性值过滤响应。 简单的过滤器采用以下形式 `{PROPERTY_NAME}={VALUE}`.

例如，查询 `name=exampleName` 仅返回对象 `name` 属性包含值“exampleName”。 相比之下，查询 `name=!exampleName` 仅返回对象 `name` 属性为 **非** &quot;exampleName&quot;。

此外，简单筛选器支持查询单个属性的多个值。 提供多个值时，响应将返回属性匹配的对象 **任意** 提供的列表中的值。 您可以通过为多值查询添加前缀来反转 `!` 字符，仅返回属性值为的对象 **非** (例如， `name=!exampleName,anotherName`)。

**API格式**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要检索的对象。 有效对象包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | 要按其值进行过滤的属性的名称。 |
| `{VALUE}` | 一个属性值，可确定要包括（或排除，具体取决于查询）的结果。 |

**请求**

以下请求检索数据集列表，已筛选以仅包含其数据集的 `name` 属性的值为“exampleName”或“anotherName”。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包含数据集列表，但不包括任何数据集 `name` 为“exampleName”或“anotherName”。 除非还指定了限制，否则响应最多包含20个对象。

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
    }
}
```

### 使用 `property` 参数 {#using-the-property-parameter}

此 `property` 查询参数为基于属性的筛选提供了比简单筛选更大的灵活性。 除了根据资产是否具有特定值进行筛选之外， `property` 参数可以使用其他比较运算符(例如“大于”(`>`)和“小于”(`<`)，以及要按属性值过滤的正则表达式。 它还可以按属性是否存在进行筛选，而不管其值是什么。

此 `property` 参数可以接受任何级别对象属性。 `sampleKey` 可用于筛选，使用 `?properties=subItem.sampleKey`.

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
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要检索的对象。 有效对象包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | 一个条件表达式，指明要查询的属性以及如何计算其值。 下面提供了示例。 |

的值 `property` 参数支持多种不同类型的条件表达式。 下表概述了支持的表达式的基本语法：

| 符号 | 描述 | 示例 |
| --- | --- | --- |
| (None) | 在属性名称中声明no运算符将只返回属性存在的对象，而不管其值是什么。 | `property=name` |
| ！ | 前缀“”`!`”到的值 `property` 参数仅返回属性执行的对象 **非** 存在。 | `property=!name` |
| ~ | 仅返回属性值（字符串）与波状符(`~`)符号。 | `property=name~^example` |
| == | 仅返回其属性值完全匹配双等符号(`==`)。 | `property=name==exampleName` |
| != | 仅返回属性值可执行的对象 **非** 匹配在不等于符号(`!=`)。 | `property=name!=exampleName` |
| &lt; | 仅返回属性值小于（但不等于）规定数量的对象。 | `property=version<1.0.0` |
| &lt;= | 仅返回属性值小于（或等于）规定数量的对象。 | `property=version<=1.0.0` |
| > | 仅返回属性值大于（但不等于）规定数量的对象。 | `property=version>1.0.0` |
| >= | 仅返回属性值大于（或等于）规定数量的对象。 | `property=version>=1.0.0` |

>[!NOTE]
>
>此 `name` 属性支持使用通配符 `*`，作为整个搜索字符串或作为其一部分。 通配符匹配空字符，例如搜索字符串 `te*st` 将匹配值“test”。 将星号加倍即可避免星号(`**`)。 搜索字符串中的双星号表示单个星号作为文本字符串。

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

成功响应包含版本号大于1.0.3的数据集列表。除非还指定了限制，否则响应最多包含20个对象。

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
    }
}
```

## 合并多个过滤器

使用&amp;符号(`&`)，则可以在单个请求中组合多个过滤器。 将其他条件添加到请求时，假定存在AND关系。

**API格式**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
