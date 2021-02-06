---
keywords: Experience Platform；主页；热门主题；列表活动沙箱；列表沙箱
solution: Experience Platform
title: 列表API中当前用户的活动沙箱
topic: developer guide
description: 您可以通过向根端点发出列表请求来GET当前用户处于活动状态的沙箱。
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 2%

---


# 列表API中当前用户的活动沙箱

>[!NOTE]
>
>与沙箱API中提供的其他端点不同，此端点可用于所有用户，包括那些没有沙箱管理访问权限的用户。

您可以通过向根(`/`)端点发出列表请求，来GET当前用户处于活动状态的沙箱。

**API格式**

```http
GET /{QUERY_PARAMS}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 可选查询参数，用于筛选结果。 有关详细信息，请参见[查询参数](#query)一节。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回当前用户处于活动状态的沙箱列表，包括诸如`name`、`title`、`state`和`type`等详细信息。

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
| `name` | 沙箱的名称。 用于API调用中的查找目的。 |
| `title` | 沙箱的显示名称。 |
| `state` | 沙箱的当前处理状态。 沙箱的状态可以是以下任一状态： <ul><li>**创建**:沙箱已创建，但系统仍在提供。</li><li>**活动**:沙箱已创建并处于活动状态。</li><li>**失败**:由于出错，沙箱无法由系统提供并被禁用。</li><li>**已删除**:已手动禁用沙箱。</li></ul> |
| `type` | 沙箱类型，“开发”或“生产”。 |
| `isDefault` | 一个布尔属性，用于指示此沙箱是否是组织的默认沙箱。 通常，这是生产沙箱。 |
| `eTag` | 沙箱的特定版本的标识符。 用于版本控制和缓存效率，每次对沙箱进行更改时都会更新此值。 |

## 使用查询参数{#query}

[[!DNL Sandbox]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) API支持在列出沙箱时使用查询参数进行页面和筛选结果。

>[!NOTE]
>
>必须同时指定`limit`和`offset`查询参数。 如果仅指定一个，API将返回错误。 如果指定无，则默认限制为50，偏移为0。

| 参数 | 描述 |
| --------- | ----------- |
| `limit` | 响应中要返回的最大记录数。 |
| `offset` | 从第一个记录到响应开始（偏移）的实体数。 |
