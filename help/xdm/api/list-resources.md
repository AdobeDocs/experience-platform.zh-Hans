---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 列表资源
topic: developer guide
translation-type: tm+mt
source-git-commit: 4b052cdd3aca9c771855b2dc2a97ca48c7b8ffb0

---


# 列表资源

您可以通过执行单个GET请求来视图容器中所有资源(模式、类、混合或数据类型)的列表。

>[!NOTE] 列出资源时，模式登记处将结果集限制为300项。 要返回超出此限制的资源，您必须使用分 [页参数](#paging)。 还建议使用查询参数筛选结 [果](#filtering) ，并减少返回的资源数。
>
> 如果要完全覆盖300项限制，则必须使用“接受”标题以在单 `application/vnd.adobe.xdm-v2+json` 个请求中返回所有结果。

**API格式**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 资源所在的容器（“全局”或“租户”）。 |
| `{RESOURCE_TYPE}` | 要从模式库检索的资源类型。 有效类 `datatypes`型有 `mixins`、 `schemas`和 `classes`。 |
| `{QUERY_PARAMS`} | 可选查询参数，用于筛选结果。 有关详细信息，请 [参阅查询](#query) 参数一节。 |

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes&limit=2 \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于在请求中发送的Accept头。 列表资源可使用以下“接受”标题：

| 接受标题 | 描述 |
| ------- | ------------ |
| application/vnd.adobe.xed-id+json | 返回每个资源的简短摘要。 这是列表资源的建议标题。 (限制：300) |
| application/vnd.adobe.xed+json | 返回每个资源的完整JSON模式，其中包含 `$ref` 原始 `allOf` 资源。 (限制：300) |
| application/vnd.adobe.xdm-v2+json | 为单个请求中的所有结果返回完整的JSON模式，覆盖300项限制。 |

**响应**

上述请求使用“接 `application/vnd.adobe.xed-id+json` 受”标题，因此响应仅包括每个资 `title`源的 `$id`、 `meta:altId`和 `version` 属性。 替换 `full` 到“接受”标题将返回每个资源的所有属性。 根据您在响应中需要的信息选择相应的“接受”标题。

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## 使用查询参数 {#query}

模式注册表支持在列出资源时使用查询参数进行页面和筛选结果。

>[!NOTE] 组合多个查询参数时，必须用&amp;符号(`&`)分隔。

### 分页 {#paging}

用于分页的最常见的查询参数包括：

| 参数 | 描述 |
| --- | --- |
| `start` | 指定列出的结果的起点。 示例：将 `start=2` 从第三个返回项目开始列表结果。 |
| `limit` | 限制返回的资源数。 示例：将 `limit=5` 返回一列表五项资源。 |
| `orderby` | 按特定属性对结果排序。 示例：将 `orderby=title` 按标题按升序(A-Z)对结果排序。 在标题( `-` )之前添`orderby=-title`加一个选项将按标题按降序(Z-A)对项目进行排序。 |

### 筛选 {#filtering}

您可以使用参数筛选结果，该参 `property` 数用于对检索的资源中的给定JSON属性应用特定的运算符。 支持的运算符包括：

| 运算符 | 描述 | 示例 |
| --- | --- | --- |
| `==` | 过滤器是否等于提供的值。 | `property=title==test` |
| `!=` | 过滤器，即物业是否不等于提供值。 | `property=title!=test` |
| `<` | 过滤器该物业是否低于提供价值。 | `property=version<5` |
| `>` | 过滤器该属性是否大于提供的值。 | `property=version>5` |
| `<=` | 过滤器该物业是否低于或等于提供值。 | `property=version<=5` |
| `>=` | 过滤器该属性是否大于或等于提供的值。 | `property=version>=5` |
| `~` | 过滤器，依据该物业是否与提供的常规表达式相匹配。 | `property=title~test$` |
| (无) | 仅声明属性名称仅返回属性所在的条目。 | `property=title` |

>[!TIP] 可以使用该参 `property` 数按其兼容类过滤混音。 例如，仅 `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` 返回与XDM Individual用户档案类兼容的混音。
