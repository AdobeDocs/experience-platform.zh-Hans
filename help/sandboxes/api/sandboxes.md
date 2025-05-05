---
keywords: Experience Platform；主页；热门主题；沙盒开发人员指南
solution: Experience Platform
title: 沙盒管理API端点
description: 沙盒API中的/sandboxes端点允许您在Adobe Experience Platform中以编程方式管理沙盒。
role: Developer
exl-id: 0ff653b4-3e31-4ea5-a22e-07e18795f73e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 3%

---

# 沙盒管理端点

Adobe Experience Platform中的沙盒提供了独立的开发环境，允许您在不影响生产环境的情况下测试功能、运行实验以及进行自定义配置。 [!DNL Sandbox] API中的`/sandboxes`端点允许您以编程方式管理Experience Platform中的沙盒。

## 快速入门

本指南中使用的API端点是[[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox)的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)，以获取相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience Platform API所需的所需标头的重要信息。

## 检索沙盒列表 {#list}

通过向`/sandboxes`端点发出GET请求，您可以列出属于您组织的所有沙盒（处于活动状态或其他状态）。

**API格式**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 用于筛选结果的可选查询参数。 有关详细信息，请参阅[查询参数](./appendix.md#query)上的部分。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的响应返回属于您组织的沙盒列表，包括`name`、`title`、`state`和`type`等详细信息。

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
| `state` | 沙盒的当前处理状态。 沙盒的状态可以是以下任一状态： <br/><ul><li>`creating`：已创建沙盒，但系统仍在配置该沙盒。</li><li>`active`：沙盒已创建并处于活动状态。</li><li>`failed`：由于错误，沙盒无法由系统配置，因此被禁用。</li><li>`deleted`：已手动禁用沙盒。</li></ul> |
| `type` | 沙盒类型。 当前支持的沙盒类型包括`development`和`production`。 |
| `isDefault` | 布尔属性，指示此沙盒是否为组织的默认生产沙盒。 |
| `eTag` | 沙盒的特定版本的标识符。 用于版本控制和缓存效率，每次对沙盒进行更改时都会更新此值。 |

## 查找沙盒 {#lookup}

您可以通过发出在请求路径中包含沙盒的`name`属性的GET请求来查找单个沙盒。

**API格式**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要查找的沙盒的`name`属性。 |

**请求**

以下请求检索名为“dev-2”的沙盒。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的响应返回沙盒的详细信息，包括其`name`、`title`、`state`和`type`。

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
| `state` | 沙盒的当前处理状态。 沙盒的状态可以是以下任一状态： <ul><li>**正在创建**：沙盒已创建，但系统仍在配置该沙盒。</li><li>**活动**：沙盒已创建并处于活动状态。</li><li>**失败**：由于错误，沙盒无法由系统配置，因此被禁用。</li><li>**已删除**：沙盒已被手动禁用。</li></ul> |
| `type` | 沙盒类型。 当前支持的沙盒类型包括： `development`和`production`。 |
| `isDefault` | 布尔属性，指示此沙盒是否为组织的默认沙盒。 通常，这是生产沙盒。 |
| `eTag` | 沙盒的特定版本的标识符。 用于版本控制和缓存效率，每次对沙盒进行更改时都会更新此值。 |

## 创建沙盒 {#create}

>[!NOTE]
>
>创建新沙盒时，您必须首先将该新沙盒添加到[Adobe Admin Console](https://adminconsole.adobe.com/)中的产品配置文件中，然后才能开始使用新沙盒。 有关如何将沙盒预配到产品配置文件的信息，请参阅有关[管理产品配置文件的权限](../../access-control/ui/permissions.md)的文档。

您可以通过向`/sandboxes`端点发出POST请求来创建新的开发或生产沙盒。

### 创建开发沙盒

要创建开发沙盒，您必须在请求有效负载中提供值为`development`的`type`特性。

**API格式**

```http
POST /sandboxes
```

**请求**

以下请求创建一个名为“acme-dev”的新开发沙盒。

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
| `name` | 将在未来请求中用于访问沙盒的标识符。 该值必须唯一，最佳做法是使其尽可能具有描述性。 此值不能包含任何空格或特殊字符。 |
| `title` | 易于用户识别的名称，用于在Experience Platform用户界面中进行显示。 |
| `type` | 要创建的沙盒的类型。 对于非生产沙盒，此值必须为`development`。 |

**响应**

成功的响应返回新创建的沙盒的详细信息，表明其`state`正在“创建”。

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
>系统配置沙盒大约需要30秒，之后其`state`将变为“活动”或“失败”。

### 创建生产沙盒

要创建生产沙盒，您必须在请求有效负载中提供值为`production`的`type`特性。

**API格式**

```http
POST /sandboxes
```

**请求**

以下请求创建一个名为“acme”的新生产沙盒。

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
| `name` | 将在未来请求中用于访问沙盒的标识符。 该值必须唯一，最佳做法是使其尽可能具有描述性。 此值不能包含任何空格或特殊字符。 |
| `title` | 易于用户识别的名称，用于在Experience Platform用户界面中进行显示。 |
| `type` | 要创建的沙盒的类型。 对于生产沙盒，此值必须为`production`。 |

**响应**

成功的响应返回新创建的沙盒的详细信息，表明其`state`正在“创建”。

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
>系统配置沙盒大约需要30秒，之后其`state`将变为“活动”或“失败”。

## 更新沙盒 {#put}

您可以通过发出PATCH请求（请求路径中包含沙盒的`name`以及在请求有效载荷中要更新的属性）来更新沙盒中的一个或多个字段。

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

以下请求更新名为“acme”的沙盒的`title`属性。

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

成功的响应返回HTTP状态200 （确定）以及新更新的沙盒的详细信息。

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

沙盒具有“工厂重置”功能，可从沙盒中删除所有非默认资源。 您可以通过发出在请求路径中包含沙盒的`name`的PUT请求来重置沙盒。

**API格式**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要重置的沙盒的`name`属性。 |
| `validationOnly` | 一个可选参数，允许您对沙盒重置操作执行预检而不发出实际请求。 将此参数设置为`validationOnly=true`以检查您即将重置的沙盒是否包含任何Adobe Analytics、Adobe Audience Manager或区段共享数据。 |

**请求**

以下请求重置名为“acme-dev”的沙盒。

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
| `action` | 必须在请求有效负载中提供值为“reset”的此参数，才能重置沙盒。 |

**响应**

>[!NOTE]
>
>沙盒重置后，系统配置沙盒大约需要30秒。

成功的响应返回已更新沙盒的详细信息，表明其`state`正在“重置”。

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

如果Adobe Analytics也在其中托管的身份图形用于[Cross Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=zh-Hans)功能，或者Adobe Audience Manager也在其中托管的身份图形用于[基于人员的目标(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=zh-Hans)功能，则无法重置默认生产沙盒和任何用户创建的生产沙盒。

以下是可阻止沙盒重置的可能异常列表：

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

您可以继续重置用于与[!DNL Audience Manager]或[!DNL Audience Core Service]进行双向区段共享的生产沙盒，方法是将`ignoreWarnings`参数添加到您的请求。

**API格式**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要重置的沙盒的`name`属性。 |
| `ignoreWarnings` | 一个可选参数，允许您跳过验证检查并强制重置用于与[!DNL Audience Manager]或[!DNL Audience Core Service]双向区段共享的生产沙盒。 此参数无法应用于默认的生产沙盒。 |

**请求**

以下请求重置名为“acme”的生产沙盒。

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

成功的响应返回已更新沙盒的详细信息，表明其`state`正在“重置”。

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

您可以通过在请求路径中包含沙盒的`name`来发出DELETE请求，以删除沙盒。

>[!NOTE]
>
>进行此API调用会将沙盒的`status`属性更新为“已删除”并停用它。 删除沙盒后，GET请求仍可以检索沙盒的详细信息。

**API格式**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要删除的沙盒的`name`。 |
| `validationOnly` | 一个可选参数，允许您对沙盒删除操作进行预检而不发出实际请求。 将此参数设置为`validationOnly=true`以检查您即将重置的沙盒是否包含任何Adobe Analytics、Adobe Audience Manager或区段共享数据。 |
| `ignoreWarnings` | 一个可选参数，允许您跳过验证检查并强制删除用于与[!DNL Audience Manager]或[!DNL Audience Core Service]双向区段共享的用户创建的生产沙盒。 此参数无法应用于默认的生产沙盒。 |

**请求**

以下请求删除名为“acme”的生产沙盒。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功的响应返回沙盒的更新详细信息，表明其`state`已“删除”。

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
