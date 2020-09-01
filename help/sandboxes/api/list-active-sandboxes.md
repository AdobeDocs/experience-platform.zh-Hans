---
keywords: Experience Platform;home;popular topics;list active sandboxes;list sandboxes
solution: Experience Platform
title: 列表当前用户的活动沙箱
topic: developer guide
description: 您可以通过向根端点发出列表请求来GET当前用户处于活动状态的沙箱。
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 1%

---


# 列表当前用户的活动沙箱

>[!NOTE]
>
>与沙箱API中提供的其他端点不同，此端点可用于所有用户，包括那些没有沙箱管理访问权限的用户。

可以通过向根()端点发出列表请求来GET当前用户处于活动状态的沙`/`箱。

**API格式**

```http
GET /
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回当前用户处于活动状态的列表沙箱，包括诸如、 `name`、 `title`和 `state`等详细信息 `type`。

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
    ]
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
