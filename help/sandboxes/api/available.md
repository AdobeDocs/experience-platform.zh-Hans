---
keywords: Experience Platform；主页；热门主题；列出可用沙盒；列出沙盒
solution: Experience Platform
title: 可用沙盒API端点
description: 您可以通过对可用沙盒端点发出GET请求来列出当前用户可用的沙盒。
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
source-git-commit: 130f3a9b65befc1cc8cf400b8ca8ca4d6e7f71e4
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 2%

---

# 可用沙盒端点

>[!NOTE]
>
>与沙盒API中提供的其他端点不同，此端点适用于所有用户，包括没有沙盒管理访问权限的用户。

您可以通过对可用沙盒端点发出GET请求来列出当前用户可用的沙盒。

**API格式**

```http
GET /{QUERY_PARAMS}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 用于筛选结果的可选查询参数。 请参阅 [附录文档](./appendix.md#query) 以获取可用参数的列表。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功的响应将返回可用于当前用户的沙盒列表，包括详细信息，例如 `name`， `title`， `state`、和 `type`.

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
        }
    ],
    "_page": {
        "limit": 3,
        "count": 1
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/?limit={limit}&offset={offset}",
            "templated": true
        }
    }
}
```

| 属性 | 描述 |
| --- | --- |
| `name` | 沙盒的名称。 用于API调用中的查找目的。 |
| `title` | 沙盒的显示名称。 |
| `state` | 沙盒的当前处理状态。 沙盒的状态可以是以下任一状态： <ul><li>`creating`：沙盒已创建，但仍由系统配置。</li><li>`active`：沙盒已创建并处于活动状态。</li><li>`failed`：由于错误，沙盒无法由系统配置并被禁用。</li><li>`deleted`：已手动禁用沙盒。</li></ul> |
| `type` | 沙盒类型：“开发”或“生产”。 |
| `isDefault` | 布尔属性，指示此沙盒是否为组织的默认生产沙盒。 |
| `eTag` | 沙盒的特定版本的标识符。 用于版本控制和缓存效率，每次对沙盒进行更改时都会更新此值。 |
