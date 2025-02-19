---
keywords: Experience Platform；主页；热门主题；过滤器；过滤器；过滤器数据；过滤器数据；日期范围
solution: Experience Platform
title: 使用查询参数筛选目录数据
description: 使用查询参数筛选目录服务API中的响应数据，并仅检索您需要的信息。 将过滤器应用于API调用可减少负载并提高性能，确保更快、更高效地检索数据。
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 14ecb971af3f6cdcc605caa05ef6609ecb9b38fd
workflow-type: tm+mt
source-wordcount: '2339'
ht-degree: 1%

---

# 使用查询参数筛选[!DNL Catalog]数据

若要提高性能并检索相关结果，请使用查询参数筛选[!DNL Catalog Service] API响应数据。

了解API中[!DNL Catalog]对象的常用筛选方法。 有关API交互的更多详细信息，请将此文档与[Catalog Developer Guide](getting-started.md)一起使用。 有关[!DNL Catalog Service]的一般信息，请参阅[[!DNL Catalog] 概述](../home.md)。

## 限制返回的对象 {#limit-returned-objects}

`limit`查询参数限制响应中返回的对象数。 [!DNL Catalog]响应遵循预定义的限制：

* 如果未指定`limit`参数，则每个响应的最大对象数为20。
* 对于数据集查询，如果使用`properties`查询参数请求`observableSchema`，则返回的最大数据集数为20。
* 对于用户令牌，最大限制为1。
* 对于服务令牌，最大限制为20。
* 其他目录查询的全局限制为100个对象。
* 无效的`limit`值（包括`limit=0`）导致指定了正确范围的400级错误响应。
* 作为查询参数传递的限制或偏移优先于标头中的限制或偏移。

**API格式**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索的[!DNL Catalog]对象的类型。 有效对象： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{LIMIT}` | 一个整数，指定要返回的对象数（范围： 1-100）。 |

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

成功的响应返回数据集列表，该列表限制为`limit`查询参数指示的数量。

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## 限制显示的属性 {#limit-displayed-properties}

即使使用`limit`参数过滤返回的对象数，返回的对象本身通常也可能包含比您实际需要更多的信息。 要进一步降低系统上的负载，最佳实践是筛选响应以仅包含所需的属性。

`properties`参数筛选响应对象，以仅返回一组指定的属性。 可将参数设置为返回一个或多个属性。

`properties`参数可以接受任何级别对象属性。 可以使用`?properties=subItem.sampleKey`提取`sampleKey`。

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
| `{OBJECT_TYPE}` | 要检索的[!DNL Catalog]对象的类型。 有效对象为： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY}` | 要包含在响应正文中的属性的名称。 |
| `{OBJECT_ID}` | 正在检索的特定[!DNL Catalog]对象的唯一标识符。 |

**请求**

以下请求检索数据集列表。 `properties`参数下提供的以逗号分隔的属性名称列表指示响应中要返回的属性。 还包含一个`limit`参数，该参数限制返回的数据集数。 如果请求不包含`limit`参数，则响应将最多包含20个对象。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回[!DNL Catalog]对象的列表，其中只显示所请求的属性。

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

根据以上响应，可以推断出以下情况：

* 如果对象缺少任何请求的属性，则它只会显示所请求的属性。(`Dataset1`)
* 如果对象不包含请求的任何属性，则将显示为空对象。(`Dataset2`)
* 如果某个数据集包含所请求的属性但没有值，则该数据集可能会将该属性作为空对象返回。(`Dataset3`)
* 否则，数据集将显示所有请求属性的完整值。(`Dataset4`)

