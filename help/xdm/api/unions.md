---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；架构注册表；架构注册表；联合；联合；联合；区段成员资格；timeSeriesEvents；
solution: Experience Platform
title: 联合API端点
description: 架构注册API中的/unions端点允许您以编程方式管理体验应用程序中的XDM合并架构。
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 1%

---

# 合并端点

联合（或联合视图）是系统生成的只读架构，这些架构聚合了共享相同类（[!DNL XDM ExperienceEvent]或[!DNL XDM Individual Profile]）并已为[[!DNL Real-Time Customer Profile]](../../profile/home.md)启用的所有架构的字段。

本文档介绍了在架构注册表API中使用合并的基本概念，包括各种操作的示例调用。 有关XDM中联合的更多常规信息，请参阅架构组合[基础知识](../schema/composition.md#union)中有关联合的部分。

## 合并架构字段

[!DNL Schema Registry]自动在合并架构中包含三个键字段：`identityMap`、`timeSeriesEvents`和`segmentMembership`。

### 标识映射

联合架构的`identityMap`表示联合关联记录架构中的已知标识。 标识映射将标识分隔为命名空间键控的不同数组。 列出的每个标识本身都是包含唯一`id`值的对象。 有关详细信息，请参阅[Identity Service文档](../../identity-service/home.md)。

### 时间序列事件

`timeSeriesEvents`数组是与联合关联的记录架构相关的时间系列事件列表。 配置文件数据导出到数据集时，每个记录都包含此数组。 这在各种用例中非常有用，例如机器学习，在这些用例中，模型需要用户档案的整个行为历史记录及其记录属性。

### 区段成员关系图

`segmentMembership`映射存储评估区段定义的结果。 使用[分段API](https://www.adobe.io/experience-platform-apis/references/segmentation/)成功运行区段作业后，映射将更新。 `segmentMembership`还会存储提取到Experience Platform中的任何预评估受众，以便与其他解决方案(如Adobe Audience Manager)集成。 有关详细信息，请参阅有关[使用API创建受众](../../segmentation/tutorials/create-a-segment.md)的教程。

## 检索联合列表 {#list}

在架构上设置`union`标记时，[!DNL Schema Registry]会自动将架构添加到架构所基于的类的并集。 如果相关类不存在并集，则会自动创建新并集。 联合的`$id`类似于其他[!DNL Schema Registry]资源的标准`$id`，唯一的区别是后附两个下划线和单词“联合”(`__union`)。

通过向`/tenant/unions`端点发出GET请求，可查看可用联合的列表。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

响应格式取决于请求中发送的`Accept`标头。 以下`Accept`标头可用于列出联合：

| `Accept`标头 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每个资源的简短摘要。 这是列出资源的推荐标头。 （限制：300） |
| `application/vnd.adobe.xed+json` | 返回每个资源的完整JSON类，包括原始`$ref`和`allOf`。 （限制：300） |

{style="table-layout:auto"}

**响应**

成功的响应在响应正文中返回HTTP状态200 （正常）和`results`数组。 如果定义了联合，则每个联合的详细信息将作为数组中的对象提供。 如果未定义联合，则仍返回HTTP状态200 （正常），但`results`数组将为空。

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

## 查找联合 {#lookup}

通过执行包含`$id`的GET请求，您可以查看特定的并集，并根据“接受”标头，查看并集的部分或全部详细信息。

>[!NOTE]
>
>合并查找可使用`/unions`和`/schemas`终结点启用，以便在向数据集的[!DNL Profile]导出中使用它们。

**API格式**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{UNION_ID}` | 要查找的合并的URL编码的`$id` URI。 联合架构的URI会附加“__union”。 |

{style="table-layout:auto"}

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

联合查找请求要求在Accept标头中包含`version`。

以下接受标头可用于合并架构查找：

| 接受 | 描述 |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | 带有`$ref`和`allOf`的原始。 包括标题和描述。 |
| `application/vnd.adobe.xed-full+json; version=1` | 已解决`$ref`属性和`allOf`。 包括标题和描述。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回所有架构的合并视图，这些架构实现在请求路径中提供了`$id`的类。

响应格式取决于请求中发送的“接受”标头。 试验不同的“接受”标头，比较响应并确定哪个标头最适合您的用例。

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

## 为合并成员资格启用架构 {#enable}

为了使架构包含在其类的合并中，必须将`union`标记添加到架构的`meta:immutableTags`属性中。 您可以通过发出PATCH请求将单个字符串值为`union`的`meta:immutableTags`数组添加到相关架构来实现这一点。 有关详细示例，请参阅[架构终结点指南](./schemas.md#union)。

## 在合并中列出架构 {#list-schemas}

要查看哪些架构是特定合并的一部分，您可以对`/tenant/schemas`端点执行GET请求。 使用`property`查询参数，您可以将响应配置为仅返回包含`meta:immutableTags`字段和`meta:class`的架构，该字段等于您正在访问其并集的类。

**API格式**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | 要列出其已启用联合的架构的类的`$id`。 |

{style="table-layout:auto"}

**请求**

以下请求检索属于[!DNL XDM Individual Profile]类的联合一部分的所有架构的列表。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于请求中发送的`Accept`标头。 以下`Accept`标头可用于列出架构：

| `Accept`标头 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每个资源的简短摘要。 这是列出资源的推荐标头。 （限制：300） |
| `application/vnd.adobe.xed+json` | 返回每个资源的完整JSON架构，包括原始`$ref`和`allOf`。 （限制：300） |

{style="table-layout:auto"}

**响应**

成功的响应将返回架构的过滤列表，其中仅包含那些属于已启用联合成员资格的指定类的架构。 请记住，使用多个查询参数时，假定使用AND关系。

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
