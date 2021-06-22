---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；架构注册；架构注册；合并；合并；合并；合并；合并；会合；区段成员资格；timeSeriesEvents;
solution: Experience Platform
title: Unions API端点
description: 架构注册表API中的/unions端点允许您以编程方式管理体验应用程序中的XDM并集架构。
topic-legacy: developer guide
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: e4bf5bb77ac4186b24580329699d74d653310d93
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 3%

---

# Unions端点

联合（或联合视图）是系统生成的只读架构，用于聚合共享相同类（[!DNL XDM ExperienceEvent]或[!DNL XDM Individual Profile]）并为[[!DNL Real-time Customer Profile]](../../profile/home.md)启用的所有架构的字段。

本文档介绍了在架构注册表API中与工会合作的基本概念，包括各种操作的示例调用。 有关XDM中联合的更多常规信息，请参阅[架构组合基础知识](../schema/composition.md#union)中有关联合的部分。

## 并集架构字段

[!DNL Schema Registry]会自动在并集架构中包含三个关键字段：`identityMap`、`timeSeriesEvents`和`segmentMembership`。

### 身份映射

并集架构的`identityMap`是并集关联记录架构内已知标识的表示形式。 标识映射将标识分隔为由命名空间键控的不同数组。 列出的每个标识本身都是一个包含唯一`id`值的对象。 有关更多信息，请参阅[Identity Service文档](../../identity-service/home.md)。

### 时间系列事件

`timeSeriesEvents`数组是与与并集关联的记录架构相关的时间序列事件列表。 将配置文件数据导出到数据集时，每个记录都包含此数组。 这对于各种用例非常有用，例如机器学习，在该用例中，模型除了需要记录属性之外，还需要用户档案的整个行为历史记录。

### 区段成员资格映射

`segmentMembership`映射存储区段评估的结果。 使用[分段API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)成功运行区段作业时，将更新映射。 `segmentMembership` 此外，还存储了摄取到Platform中的任何预评估受众区段，以便与Adobe Audience Manager等其他解决方案集成。有关更多信息，请参阅有关[使用API创建区段的教程](../../segmentation/tutorials/create-a-segment.md) 。

## 检索工会列表 {#list}

在架构上设置`union`标记后，[!DNL Schema Registry]会自动将架构添加到该架构所依据的类的并集中。 如果相关类不存在并集，则会自动创建新并集。 并集的`$id`与其他[!DNL Schema Registry]资源的标准`$id`类似，唯一的区别在于附加了两个下划线和单词“union”(`__union`)。

通过向`/tenant/unions`端点发出GET请求，可以查看可用联合的列表。

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

响应格式取决于请求中发送的`Accept`标头。 以下`Accept`标头可用于列表联合：

| `Accept` 标题 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每个资源的简短摘要。 这是列出资源的建议标头。 (限制：300) |
| `application/vnd.adobe.xed+json` | 为每个资源返回完整的JSON类，其中包含原始的`$ref`和`allOf`。 (限制：300) |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回HTTP状态200(OK)和响应正文中的`results`数组。 如果定义了并集，则每个并集的详细信息将作为数组中的对象提供。 如果尚未定义联合，则仍会返回HTTP状态200（确定），但`results`数组将为空。

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

## 查找工会 {#lookup}

您可以通过执行包含`$id`的GET请求来查看特定的并集，并根据Accept标头，查看并集的部分或全部详细信息。

>[!NOTE]
>
>使用`/unions`和`/schemas`端点可进行并集查找，以启用它们以在[!DNL Profile]导出到数据集中时使用。

**API格式**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{UNION_ID}` | 要查找的并集的URL编码的`$id` URI。 并集模式的URI将附加“__union”。 |

{style=&quot;table-layout:auto&quot;}

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

并集查找请求要求在Accept标头中包含`version`。

以下接受标头可用于并集架构查找：

| Accept | 描述 |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | 具有`$ref`和`allOf`的原始数据。 包括标题和描述。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 属性和已 `allOf` 解析。包括标题和描述。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功响应会返回实现请求路径中提供`$id`类的所有架构的并集视图。

响应格式取决于请求中发送的Accept标头。 尝试使用不同的接受标头来比较响应并确定最适合您的用例的标头。

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

## 启用联合成员资格的架构 {#enable}

要将架构包含在其类的并集中，必须将`union`标记添加到架构的`meta:immutableTags`属性中。 为此，您可以发出PATCH请求，将`meta:immutableTags`数组（单个字符串值为`union`）添加到相关架构中。 有关详细示例，请参阅[架构端点指南](./schemas.md#union)。

## 列出并集{#list-schemas}中的架构

为了查看哪些架构是特定并集的一部分，您可以对`/tenant/schemas`端点执行GET请求。 使用`property`查询参数，您可以配置响应，以仅返回包含`meta:immutableTags`字段和等于您正在访问的并集的类的`meta:class`架构。

**API格式**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | 要列出其启用并集架构的类的`$id`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求将检索属于[!DNL XDM Individual Profile]类并集的所有架构的列表。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于请求中发送的`Accept`标头。 以下`Accept`标头可用于列出架构：

| `Accept` 标题 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每个资源的简短摘要。 这是列出资源的建议标头。 (限制：300) |
| `application/vnd.adobe.xed+json` | 为每个资源返回完整的JSON架构，其中包含原始的`$ref`和`allOf`。 (限制：300) |

{style=&quot;table-layout:auto&quot;}

**响应**

成功响应会返回一个已过滤的架构列表，其中仅包含属于已启用并集成员资格的指定类的架构列表。 请记住，使用多个查询参数时，假定为AND关系。

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
