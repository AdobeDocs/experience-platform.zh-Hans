---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 合并
topic: developer guide
translation-type: tm+mt
source-git-commit: 7f61cee8fb5160d0f393f8392b4ce2462d602981

---


# 合并

合并(或合并视图)是系统生成的只读模式,聚合共享同一类(XDM ExperienceEvent或XDM个人用户档案)的所有模式的字段，并启用实时客户用户档案 [](../../profile/home.md)。

本文档涵盖与模式注册表API中的合并协作的基本概念，包括各种操作的示例调用。 有关XDM中合并的更多一般信息，请参阅模式合成基础 [知识中的合并部分](../schema/composition.md#union)。

## 合并混合

模式注册处自动在合并模式中包括三个混音： `identityMap`、 `timeSeriesEvents`和 `segmentMembership`。

### 身份映射

合并模式 `identityMap` 是合并相关记录模式中已知身份的表示。 标识映射将标识分为由命名空间键控的不同数组。 列出的每个标识本身都是一个包含唯一值的 `id` 对象。

See the [Identity Service documentation](../../identity-service/home.md) for more information.

### 时间序列事件

该 `timeSeriesEvents` 阵列是与与该列表相关联的记录模式相关的时间序列事件的合并。 将用户档案数据导出到数据集时，每个记录都包含此数组。 这对于各种用例（如机器学习）很有用，其中模型除了记录属性外还需要用户档案的整个行为历史记录。

### 区段成员关系图

该 `segmentMembership` 地图存储分部评估的结果。 当使用分段API成功运行段作 [业时](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)，将更新映射。 `segmentMembership` 还存储任何被引入平台的预评估受众细分，允许与Adobe受众管理器等其他解决方案集成。

有关详细信息，请 [参阅有关使用API创建区段](../../segmentation/tutorials/create-a-segment.md) 的教程。

## 为模式会员资格启用合并

要使模式包含在合并合并视图中，必须将“合并”标签添加到模式的 `meta:immutableTags` 属性中。 这是通过PATCH请求完成的，该请求用于更新模式并 `meta:immutableTags` 添加值为“合并”的阵列。

>[!NOTE] 不可改变的标记是要设置但从不删除的标记。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | URL编码的 `$id` URI或 `meta:altId` 要启用以在用户档案中使用的模式。 |

**请求**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**响应**

成功的响应会返回更新的模式的详细信息，该更新现在包括一个 `meta:immutableTags` 包含字符串值“合并”的数组。

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.2",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552091263267,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 列表合并

在模式上设置“合并”标签时，模式注册表会自动为该模式所基于的类创建和维护一个合并。 合并 `$id` 与类的标准相似，唯一的区别是 `$id` 附加两个下划线和单词“合并”(`"__union"`)。

要视图可用合并的列表，可以对端点执行GET请 `/unions` 求。

**API格式**

```http
GET /tenant/unions
```

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**响应**

成功的响应会返回HTTP状态200(OK)和响 `results` 应体中的数组。 如果已定义合并，则每 `title`个合并的、 `$id`、 `meta:altId`和 `version` 将作为数组中的对象提供。 如果尚未定义合并，则仍会返回HTTP状态200（确定），但数 `results` 组将为空。

```JSON
{
    "results": [
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile__union",
            "meta:altId": "_xdm.context.profile__union",
            "version": "1"
        },
        {
            "title": "Property",
            "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590__union",
            "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590__union",
            "version": "1"
        }
    ]
}
```

## 查找特定合并

您可以通过执行GET请求来视图特定合并，该请求包含和(取决于 `$id` Accept头)，该合并的部分或全部详细信息。

>[!NOTE] 合并查找可使用和 `/unions` 端点 `/schemas` 来启用它们，以便在用户档案导出到数据集中时使用。

**API格式**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{UNION_ID}` | 要查找的合并的URL `$id` 编码URI。 合并模式的URI后面附加有“__合并”。 |

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

合并查找请求需 `version` 要包含在“接受”标题中。

以下“接受”标题可用于合并模式查找：

| 接受 | 描述 |
| -------|------------ |
| application/vnd.adobe.xed+json;version={MAJOR_VERSION} | Raw with `$ref` and `allOf`. 包括标题和说明。 |
| application/vnd.adobe.xed-full+json;version={MAJOR_VERSION} | `$ref` 属性和已 `allOf` 解析。 包括标题和说明。 |

**响应**

成功的响应将返回实现请求路径中提供的类的所有合并 `$id` 的模式视图。

响应格式取决于在请求中发送的Accept头。 尝试不同的接受标题以比较响应并确定最适合您的用例的标题。

```JSON
{
    "type": "object",
    "description": "Union view of all schemas that extend https://ns.adobe.com/xdm/context/profile",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "title": "Union object for https://ns.adobe.com/xdm/context/profile",
    "$id": "https://ns.adobe.com/xdm/context/profile__union",
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:altId": "_xdm.context.profile__union",
    "version": "1.0",
    "meta:resourceType": "unions",
    "meta:registryMetadata": {}
}
```

## 列表模式

为了查看哪些模式是特定合并的一部分，您可以使用查询参数在租户容器中过滤模式，从而执行GET请求。

使用 `property` 查询参数，您可以配置响应，以仅返回包含字段和等于您正在访问其合并的 `meta:immutableTags``meta:class` 类的模式。

**API格式**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | 要 `$id` 访问其合并的类的名称。 |

**请求**

以下请求查找属于XDM单个模式类合并的所有用户档案。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回筛选后的模式列表，该仅包含满足这两个要求的响应。 请记住，在使用多个查询参数时，会假定AND关系。 响应的格式取决于请求中发送的接受头。

```JSON
{
    "results": [
        {
            "title": "Schema 1",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "meta:altId": "_{TENANT_ID}.schemas.142afb78d8b368a5ba97a6cc8fc7e033",
            "version": "1.2"
        },
        {
            "title": "Schema 2",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e7297a6ddfc7812ab3a7b504a1ab98da",
            "meta:altId": "_{TENANT_ID}.schemas.e7297a6ddfc7812ab3a7b504a1ab98da",
            "version": "1.5"
        },
        {
            "title": "Schema 3",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/50f960bb810e99a21737254866a477bf",
            "meta:altId": "_{TENANT_ID}.schemas.50f960bb810e99a21737254866a477bf",
            "version": "1.2"
        },
        {
            "title": "Schema 4",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/a39655ca8ea3d5c1f36a463b45fccca8",
            "meta:altId": "_{TENANT_ID}.schemas.a39655ca8ea3d5c1f36a463b45fccca8",
            "version": "1.1"
        },
        {
            "title": "Schema 5",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c063fac45c6d6285ef33b0e2af09f633",
            "meta:altId": "_{TENANT_ID}.schemas.c063fac45c6d6285ef33b0e2af09f633",
            "version": "1.2"
        },
        {
            "title": "Schema 6",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/dfebb19b93827b70bbad006137812537",
            "meta:altId": "_{TENANT_ID}.schemas.dfebb19b93827b70bbad006137812537",
            "version": "1.7"
        }
    ],
    "_links": {
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```
