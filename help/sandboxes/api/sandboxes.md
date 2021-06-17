---
keywords: Experience Platform；主页；热门主题；沙盒开发人员指南
solution: Experience Platform
title: 沙盒管理API端点
topic-legacy: developer guide
description: 沙盒API中的/沙盒端点允许您以编程方式管理Adobe Experience Platform中的沙盒。
source-git-commit: 1ec141fa5a13bb4ca6a4ec57f597f38802a92b3f
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 2%

---

# 沙盒管理端点

Adobe Experience Platform中的沙箱提供了独立的开发环境，允许您在不影响生产环境的情况下测试功能、运行实验和进行自定义配置。 [!DNL Sandbox] API中的`/sandboxes`端点允许您以编程方式管理Platform中的沙箱。

## 快速入门

本指南中使用的API端点是[[!DNL Sandbox] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml)的一部分。 在继续操作之前，请查阅[快速入门指南](./getting-started.md) ，以获取相关文档的链接、本文档中API调用示例的阅读指南，以及成功调用任何Experience PlatformAPI所需的标头的重要信息。

## 检索沙箱列表 {#list}

您可以通过向`/sandboxes`端点发出GET请求，列出属于您的IMS组织（活动或其他）的所有沙箱。

**API格式**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 用于按筛选结果的可选查询参数。 有关更多信息，请参阅[查询参数](./appendix.md#query)中的部分。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回属于贵组织的沙箱列表，包括`name`、`title`、`state`和`type`等详细信息。

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev-2",
            "title": "Development 2",
            "state": "creating",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-07 10:16:02",
            "lastModifiedDate": "2019-09-07 10:16:02",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 4,
        "count": 4
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes/?limit={limit}&offset={offset}",
            "templated": true
        },
        "prev": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=0&limit=1",
            "templated": null
        },
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=1&limit=1",
            "templated": null
        }
    }
}
```

| 属性 | 描述 |
| --- | --- |
| `name` | 沙盒的名称。 此属性用于API调用中的查找目的。 |
| `title` | 沙盒的显示名称。 |
| `state` | 沙盒的当前处理状态。 沙盒的状态可以是以下任一状态：<br/><ul><li>`creating`:沙盒已创建，但仍由系统进行配置。</li><li>`active`:沙盒已创建并处于活动状态。</li><li>`failed`:由于错误，系统无法配置沙盒并禁用该沙盒。</li><li>`deleted`:已手动禁用沙盒。</li></ul> |
| `type` | 沙盒类型。 当前支持的沙盒类型包括`development`和`production`。 |
| `isDefault` | 布尔属性，用于指示此沙盒是否为组织的默认生产沙盒。 |
| `eTag` | 沙盒特定版本的标识符。 对于版本控制和缓存效率，每当对沙盒进行更改时，都会更新此值。 |

## 查找沙盒 {#lookup}

您可以通过发出GET请求来查找单个沙盒，该请求在请求路径中包含沙盒的`name`属性。

**API格式**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要查找的沙盒的`name`属性。 |

**请求**

以下请求会检索名为“dev-2”的沙盒。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应会返回沙盒的详细信息，包括其`name`、`title`、`state`和`type`。

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| 属性 | 描述 |
| --- | --- |
| `name` | 沙盒的名称。 此属性用于API调用中的查找目的。 |
| `title` | 沙盒的显示名称。 |
| `state` | 沙盒的当前处理状态。 沙盒的状态可以是以下任一状态： <ul><li>**创建**:沙盒已创建，但仍由系统进行配置。</li><li>**活动**:沙盒已创建并处于活动状态。</li><li>**失败**:由于错误，系统无法配置沙盒并禁用该沙盒。</li><li>**已删除**:已手动禁用沙盒。</li></ul> |
| `type` | 沙盒类型。 当前支持的沙盒类型包括：`development`和`production`。 |
| `isDefault` | 布尔属性，用于指示此沙盒是否为组织的默认沙盒。 通常为生产沙盒。 |
| `eTag` | 沙盒特定版本的标识符。 对于版本控制和缓存效率，每当对沙盒进行更改时，都会更新此值。 |

## 创建沙盒 {#create}

您可以通过向`/sandboxes`端点发出POST请求，来创建新的开发或生产沙盒。

### 创建开发沙盒

要创建开发沙盒，必须在请求有效负载中提供值为`development`的`type`属性。

**API格式**

```http
POST /sandboxes
```

**请求**

以下请求将创建一个名为“acme-dev”的新开发沙箱。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "type": "development"
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 将用于在将来的请求中访问沙盒的标识符。 此值必须唯一，最佳做法是尽可能使其具有描述性。 此值不能包含任何空格或特殊字符。 |
| `title` | 在Platform用户界面中用于显示目的的可读名称。 |
| `type` | 要创建的沙盒类型。 对于非生产沙盒，此值必须为`development`。 |

**响应**

成功的响应会返回新创建的沙盒的详细信息，显示其`state`是“正在创建”。

```json
{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>沙盒需要大约30秒才能由系统进行配置，之后其`state`将变为“活动”或“失败”。

### 创建生产沙盒

要创建生产沙盒，必须在请求有效负载中提供值为`production`的`type`属性。

**API格式**

```http
POST /sandboxes
```

**请求**

以下请求会创建一个名为“acme”的新生产沙箱。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H `Accept: application/json` \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme",
    "title": "Acme Business Group",
    "type": "production"
}'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 将用于在将来的请求中访问沙盒的标识符。 此值必须唯一，最佳做法是尽可能使其具有描述性。 此值不能包含任何空格或特殊字符。 |
| `title` | 在Platform用户界面中用于显示目的的可读名称。 |
| `type` | 要创建的沙盒类型。 对于生产沙盒，此值必须为`production`。 |

