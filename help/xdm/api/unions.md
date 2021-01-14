---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;union;Union;unions;Unions;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: 合并
description: 模式注册表API中的/合并端点允许您以编程方式管理体验应用程序中的XDM合并模式。
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 1%

---


# 合并端点

合并(或合并视图)是系统生成的只读模式，它聚合共享相同类（[!DNL XDM ExperienceEvent]或[!DNL XDM Individual Profile]）并为[[!DNL Real-time Customer Profile]](../../profile/home.md)启用的所有模式的字段。

此文档涵盖在模式注册表API中与合并协作的基本概念，包括各种操作的示例调用。 有关XDM中合并的更多一般信息，请参阅[模式合成基础知识](../schema/composition.md#union)中有关合并的部分。

## 合并模式字段

[!DNL Schema Registry]在合并模式中自动包含三个键字段：`identityMap`、`timeSeriesEvents`和`segmentMembership`。

### 身份映射

合并模式的`identityMap`是合并相关记录模式中已知身份的表示。 标识图将标识分为由命名空间键控的不同数组。 列出的每个标识本身都是一个包含唯一`id`值的对象。 有关详细信息，请参阅[Identity Service文档](../../identity-service/home.md)。

### 时间系列事件

`timeSeriesEvents`阵列是与与该事件关联的记录模式相关的时间序列列表。 将用户档案数据导出到数据集时，每个记录都包含此数组。 这对于各种用例都很有用，例如机器学习，其中模型除了记录属性外还需要用户档案的整个行为历史记录。

### 区段成员关系图

`segmentMembership`映射存储段评估的结果。 使用[分段API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)成功运行段作业时，将更新映射。 `segmentMembership` 还存储任何预评估的受众细分，这些细分被引入平台，允许与Adobe Audience Manager等其他解决方案集成。有关详细信息，请参阅[使用API创建区段的教程](../../segmentation/tutorials/create-a-segment.md)。

## 检索列表合并{#list}

在模式上设置`union`标记时，[!DNL Schema Registry]会自动将模式添加到模式所基于的类的合并中。 如果所涉及的类不存在合并，则会自动创建新合并。 该合并的`$id`与其他[!DNL Schema Registry]资源的标准`$id`类似，唯一的区别是附加两个下划线和单词“合并”(`__union`)。

可以通过向`/tenant/unions`端点发出GET请求来视图可用合并的列表。

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

响应格式取决于请求中发送的`Accept`头。 以下`Accept`标头可用于列出合并:

| `Accept` 标题 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每个资源的简短摘要。 这是列出资源的建议标头。 (限制：300) |
| `application/vnd.adobe.xed+json` | 为每个资源返回完整的JSON类，其中包含原始`$ref`和`allOf`。 (限制：300) |

**响应**

成功的响应会返回HTTP状态200(OK)和响应主体中的`results`数组。 如果已定义合并，则每个合并的详细信息将作为数组中的对象提供。 如果尚未定义合并，则仍返回HTTP状态200（确定），但`results`数组将为空。

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

## 查找合并{#lookup}

您可以通过执行包含`$id`的GET请求来视图特定合并，并根据“接受”标题，执行合并的部分或全部详细信息。

>[!NOTE]
>
>合并查找可使用`/unions`和`/schemas`端点，以允许在[!DNL Profile]导出到数据集中时使用。

**API格式**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{UNION_ID}` | 要查找的合并的URL编码的`$id` URI。 合并模式的URI附加“__合并”。 |

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

合并查找请求要求`version`包含在“接受”标头中。

以下接受标题可用于合并模式查找：

| 接受 | 描述 |
| -------|------------ |
| application/vnd.adobe.xed+json;version={MAJOR_VERSION} | 具有`$ref`和`allOf`的原始数据。 包括标题和说明。 |
| application/vnd.adobe.xed-full+json;version={MAJOR_VERSION} | `$ref` 属性和已 `allOf` 解析。包括标题和说明。 |

**响应**

成功的响应返回实现`$id`在请求路径中提供的类的所有模式的合并视图。

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

## 启用合并成员身份模式{#enable}

要使模式包含在其类的合并中，必须将`union`标记添加到模式的`meta:immutableTags`属性中。 为此，可以发出PATCH请求，将`meta:immutableTags`数组添加为单个字符串值`union`的模式。 有关详细示例，请参见[模式端点指南](./schemas.md#union)。

## 列表{#list-schemas}合并中的模式

为了查看哪些模式是特定合并的一部分，您可以对`/tenant/schemas`端点执行GET请求。 使用`property`查询参数，可以配置响应以仅返回包含`meta:immutableTags`字段和与您访问其合并的类相等的`meta:class`的模式。

**API格式**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | 类的`$id`，要合并其启用模式的类。 |

**请求**

以下请求检索属于[!DNL XDM Individual Profile]类列表的所有模式的合并。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于请求中发送的`Accept`头。 以下`Accept`标头可用于列出模式:

| `Accept` 标题 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每个资源的简短摘要。 这是列出资源的建议标头。 (限制：300) |
| `application/vnd.adobe.xed+json` | 为每个资源返回完整的JSON模式，其中包括原始的`$ref`和`allOf`。 (限制：300) |

**响应**

成功的响应会返回已过滤的模式列表，该仅包含属于已启用合并成员资格的指定类的。 请记住，使用多个查询参数时，会假定AND关系。

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
