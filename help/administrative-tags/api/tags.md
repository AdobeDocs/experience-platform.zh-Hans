---
title: 统一标记端点
description: 了解如何使用Adobe Experience Platform API创建、更新、管理和删除标记类别和标记。
role: Developer
exl-id: 6687d1da-a5e4-435a-9f99-1b0f9ac98088
source-git-commit: 717a4ea0568200c940cf9b8f26f4dd2aa9c00a3e
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 3%

---

# 统一标记端点

>[!IMPORTANT]
>
>此终结点集的终结点URL为`https://experience.adobe.io`。

标记是一项功能，可让您管理元数据分类，以分类业务对象以便于发现和分类。 随后，您可以通过将这些标记添加到标记类别来将这些标记组织到其他组中。

本指南提供的信息可帮助您更好地了解标记和标记类别，包括用于使用API执行基本操作的示例API调用。

## 快速入门

本指南中使用的端点是Adobe Experience Platform API的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)以了解成功调用API所需了解的重要信息，包括所需的标头以及如何读取示例API调用

### 术语表

以下术语表突出显示&#x200B;**标记**&#x200B;和&#x200B;**标记类别**&#x200B;之间的区别。

- **标记**：标记允许您管理业务对象的元数据分类，从而允许您对这些对象进行分类，以便于发现和分类。
   - **未分类的标记**：未分类的标记是不属于标记类别的标记。 默认情况下，创建的标记将取消分类。
- **标记类别**：标记类别允许您将标记分组为有意义的集，从而提供更多有关标记目的的上下文。

## 检索标记类别的列表 {#get-tag-categories}

您可以通过向`/tagCategory`端点发出GET请求来检索属于您组织的标记类别的列表。

**API格式**

```http
GET /tagCategory
GET /tagCategory?{QUERY_PARAMETERS}
```

检索标记类别时，可以使用以下可选查询参数。

| 查询参数 | 描述 | 示例 |
| --------------- | ----------- | ------- |
| `start` | 结果列表的开始位置。 您可以使用此项来指示结果分页的起始索引。 | `start=a` |
| `limit` | 每页检索的最大标记类别数。 | `limit=20` |
| `property` | 检索标记类别时要过滤的属性。 支持的值包括： &lt;ul≥<li>`name`：标记类别的名称。</li></ul> | `property=name==category` |
| `sortBy` | 标记类别的排序顺序。 支持的值包括`name`、`createdAt`和`modifiedAt`。 | `sortBy=name` |
| `sortOrder` | 标记类别排序的方向。 支持的值包括`asc`和`desc`。 | `sortOrder=asc` |

**请求**

+++列出组织中所有标记类别的示例请求

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**响应**

成功的响应会返回HTTP状态200，其中包含贵组织所有标记类别的列表。

+++包含组织中所有标记类别列表的示例响应。

```json
{
    "_page": {
        "count": 1,
        "limit": 10,
        "property": []
    },
    "tags": [
        {
            "id": "e2b7c656-067b-4413-a366-adde0401df50",
            "name": "Test Category",
            "description": "A sample description for the test tag category.",
            "org": "{ORG_ID}",
            "createdBy": "{USER_ID}",
            "createdAt": "1661752268000",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "1661752268000",
            "tagCount": 0
        }
    ]
}
```

+++

## 创建新标记类别 {#create-tag-category}

>[!IMPORTANT]
>
>只有系统管理员和产品管理员可以使用此API调用。

您可以通过向`/tagCategory`端点发出POST请求来创建新的标记类别。

**API格式**

```http
POST /tagCategory
```

**请求**

+++用于创建新标记类别的示例请求。

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "Sample Test Category",
    "description": "Sample test category"
 }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 要创建的标记类别的名称。 |
| `description` | 要创建的标记类别的描述。 |

+++

**响应**

示例响应返回HTTP状态200以及新创建的标记类别的详细信息。

+++包含新创建标记类别详细信息的示例响应。

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Sample Test Category",
    "description": "Sample test category",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## 检索特定标记类别 {#get-tag-category}

您可以通过向`/tagCategory`端点发出GET请求并指定标记类别的ID来检索属于您组织的特定标记类别。

**API格式**

