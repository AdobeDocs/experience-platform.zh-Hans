---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;list;List;get;GET
solution: Experience Platform
title: 列表资源
description: 您可以通过执行单个视图请求，列表某个容器中特定类型(类、混合、模式、数据类型或描述符)的所有模式注册表资源。
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 2%

---


# 列表资源

您可以通过执行单个 [!DNL Schema Registry] GET请求，视图容器中特定类型(类、混合、模式、数据类型或描述符)的所有资源的列表。

>[!NOTE]
>
>列出资源时， [!DNL Schema Registry] 结果集限制为300项。 要返回超出此限制的资源，必须使用分 [页参数](#paging)。 还建议使用查询参数来筛 [选结果](#filtering) ，并减少返回的资源数。

**API格式**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 资源所在的容器（“全局”或“租户”）。 |
| `{RESOURCE_TYPE}` | 要从中检索的资源的类型 [!DNL Schema Library]。 有效类 `classes`型有 `mixins`、 `schemas`、 `datatypes`和 `descriptors`。 |
| `{QUERY_PARAMS}` | 可选查询参数，用于筛选结果。 有关详细信息，请 [参阅查询](#query) 参数一节。 |

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

响应格式取决于请求中发送的接受头。 下列接受标题可用于列出资源：

| 接受标题 | 描述 |
| ------- | ------------ |
| application/vnd.adobe.xed-id+json | 返回每个资源的简短摘要。 这是列出资源的建议标头。 (限制：300) |
| application/vnd.adobe.xed+json | 返回每个资源的完整JSON模式，其中包 `$ref` 含原始 `allOf` 资源。 (限制：300) |
| application/vnd.adobe.xdm-v2+json | 使用端点 `/descriptors` 时，必须使用此Accept头才能使用分页功能。 |

**响应**

上述请求使用 `application/vnd.adobe.xed-id+json` Accept标题，因此响应只包括每个资 `title`源的 `$id`、 `meta:altId`和 `version` 属性。 替换 `full` 到“接受”标题将返回每个资源的所有属性。 根据您在响应中需要的信息选择相应的接受标题。

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

支 [!DNL Schema Registry] 持在列出资源时使用查询参数进行页面和筛选结果。

>[!NOTE]
>
>组合多个查询参数时，必须用和号(`&`)分隔。

### 分页 {#paging}

用于分页的最常见的查询参数包括：

| 参数 | 描述 |
| --- | --- |
| `start` | 指定列出的结果的开始位置。 此值可以从列表响 `_page.next` 应的属性中获取，并用于访问结果的下一页。 如果 `_page.next` 值为null，则没有其他页可用。 |
| `limit` | 限制返回的资源数。 示例： `limit=5` 将返还列表5个资源。 |
| `orderby` | 按特定属性对结果排序。 示例： `orderby=title` 将按标题按升序(A-Z)对结果排序。 在标 `-` 题()`orderby=-title`前添加一个标题将按标题以降序(Z-A)对项目排序。 |

### 筛选 {#filtering}

您可以使用参数筛选结 `property` 果，该参数用于对检索的资源中的给定JSON属性应用特定运算符。 支持的运算符包括：

| 运算符 | 描述 | 示例 |
| --- | --- | --- |
| `==` | 过滤器属性是否等于提供的值。 | `property=title==test` |
| `!=` | 过滤器：属性是否不等于提供的值。 | `property=title!=test` |
| `<` | 过滤器该属性是否小于提供的值。 | `property=version<5` |
| `>` | 过滤器该属性是否大于提供的值。 | `property=version>5` |
| `<=` | 过滤器，该属性是否小于或等于提供的值。 | `property=version<=5` |
| `>=` | 过滤器为属性是大于或等于提供的值。 | `property=version>=5` |
| `~` | 过滤器，根据该属性是否与提供的常规表达式匹配。 | `property=title~test$` |
| (None) | 仅声明属性名称只返回存在属性的条目。 | `property=title` |

>[!TIP]
>
>可以使用该参 `property` 数按其兼容类过滤混音。 例如， `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` 只返回与类兼容的混 [!DNL XDM Individual Profile] 合。
