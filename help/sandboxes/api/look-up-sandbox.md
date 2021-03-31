---
keywords: Experience Platform；主页；热门主题；查找沙箱；查找沙箱
solution: Experience Platform
title: 在API中查找沙箱
topic: 开发人员指南
description: 可以通过发出一个GET请求来查找单个沙箱，该请求在请求路径中包含沙箱的name属性。
translation-type: tm+mt
source-git-commit: ca3de18c093d7b692b582045afea4401d7133b9b
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 2%

---


# 在API中查找沙箱

可以通过发出GET请求来查找单个沙箱，该请求在请求路径中包含沙箱的`name`属性。

**API格式**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要查找的沙箱的`name`属性。 |

**请求**

以下请求检索名为“dev-2”的沙箱。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应返回沙箱的详细信息，包括沙箱的`name`、`title`、`state`和`type`。

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
| `name` | 沙箱的名称。 用于API调用中的查找目的。 |
| `title` | 沙箱的显示名称。 |
| `state` | 沙箱的当前处理状态。 沙箱的状态可以是以下任一状态： <ul><li>**创建**:沙箱已创建，但系统仍在提供。</li><li>**活动**:沙箱已创建并处于活动状态。</li><li>**失败**:由于出错，系统无法设置沙箱并禁用沙箱。</li><li>**已删除**:已手动禁用沙箱。</li></ul> |
| `type` | 沙箱类型，“开发”或“生产”。 |
| `isDefault` | 一个布尔属性，指示此沙箱是否是组织的默认沙箱。 通常，这是生产沙箱。 |
| `eTag` | 沙箱的特定版本的标识符。 用于版本控制和缓存效率，每次对沙箱进行更改时都会更新此值。 |