```http
GET /tagCategory/{TAG_CATEGORY_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | 正在检索的标记类别的ID。 |

**请求**

+++检索特定标记类别的示例请求

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**响应**

成功的响应返回HTTP状态200以及指定标记类别的详细信息。

+++包含指定标记类别详细信息的示例响应。

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "A sample description for the test tag category.",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 请求的标记类别的ID。 |
| `name` | 请求的标记类别的名称。 |
| `description` | 请求的标记类别的描述。 |
| `createdBy` | 创建标记类别的用户的ID。 |
| `createdAt` | 创建标记类别的时间戳。 |
| `modifiedBy` | 上次更新标记类别的用户的ID。 |
| `modifiedAt` | 标记类别上次更新的时间戳。 |
| `tagCount` | 属于标记类别的标记数。 |

+++

## 更新特定标记类别 {#update-tag-category}

>[!IMPORTANT]
>
>只有系统管理员和产品管理员可以使用此API调用。

您可以通过向`/tagCategory`端点发出PATCH请求并指定标记类别的ID来更新属于您组织的特定标记类别的详细信息。

**API格式**

```http
PATCH /tagCategory/{TAG_CATEGORY_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | 正在检索的标记类别的ID。 |

**请求**

+++更新特定标记类别的示例请求

```shell
curl -X PATCH https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "description",
    "value": "Updated sample description",
    "from": "Sample description"
 }]'
```

| 参数 | 描述 |
| --------- | ----------- |
| `op` | 已完成的操作。 要更新特定标记类别，请将此值设置为`replace`。 |
| `path` | 将更新的字段的路径。 支持的值包括`name`和`description`。 |
| `value` | 要更新的字段的更新值。 |
| `from` | 要更新的字段的原始值。 |

+++

**响应**

成功响应HTTP状态200，其中包含有关新更新的标记类别的信息。

+++包含新更新标记类别详细信息的示例响应。

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "Updated sample description",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## 删除特定标记类别 {#delete-tag-category}

>[!IMPORTANT]
>
>只有系统管理员和产品管理员可以使用此API调用。

通过向`/tagCategory`端点发出DELETE请求并指定标记类别的ID，可以删除属于您组织的特定标记类别。

**API格式**

```http
DELETE /tagCategory/{TAG_CATEGORY_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | 正在检索的标记类别的ID。 |

**请求**

+++删除特定标记类别的示例请求

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**响应**

成功的响应返回HTTP状态200以及空响应。

## 检索标记列表 {#get-tags}

您可以通过向`/tags`端点以及标记类别的ID发出GET请求来检索属于您组织的标记列表。

**API格式**

```http
GET /tags
GET /tags?{QUERY_PARAMETERS}
```

检索标记时，可以使用以下可选查询参数。

| 查询参数 | 描述 | 示例 |
| --------------- | ----------- | ------- |
| `start` | 结果列表的开始位置。 您可以使用此项来指示结果分页的起始索引。 | `start=a` |
| `limit` | 每页检索的最大标记数。 | `limit=20` |
| `property` | 检索标记时要过滤的属性。 支持的值包括：<ul><li>`name`：标记的名称。</li><li>`archived`：标记是否已存档或取消存档。 您可以将此值设置为`true`或`false`。</li><li>`tagCategoryId`：标记所属的标记类别的ID。</li></ul> | <ul><li>`property=name==TestTag`</li><li>`property=archived==false`</li><li>`property=tagCategoryId==e2b7c656-067b-4413-a366-adde0401df50`</li> |
| `sortBy` | 标记排序的顺序。 支持的值包括`name`、`createdAt`和`modifiedAt`。 | `sortBy=name` |
| `sortOrder` | 标记类别排序的方向。 支持的值包括`asc`和`desc`。 | `sortOrder=asc` |


**请求**

+++用于检索属于特定标记类别的所有标记的示例请求

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags?property=tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**响应**

成功的响应会返回HTTP状态200，其中包含属于该标记类别的标记的详细信息。

+++ 包含所请求标记详细信息的示例响应。

```json
{
    "_page": {
        "count": 166,
        "limit": 10,
        "next": "eyJjb21wb3NpdGVUb2tlbiI6IntcInRva2VuXCI6XCIrUklEOn52a0owQUp3WDRrVko1d0FBQUFBQUFBPT0jUlQ6MiNUUkM6MjAjUlREOnVDTmQyWlAvWjV6TGdvUGVGR1JHQk1KNVExVmR6Mnc9I0lTVjoyI0lFTzo2NTU2NyNRQ0Y6OCNGUEM6QWdFQ0J3TG1BQ1NmQnNBQ0JBb0FBQVFBQ0FBQUNJQVlnQWVBRElBTmdBWEFFTUJCUUVBQUFBQkFRQkdBSElBR2dBQ0FENEFId0FKUkRFQUNBZ2dBUUJnQUVBQUlIb0FaZ0FDQUJNQUFRVUFBUUFCQVFScUFBc0FTQUFBRUxvQU9nQWFBQmNBQVlBQUFHSUlCUUFDQU1vQUlnQWlBQk1DQUFRQUFnZ0FnQUM2QURZQTNnQWlBR1lBQWdCZUFBY0FCZ0JlQUM4QURBQUlBQWdBQVFBQ0FBRUZBQVFFQUFBRWdBQ0FBSjRCR2dBeUFCSUFPZ0F5QU13QVNRQ0FBQUVBdGdCRUFBR0FkZ0FuQUFDZ0NBQUFBQ0lCQUFDSkFnQUJBRUFDQUg0QUhnQWFBQllBVUFFQUNCQUFFQUFRQUF4QUFzUnJBQUlFQUFBYkxoQklIQVBBQUhnUUVBTEVxQUE4RkNBQVFtcUVBd0FBTWd3Y09BSFdIa1FBZ0JGT0FTNEN4QVE0QVwiLFwicmFuZ2VcIjp7XCJtaW5cIjpcIlwiLFwibWF4XCI6XCJGRlwifX0iLCJvcmRlckJ5SXRlbXMiOlt7Iml0ZW0iOjE2OTQ0ODg2MDMwMDB9XSwicmlkIjoidmtKMEFKd1g0a1hHV2dFQUFBQUFBQT09IiwiaW5jbHVzaXZlIjp0cnVlfQ==",
        "property": [
            "tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50"
        ]
    },
    "tags": [
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8af14b1e-f267-44ad-b94c-9ac70274e3d5",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624481530",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8b907a2c-0f15-4d2c-9672-bf545d5e47ab",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624489131",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "e30bd956-afad-40a1-8f4a-7e4428855856",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624494191",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705451722000,
            "createdBy": "{USER_ID}",
            "id": "3bf6a6ba-0b11-4d83-8f35-db6e5b9652d8",
            "modifiedAt": 1705451722000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705451701640",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705422929000,
            "createdBy": "{USER_ID}",
            "id": "0910dfc8-7924-473d-afc6-1aa68337b3b6",
            "modifiedAt": 1705422929000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705422890399",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705394126000,
            "createdBy": "{USER_ID}",
            "id": "b426085e-580b-4147-9921-8ba77ffa77a9",
            "modifiedAt": 1705394126000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705394104556",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": true,
            "createdAt": 1705392795000,
            "createdBy": "{USER_ID}",
            "id": "92961035-e72b-45a0-9625-781380017585",
            "modifiedAt": 1705392832000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705392794917",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705335274000,
            "createdBy": "{USER_ID}",
            "id": "436ce801-ef87-45fd-b34a-9ce938a447e1",
            "modifiedAt": 1705335274000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705335252944",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694776514000,
            "createdBy": "{USER_ID}",
            "id": "1e6e9836-5e18-4340-a959-3206c9bc3a94",
            "modifiedAt": 1694776514000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694776510734",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694488609000,
            "createdBy": "{USER_ID}",
            "id": "b8400673-2f90-48e9-b73b-cdfbba5ab361",
            "modifiedAt": 1694488609000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694488608301",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        }
    ]
}
```

+++

## 创建新标记 {#create-tag}

>[!IMPORTANT]
>
>只有系统管理员和产品管理员可以使用此API调用在指定的标记类别中创建新标记。
>
>如果您正在创建未分类的标记，则&#x200B;**不需要**&#x200B;管理员权限。

您可以通过向`/tags`端点发出POST请求来创建新标记。

**API格式**

```http
POST /tags
```

**请求**

+++用于创建新标记的示例请求。

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "sampleTag"
 }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | **必需**。 要创建的标记的名称。 |
| `tagCategoryId` | *可选*。 您希望标记所属的标记类别的ID。 如果未指定，则标记将作为“未分类”类别的一部分创建。 |

+++

**响应**

成功的响应会返回HTTP状态201以及新创建标记的详细信息。

+++包含新创建标记详细信息的示例响应。

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Uncategorized-{ORG_ID}",
    "tagCategoryName": "Uncategorized",
    "archived": false
}
```

| 参数 | 描述 |
| --------- | ----------- |
| `name` | 新创建的标记的名称。 |
| `id` | 新创建的标记的ID。 |
| `org` | 标记所属的组织的ID。 |
| `createdAt` | 创建标记时的时间戳。 |
| `createdBy` | 创建标记的用户的ID。 |
| `modifiedAt` | 标记上次更新的时间戳。 |
| `modifiedBy` | 上次更新标记的用户的ID。 |
| `tagCategoryId` | 标记所属的标记类别的ID。 |
| `tagCategoryName` | 标记所属的标记类别的名称。 |

+++

## 检索特定标记 {#get-tag}

您可以通过向`/tags`端点发出GET请求并指定要检索的标记的ID，来检索属于您组织的特定标记。

**API格式**

```http
GET /tags/{TAG_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TAG_ID}` | 正在检索的标记的ID。 |

**请求**

+++检索特定标记的示例请求

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**响应**

成功的响应返回HTTP状态200以及指定标记的详细信息。

+++包含指定标记详细信息的示例响应。

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

| 参数 | 描述 |
| --------- | ----------- |
| `name` | 检索到的标记的名称。 |
| `id` | 您检索到的标记的ID。 |
| `org` | 标记所属的组织的ID。 |
| `createdAt` | 创建标记时的时间戳。 |
| `createdBy` | 创建标记的用户的ID。 |
| `modifiedAt` | 标记上次更新的时间戳。 |
| `modifiedBy` | 上次更新标记的用户的ID。 |
| `tagCategoryId` | 标记所属的标记类别的ID。 |
| `tagCategoryName` | 标记所属的标记类别的名称。 |
| `archived` | 标记的存档状态。 如果设置为`true`，则表示标记已存档。 |

+++

## 验证标记 {#validate-tags}

您可以通过向`/tags/validate`端点发出POST请求来验证标记是否存在。

**API格式**

```http
POST /tags/validate
```

**请求**

+++用于验证所提供的标记ID的示例请求。

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "ids": [
        "2bd5ddd9-7284-4767-81d9-c75b122f2a6a","d113f40c-0097-4626-8d5f-6d5017694453", "invalid-tag"
    ],
    "entity": "{API_KEY}"
 }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `ids` | 包含要验证的标记ID列表的数组。 |
