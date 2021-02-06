---
keywords: Experience Platform；主页；热门主题；沙箱；沙箱
solution: Experience Platform
title: 在API中创建沙箱
topic: developer guide
description: 可以通过向“/沙箱”端点发出POST请求来创建新沙箱。
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 2%

---


# 在API中创建沙箱

可以通过向`/sandboxes`端点发出POST请求来创建新沙箱。

**API格式**

```http
POST /sandboxes
```

**请求**

以下请求将创建一个名为“dev-3”的新开发沙箱。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 将来请求中用于访问沙箱的标识符。 此值必须是唯一的，最佳实践是使其尽可能具有描述性。 不能包含任何空格或大写字母。 |
| `title` | 用于平台用户界面中显示目的的可读名称。 |
| `type` | 要创建的沙箱类型。 目前，组织只能创建“开发”类型沙箱。 |

**响应**

成功的响应会返回新创建的沙箱的详细信息，显示其`state`是“creating”。

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>沙箱需要大约15分钟才能由系统进行配置，之后其`state`将变为“活动”或“失败”。
