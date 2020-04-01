---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 列表资源
topic: developer guide
translation-type: tm+mt
source-git-commit: 1541b027a4e572dc5e4e64de1117a269c58bafab

---


# 列表资源

您可以通过执行单个GET请求来视图容器中所有资源(模式、类、混合或数据类型)的列表。 为了帮助筛选结果，模式注册表支持在列出资源时使用查询参数。

最常见的查询参数包括：

* `limit` -限制返回的资源数。 示例：将 `limit=5` 返回一列表五项资源。
* `orderby` -按特定属性对结果排序。 示例：将 `orderby=title` 按标题按升序(A-Z)对结果排序。 在标题( `-` )之前添`orderby=-title`加一个选项将按标题按降序(Z-A)对项目进行排序。
* `property` -对任何顶级属性筛选结果。 例如，仅 `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` 返回与XDM Individual用户档案类兼容的混音。

组合多个查询参数时，必须用&amp;符号(`&`)分隔。

**API格式**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 资源所在的容器（“全局”或“租户”）。 |
| `{RESOURCE_TYPE}` | 要从模式库检索的资源类型。 有效类 `datatypes`型有 `mixins`、 `schemas`和 `classes`。 |

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
| application/vnd.adobe.xed-id+json | 返回每个资源的简短摘要，通常是列表的首选标题 |
| application/vnd.adobe.xed+json | 返回每个资源的完整JSON模式，其中包含 `$ref` 原始 `allOf` 资源 |

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