**响应**

成功的响应会返回新创建的沙盒的详细信息，显示其`state`是“正在创建”。

```json
{
    "name": "acme",
    "title": "Acme Business Group",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```

>[!NOTE]
>
>沙盒需要大约30秒才能由系统进行配置，之后其`state`将变为“活动”或“失败”。

## 更新沙盒 {#put}

您可以通过发出PATCH请求来更新沙盒中的一个或多个字段，该请求在请求路径中包含沙盒的`name`，并且属性要在请求有效负载中进行更新。

>[!NOTE]
>
>当前只能更新沙盒的`title`属性。

**API格式**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要更新的沙盒的`name`属性。 |

**请求**

以下请求会更新名为“acme”的沙盒的`title`属性。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "title": "Acme Business Group prod"
  }'
```

**响应**

成功响应会返回HTTP状态200（确定），其中包含新更新的沙盒的详细信息。

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "active",
    "type": "production",
    "region": "VA7"
}
```

## 重置沙盒 {#reset}

沙盒具有“工厂重置”功能，可从沙盒中删除所有非默认资源。 您可以通过发出PUT请求来重置沙盒，该请求在请求路径中包含沙盒的`name`。

**API格式**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要重置的沙盒的`name`属性。 |
| `validationOnly` | 一个可选参数，允许您对沙盒重置操作进行试运行前检查，而无需发出实际请求。 将此参数设置为`validationOnly=true` ，以检查要重置的沙盒是否包含任何Adobe Analytics、Adobe Audience Manager或区段共享数据。 |

**请求**

以下请求会重置名为“acme-dev”的沙盒。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev?validationOnly=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

| 属性 | 描述 |
| --- | --- |
| `action` | 必须在请求有效负载中提供此参数，其值为“reset”，才能重置沙盒。 |

**响应**

>[!NOTE]
>
>重置沙盒后，系统大约需要30秒才能进行配置。

成功的响应会返回更新的沙盒的详细信息，表明其`state`是“重置”的。

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

如果Adobe Analytics还在为[跨设备分析(CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html)功能使用其中托管的身份图，或者如果Adobe Audience Manager也在为[基于人员的目标(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html)功能使用其中托管的身份图，则无法重置默认生产沙盒和任何用户创建的生产沙盒。

以下是可能会阻止重置沙盒的可能异常列表：

```json
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2074-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2075-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature, as well by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2076-400"
},
{
    "status": 400,
    "title": "Warning: Sandbox `{SANDBOX_NAME}` is used for bi-directional segment sharing with Adobe Audience Manager or Audience Core Service.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2077-400"
}
```

您可以通过向请求添加`ignoreWarnings`参数，继续重置用于与[!DNL Audience Manager]或[!DNL Audience Core Service]进行双向区段共享的生产沙盒。

**API格式**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要重置的沙盒的`name`属性。 |
| `ignoreWarnings` | 可选参数，用于跳过验证检查并强制重置用于与[!DNL Audience Manager]或[!DNL Audience Core Service]进行双向区段共享的生产沙盒。 此参数不能应用于默认的生产沙盒。 |

**请求**

以下请求会重置名为“acme”的生产沙箱。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

**响应**

成功的响应会返回更新的沙盒的详细信息，表明其`state`是“重置”的。

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "resetting",
    "type": "production",
    "region": "VA7"
}
```

## 删除沙盒 {#delete}

>[!IMPORTANT]
>
>无法删除默认的生产沙盒。

您可以通过发出DELETE请求来删除沙盒，请求路径中包含沙盒的`name`。

>[!NOTE]
>
>进行此API调用会将沙盒的`status`属性更新为“deleted”并停用该属性。 GET请求在删除后仍可以检索沙盒的详细信息。

**API格式**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要删除的沙盒的`name`。 |
| `validationOnly` | 一个可选参数，允许您在执行沙盒删除操作时进行试运行前检查，而无需发出实际请求。 将此参数设置为`validationOnly=true` ，以检查要重置的沙盒是否包含任何Adobe Analytics、Adobe Audience Manager或区段共享数据。 |
| `ignoreWarnings` | 可选参数，允许您跳过验证检查并强制删除用户创建的生产沙盒，该沙盒用于与[!DNL Audience Manager]或[!DNL Audience Core Service]进行双向区段共享。 此参数不能应用于默认的生产沙盒。 |

**请求**

以下请求会删除名为“acme”的生产沙箱。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**响应**

成功的响应会返回沙盒的更新详细信息，显示其`state`为“已删除”。

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
