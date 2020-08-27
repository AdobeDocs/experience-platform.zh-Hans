---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 合并
topic: developer guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---


# 合并

合并(或合并视图)是系统生成的只读模式，它聚合共享同一类(或[!DNL XDM ExperienceEvent][!DNL XDM Individual Profile])并启用[!DNL实 [时客户用户档案]的所有模式的字段](../../profile/home.md)。

此文档涵盖在模式注册表API中与合并协作的基本概念，包括各种操作的示例调用。 有关XDM中合并的更多一般信息，请参阅模式合成基 [础知识中的合并部分](../schema/composition.md#union)。

## 合并混合

在合并 [!DNL Schema Registry] 模式中，自动包含三个混音： `identityMap`、 `timeSeriesEvents`和 `segmentMembership`。

### 身份映射

合并 `identityMap` 模式是合并相关记录模式中已知身份的表示。 标识图将标识分为由命名空间键控的不同数组。 列出的每个标识本身都是包含唯一值的 `id` 对象。

See the [Identity Service documentation](../../identity-service/home.md) for more information.

### 时间系列事件

阵 `timeSeriesEvents` 列是与与列表相关联的记录模式相关的时间序列事件的合并。 当数 [!DNL Profile] 据导出到数据集时，每个记录都包含此数组。 这对于各种用例都很有用，例如机器学习，其中模型除了记录属性外还需要用户档案的整个行为历史记录。

### 区段成员关系图

该 `segmentMembership` 地图存储分部评估的结果。 使用分段API成功运行段作 [业时](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)，将更新映射。 `segmentMembership` 还存储任何预评估的受众细分，这些细分被引入平台，允许与Adobe Audience Manager等其他解决方案集成。

有关详细信息， [请参阅有关使用API创建](../../segmentation/tutorials/create-a-segment.md) 区段的教程。

## 启用模式以成为合并会员

要将模式包含在合并合并视图中，必须将“合并”标记添加到模式 `meta:immutableTags` 的属性中。 这是通过PATCH请求来更新模式并添 `meta:immutableTags` 加值为“合并”的数组。

>[!NOTE]
>
>不可变标记是要设置但从不删除的标记。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | URL编码 `$id` 的URI `meta:altId` 或要在中启用的模式的URI [!DNL Profile]。 |

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

成功的响应会返回更新模式的详细信息，该现在包 `meta:immutableTags` 含一个包含字符串值“合并”的数组。

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

在模式上设置“合并”标签时，将自 [!DNL Schema Registry] 动为模式所基于的类创建和维护合并。 合并 `$id` 的与类的标准相似，唯一 `$id` 的区别是用两个下划线和单词“合并”(`"__union"`)附加。

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

成功的响应返回HTTP状态200(OK)和响 `results` 应主体中的数组。 如果已定义合并，则 `title`每个 `$id`的 `meta:altId`、、和 `version` 合并都作为数组中的对象提供。 如果尚未定义合并，则仍返回HTTP状态200（确定），但数 `results` 组将为空。

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

您可以通过执行包含和的视图请求来GET特 `$id` 定合并，具体取决于“接受”标题，包括合并的部分或全部详细信息。

>[!NOTE]
>
>合并查找可使用 `/unions` 和 `/schemas` 端点，以便在导出到数 [!DNL Profile] 据集时使用。

**API格式**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{UNION_ID}` | 要查找的 `$id` 合并的URL编码URI。 合并模式的URI附加“__合并”。 |

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

合并查找请求 `version` 需要包含在Accept头中。

以下接受标题可用于合并模式查找：

| 接受 | 描述 |
| -------|------------ |
| application/vnd.adobe.xed+json;version={MAJOR_VERSION} | 原始 `$ref` 和 `allOf`。 包括标题和说明。 |
| application/vnd.adobe.xed-full+json;version={MAJOR_VERSION} | `$ref` 属性和已 `allOf` 解析。 包括标题和说明。 |

**响应**

成功的响应返回实现请求路径中提供的类的所有合并 `$id` 的模式视图。

响应格式取决于请求中发送的接受头。 尝试不同的接受标题以比较响应并确定最适合您的用例的标题。

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

为了查看哪些模式是特定合并的一部分，您可以使用查询参数来执行GET请求，以在租户容器内过滤模式。

使用 `property` 查询参数，您可以配置响应以仅返回包含字段和等于 `meta:immutableTags` 您正在访 `meta:class` 问其合并的类的模式。

**API格式**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | 要 `$id` 访问其合并的类的名称。 |

**请求**

以下请求会查找属于类模式的所 [!DNL XDM Individual Profile] 有合并。

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

成功的响应会返回已过滤的模式列表，只包含满足这两个要求的。 请记住，使用多个查询参数时，会假定AND关系。 响应的格式取决于请求中发送的接受头。

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
