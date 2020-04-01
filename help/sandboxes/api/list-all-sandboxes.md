---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 列表所有沙箱
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c

---


# 列表所有沙箱

要列表属于您的IMS组织（活动或其他）的所有沙箱，请向端点发出GET请 `/sandboxes` 求。

**API格式**

```http
GET /sandboxes
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回属于您组织的一列表沙箱，包括诸如、 `name`、 `title`和 `state`等详细信息 `type`。

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
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `name` | 沙箱的名称。 用于API调用中的查找用途。 |
| `title` | 沙箱的显示名称。 |
| `state` | 沙箱的当前处理状态。 沙箱的状态可以是以下任一状态： <br/><ul><li>**创建**:沙箱已创建，但系统仍在提供。</li><li>**活动**:沙箱已创建且处于活动状态。</li><li>**失败**:由于出错，沙箱无法由系统提供并被禁用。</li><li>**已删除**:沙箱已手动禁用。</li></ul> |
| `type` | 沙箱类型，“开发”或“生产”。 |
| `isDefault` | 指示此沙箱是否为组织的默认沙箱的布尔属性。 通常，这是生产沙箱。 |
| `eTag` | 沙箱特定版本的标识符。 用于版本控制和缓存效率，该值在每次对沙箱进行更改时都会更新。 |