>[!NOTE]
>
>在每个数据集的`schemaRef`属性中，版本号表示架构的最新次版本。 有关详细信息，请参阅XDM API指南中有关[架构版本控制](../../xdm/api/getting-started.md#versioning)的部分。

## 响应列表的偏移起始索引 {#offset-starting-index}

`start`查询参数使用从零开始的编号，将响应列表向前偏移指定的编号。 例如，`start=2`将偏移响应以在列出的第三个对象上开始。

如果`start`参数未与`limit`参数配对，则返回的最大对象数为20。

**API格式**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索的目录对象的类型。 有效对象为： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
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

响应包括一个JSON对象，该对象包含两个顶级项(`limit=2`)，每个数据集各一个，且其详细信息（示例中已经压缩了详细信息）。 响应偏移了四(`start=4`)，这意味着所显示的数据集按时间顺序排在第5和第6位。

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## 按标记筛选

某些目录对象支持使用`tags`属性。 标记可以将信息附加到对象，然后稍后用于检索该对象。 要使用的标记以及如何应用这些标记取决于您的组织流程。

使用标记时，需要考虑一些限制：

* 当前支持标记的目录对象只有数据集、批次和连接。
* 标记名称对您的组织是唯一的。
* Adobe流程可能会针对特定行为使用标记。 这些标记的名称以“adobe”为标准前缀。 因此，在声明标记名称时，应避免使用此约定。
* 以下标记名称是保留名称，以供在[!DNL Experience Platform]中使用，因此不能声明为您的组织的标记名称：
   * `unifiedProfile`：此标记名称是为要由[[!DNL Real-Time Customer Profile]](../../profile/home.md)引入的数据集而保留的。
   * `unifiedIdentity`：此标记名称是为要由[[!DNL Identity Service]](../../identity-service/home.md)引入的数据集而保留的。

以下是包含`tags`属性的数据集示例。 该属性中的标记采用键值对的形式，每个标记值都显示为包含单个字符串的数组：

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

`tags`参数的值采用键值对的形式，格式为`{TAG_NAME}:{TAG_VALUE}`。 可以以逗号分隔列表的形式提供多个键值对。 如果提供了多个标记，则假定为AND关系。

参数支持标记值的通配符(`*`)。 例如，搜索字符串`test*`返回标记值以“test”开头的任何对象。 仅由通配符组成的搜索字符串可用于根据对象是否包含特定标记对其进行过滤，而不管其值如何。

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索的[!DNL Catalog]对象的类型。 有效对象为： <ul><li>`batches`</li><li>`dataSets`</li></ul> |
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

成功的响应返回了一个数据集列表，该列表包含值为“123456”的`sampleTag`和任意值的`secondTag`。 除非也指定了限制，否则响应最多包含20个对象。

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

## 按日期范围过滤

[!DNL Catalog] API中的某些端点具有允许范围查询的查询参数，最常见的是日期查询。

**API格式**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| 参数 | 描述 |
| --- | --- |
| `{TIMESTAMP }` | 以Unix纪元时间表示的日期时间整数。 |

**请求**

以下请求会检索在2019年4月期间创建的批次列表。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包含指定日期范围内的[!DNL Catalog]对象列表。 除非也指定了限制，否则响应最多包含20个对象。

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

`orderBy`查询参数允许您根据指定的属性值对响应数据排序（排序）。 此参数需要一个“方向”（`asc`表示升序，`desc`表示降序），后跟一个冒号(`:`)，然后是一个属性以对结果排序。 如果未指定方向，则默认方向为升序。

可以以逗号分隔列表的形式提供多个排序属性。 如果第一个排序属性生成的多个对象包含该属性的相同值，则第二个排序属性用于进一步排序这些匹配的对象。

例如，请考虑以下查询： `orderBy=name,desc:created`。 结果根据第一个排序属性`name`按升序排序。 如果多个记录共享同一`name`属性，则这些匹配的记录将按第二个排序属性`created`排序。 如果没有返回的记录共享同一`name`，则`created`属性不会考虑排序的因素。


**API格式**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索的目录对象的类型。 有效对象为： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | 要作为结果排序依据的属性的名称。 |

**请求**

以下请求检索按其`name`属性排序的数据集列表。 如果任何数据集共享相同的`name`，则这些数据集将依次按其`updated`属性降序排序。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包含根据`orderBy`参数排序的[!DNL Catalog]对象的列表。 除非也指定了限制，否则响应最多包含20个对象。

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

[!DNL Catalog]提供了两种按属性进行筛选的方法，下面几节将对这些方法作进一步概述：

* [使用简单筛选器](#using-simple-filters)：按特定属性是否与特定值匹配进行筛选。
* [使用属性参数](#using-the-property-parameter)：使用条件表达式根据属性是否存在，或者属性的值是否匹配、近似或与其他指定值或正则表达式比较来进行筛选。

>[!NOTE]
>
>目录对象的任何属性都可用于在目录服务API中筛选结果。

### 使用简单过滤器 {#using-simple-filters}

使用简单过滤器，可根据特定的属性值过滤响应。 简单筛选器采用`{PROPERTY_NAME}={VALUE}`形式。

例如，查询`name=exampleName`只返回`name`属性包含“exampleName”值的对象。 相反，查询`name=!exampleName`只返回`name`属性为&#x200B;**而非**“exampleName”的对象。

此外，简单过滤器支持查询单个属性的多个值。 提供多个值时，响应将返回其属性与所提供列表中的值&#x200B;**any**&#x200B;匹配的对象。 您可以通过在列表中添加前缀`!`字符来反转多值查询，在提供的列表中（例如，`name=!exampleName,anotherName`）仅返回属性值是&#x200B;**而不是**&#x200B;的对象。

**API格式**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索的[!DNL Catalog]对象的类型。 有效对象为： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | 要按其值进行过滤的属性的名称。 |
| `{VALUE}` | 一个属性值，可确定要包括（或排除，具体取决于查询）的结果。 |

**请求**

以下请求检索经过筛选的数据集列表，以仅包含其`name`属性值为“exampleName”或“anotherName”的数据集。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包含数据集列表，不包括`name`为“exampleName”或“anotherName”的任何数据集。 除非也指定了限制，否则响应最多包含20个对象。

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

### 使用`property`参数 {#using-the-property-parameter}

`property`查询参数为基于属性的筛选提供了比简单筛选更大的灵活性。 除了根据属性是否具有特定值进行筛选之外，`property`参数还可以使用其他比较运算符(如“大于”(`>`)和“小于”(`<`))以及正则表达式来按属性值筛选。 它还可以按属性是否存在进行筛选，而不管其值如何。

使用&amp;符号(`&`)组合多个筛选器并在单个请求中优化查询。 当按多个字段过滤时，默认情况下应用`AND`关系。

>[!NOTE]
>
>如果在单个查询中合并多个`property`参数，则必须至少将一个参数应用于`id`或`created`字段。 以下查询返回`id`为`abc123` **且** `name`不是`test`的对象：
>
>```http
>GET /datasets?property=id==abc123&property=name!=test
>```

如果对同一字段使用多个`property`参数，则只有最后指定的参数生效。

>[!IMPORTANT]
>
>您&#x200B;**不能**&#x200B;使用单个`property`参数同时筛选多个字段。 每个字段必须具有自己的`property`参数。 以下示例(`property=id>abc,name==myDataset`)是&#x200B;**不允许**&#x200B;的，因为它尝试在&#x200B;**单个`property`参数**&#x200B;中向`id`和`name`应用条件。

`property`参数可以接受任何级别对象属性。 `sampleKey`可用于使用`?properties=subItem.sampleKey`进行筛选。

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
| `{OBJECT_TYPE}` | 要检索的[!DNL Catalog]对象的类型。 有效对象为： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{CONDITION}` | 一个条件表达式，指明要查询的属性及其值的计算方式。 下面提供了示例。 |

`property`参数的值支持多种不同类型的条件表达式。 下表概述了支持的表达式的基本语法：

| 符号 | 描述 | 示例 |
| --- | --- | --- |
| （无） | 在属性名称中声明no运算符将只返回存在该属性的对象，而不管其值是什么。 | `property=name` |
| ！ | 将“`!`”前缀为`property`参数的值将只返回属性&#x200B;**不**&#x200B;存在的对象。 | `property=!name` |
| ~ | 仅返回属性值（字符串）与波状符(`~`)后面提供的正则表达式匹配的对象。 | `property=name~^example` |
| == | 仅返回其属性值完全匹配双等号(`==`)后提供的字符串的对象。 | `property=name==exampleName` |
| ！= | 仅返回其属性值不为&#x200B;**不为**&#x200B;且与非等号符号(`!=`)后提供的字符串匹配的对象。 | `property=name!=exampleName` |
| &lt; | 仅返回属性值小于（但不等于）规定数量的对象。 | `property=version<1.0.0` |
| &lt;= | 仅返回属性值小于（或等于）规定数量的对象。 | `property=version<=1.0.0` |
| > | 仅返回属性值大于（但不等于）规定数量的对象。 | `property=version>1.0.0` |
| >= | 仅返回属性值大于（或等于）规定数量的对象。 | `property=version>=1.0.0` |
| * | 通配符适用于任何字符串属性，并匹配任意字符序列。 使用`**`对文字星号进行转义。 | `property=name==te*st` |
| 和 | 将多个`property`参数与它们之间的`AND`关系组合在一起。 | `property=id==abc&property=name!=test` |

>[!NOTE]
>
>`name`属性支持将通配符`*`用作整个搜索字符串或作为其一部分。 通配符匹配空字符，因此搜索字符串`te*st`将匹配值“test”。 将星号加倍(`**`)可避免星号。 搜索字符串中的双星号表示一个星号作为文本字符串。

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

成功的响应包含版本号大于1.0.3的数据集列表。除非也指定了限制，否则响应最多包含20个对象。

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

## 使用属性参数筛选数组 {#filter-arrays}

根据数组属性过滤结果时，使用相等和不等运算符可包含或排除特定值。

### 等式过滤器 {#equality-filters}

要按多个值过滤数组字段，请为每个值使用单独的属性参数。 使用相等过滤器仅返回数组数据中匹配指定值的条目。

>[!NOTE]
>
>在筛选多个字段时要求包括`id`或`created`在筛选数组字段中的多个值时&#x200B;**不**&#x200B;适用。

下面的示例查询只返回数组中同时包含`val1`和`val2`的结果。

**API格式**

```http
GET /{OBJECT_TYPE}?property=arrayField=val1&property=arrayField=val2
```

### 不等式过滤器 {#inequality-filters}

对数组字段使用不等式运算符(`!=`)以排除数组中包含指定值的数据中的任何条目。

**API格式**

```http
GET /{OBJECT_TYPE}?property=arrayField!=val1&property=arrayField!=val2
```

此查询返回arrayField不包含`val1`或`val2`的文档。

### 等式和不等式筛选器限制 {#equality-inequality-limitations}

不能在单个查询中将等式(`=`)和不等式(`!=`)同时应用于同一字段。