| `entity` | 请求验证的实体。 您可以对此参数使用`{API_KEY}`值。 |

+++

**响应**

成功的响应返回HTTP状态200，其中包含有关哪些标记有效及无效的信息。

+++显示哪些标记有效或无效的示例响应。

```json
{
    "invalidTags": [
        {
            "id": "invalid-tag"
        }
    ],
    "validTags": [
        {
            "id": "d113f40c-0097-4626-8d5f-6d5017694453"
        },
        {
            "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a"
        }
    ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `invalidTags` | 包含无效标记ID列表的数组。 |
| `validTags` | 包含有效标记ID列表的数组。 |

+++

## 更新特定标记 {#update-tag}

您可以通过向`/tags`端点发出PATCH请求并提供要更新的标记的ID来更新指定的标记。

**API格式**

```http
PATCH /tags/{TAG_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TAG_ID}` | 要更新的标记的ID。 |

**请求**

+++更新特定标记的示例请求

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "name",
    "value": "newSampleTag",
    "from": "sampleTag"
 }]'
```

| 属性 | 描述 |
| -------- | ----------- |
| `op` | 需要执行的操作。 在此使用案例中，它将始终设置为`replace`。 |
| `path` | 将更新的字段的路径。 支持的值包括`name`、`archived`和`tagCategoryId`。 |
| `value` | 要更新的字段的更新值。 |
| `from` | 要更新的字段的原始值。 |

+++

**响应**

成功的响应返回HTTP状态200以及新更新标记的详细信息。

+++包含已更新标记详细信息的示例响应。

```json
{
    "name": "newSampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

+++

## 删除特定标记 {#delete-tag}

>[!IMPORTANT]
>
>只有系统管理员和产品管理员可以使用此API调用。
>
>此外，标记&#x200B;**不能**&#x200B;与任何业务对象相关联，而且&#x200B;**必须**&#x200B;存档后才能删除标记。 您可以使用[更新标记终结点](#update-tag)将标记存档。

您可以通过为`/tags`端点创建DELETE标记并指定要删除的标记的ID来删除特定标记。

**API格式**

```http
DELETE /tags/{TAG_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TAG_ID}` | 您要删除的标记的ID。 |

**请求**

+++删除特定标记的示例请求

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**响应**

成功的响应返回HTTP状态200以及空响应。

## 后续步骤

阅读本指南后，您将会更好地了解如何使用Adobe Experience Platform API创建、管理和删除标记和标记类别。 有关使用UI管理标记的更多信息，请参阅[管理标记指南](../ui/managing-tags.md)。 有关使用UI管理标记类别的更多信息，请参阅[标记类别指南](../ui/tags-categories.md)。
