---
keywords: Experience Platform；主页；热门主题；沙盒开发人员指南
solution: Experience Platform
title: 沙盒管理API端点
description: 沙盒API中的/沙盒端点允许您以编程方式管理Adobe Experience Platform中的沙盒。
exl-id: 0ff653b4-3e31-4ea5-a22e-07e18795f73e
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 3%

---

# 沙盒管理端点

Adobe Experience Platform中的沙箱提供了独立的开发环境，允许您在不影响生产环境的情况下测试功能、运行实验和进行自定义配置。 的 `/sandboxes` 的端点 [!DNL Sandbox] API允许您以编程方式管理Platform中的沙箱。

## 快速入门

本指南中使用的API端点是 [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). 在继续之前，请查看 [入门指南](./getting-started.md) 有关相关文档的链接，请参阅本文档中的API调用示例指南，以及有关成功调用任何Experience PlatformAPI所需标头的重要信息。

## 检索沙箱列表 {#list}

您可以通过向 `/sandboxes` 端点。

**API格式**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 用于按筛选结果的可选查询参数。 请参阅 [查询参数](./appendix.md#query) 以了解更多信息。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回属于贵组织的沙箱列表，包括详细信息，例如 `name`, `title`, `state`和 `type`.

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
| `state` | 沙盒的当前处理状态。 沙盒的状态可以是以下任一状态： <br/><ul><li>`creating`:沙盒已创建，但仍由系统进行配置。</li><li>`active`:沙盒已创建并处于活动状态。</li><li>`failed`:由于错误，系统无法配置沙盒并禁用该沙盒。</li><li>`deleted`:已手动禁用沙盒。</li></ul> |
| `type` | 沙盒类型。 当前支持的沙盒类型包括 `development` 和 `production`. |
| `isDefault` | 布尔属性，用于指示此沙盒是否为组织的默认生产沙盒。 |
| `eTag` | 沙盒特定版本的标识符。 对于版本控制和缓存效率，每当对沙盒进行更改时，都会更新此值。 |

## 查找沙盒 {#lookup}

您可以通过发出包含沙盒的GET请求来查找单个沙盒 `name` 属性。

**API格式**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 的 `name` 要查找的沙盒的属性。 |

**请求**

以下请求会检索名为“dev-2”的沙盒。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的响应会返回沙盒的详细信息，包括 `name`, `title`, `state`和 `type`.

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
| `type` | 沙盒类型。 当前支持的沙盒类型包括： `development` 和 `production`. |
| `isDefault` | 布尔属性，用于指示此沙盒是否为组织的默认沙盒。 通常为生产沙盒。 |
| `eTag` | 沙盒特定版本的标识符。 对于版本控制和缓存效率，每当对沙盒进行更改时，都会更新此值。 |

## 创建沙盒 {#create}

>[!NOTE]
>
>创建新沙盒后，必须首先将该新沙盒添加到 [Adobe Admin Console](https://adminconsole.adobe.com/) 才能开始使用新沙盒。 请参阅 [管理产品配置文件的权限](../../access-control/ui/permissions.md) 有关如何向产品用户档案配置沙盒的信息。

您可以通过向 `/sandboxes` 端点。

### 创建开发沙盒

要创建开发沙盒，您必须提供 `type` 值为 `development` 在请求有效负载中。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `type` | 要创建的沙盒类型。 对于非生产沙盒，此值必须为 `development`. |

**响应**

成功的响应会返回新创建的沙盒的详细信息，以显示其 `state` 是“正在创建”。

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
>沙盒需要大约30秒才能由系统进行配置，之后系统会设置沙盒 `state` 将变为“活动”或“失败”。

### 创建生产沙盒

要创建生产沙盒，您必须提供 `type` 值为 `production` 在请求有效负载中。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `type` | 要创建的沙盒类型。 对于生产沙盒，此值必须为 `production`. |

**响应**

成功的响应会返回新创建的沙盒的详细信息，以显示其 `state` 是“正在创建”。

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
>沙盒需要大约30秒才能由系统进行配置，之后系统会设置沙盒 `state` 将变为“活动”或“失败”。

## 更新沙盒 {#put}

您可以通过发出包含沙盒的PATCH请求来更新沙盒中的一个或多个字段 `name` 在请求路径和属性中，要在请求有效负载中进行更新。

>[!NOTE]
>
>当前仅为沙盒的 `title` 属性。

**API格式**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 的 `name` 要更新的沙盒的属性。 |

**请求**

以下请求更新了 `title` 名为“acme”的沙盒的属性。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

沙盒具有“工厂重置”功能，可从沙盒中删除所有非默认资源。 您可以通过发出包含沙盒的PUT请求来重置沙盒 `name` 在请求路径中。

**API格式**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 的 `name` 要重置的沙盒的属性。 |
| `validationOnly` | 一个可选参数，允许您对沙盒重置操作进行试运行前检查，而无需发出实际请求。 将此参数设置为 `validationOnly=true` 用于检查要重置的沙盒是否包含任何Adobe Analytics、Adobe Audience Manager或区段共享数据。 |

**请求**

以下请求会重置名为“acme-dev”的沙盒。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev?validationOnly=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功的响应会返回更新的沙盒的详细信息，以表明其 `state` 为“正在重置”。

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

如果Adobe Analytics还在将默认生产沙盒和任何用户创建的生产沙箱用作 [跨设备分析(CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) 功能，或者如果在其中托管的身份图表也由Adobe Audience Manager用于 [基于人员的目标(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html) 功能。

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

您可以继续重置用于与共享双向区段的生产沙盒 [!DNL Audience Manager] 或 [!DNL Audience Core Service] 通过添加 `ignoreWarnings` 参数。

**API格式**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 的 `name` 要重置的沙盒的属性。 |
| `ignoreWarnings` | 可选参数，用于跳过验证检查并强制重置用于与共享双向区段的生产沙盒 [!DNL Audience Manager] 或 [!DNL Audience Core Service]. 此参数不能应用于默认的生产沙盒。 |

**请求**

以下请求会重置名为“acme”的生产沙箱。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

**响应**

成功的响应会返回更新的沙盒的详细信息，以表明其 `state` 为“正在重置”。

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

您可以通过发出包含沙盒的DELETE请求来删除沙盒 `name` 在请求路径中。

>[!NOTE]
>
>发出此API调用会更新沙盒的 `status` 属性，并将其停用。 GET请求在删除后仍可以检索沙盒的详细信息。

**API格式**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 的 `name` 的沙盒。 |
| `validationOnly` | 一个可选参数，允许您在执行沙盒删除操作时进行试运行前检查，而无需发出实际请求。 将此参数设置为 `validationOnly=true` 用于检查要重置的沙盒是否包含任何Adobe Analytics、Adobe Audience Manager或区段共享数据。 |
| `ignoreWarnings` | 一个可选参数，允许您跳过验证检查并强制删除用户创建的生产沙盒，该沙盒用于与 [!DNL Audience Manager] 或 [!DNL Audience Core Service]. 此参数不能应用于默认的生产沙盒。 |

**请求**

以下请求会删除名为“acme”的生产沙箱。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功的响应会返回沙盒的更新详细信息，显示 `state` 为“已删除”。

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
