---
keywords: Experience Platform；主页；热门主题；沙箱；沙箱
solution: Experience Platform
title: 在API中创建沙箱
topic: 开发人员指南
description: 可以通过向“/沙箱”端点发出POST请求来创建新沙箱。
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 2%

---


# 在API中创建沙箱

可以通过向`/sandboxes`端点发出POST请求来创建开发或生产沙箱。

## 创建开发沙箱

要创建开发沙箱，请向`/sandboxes`端点发出POST请求，并为属性`type`提供值`development`。

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
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 将来请求中用于访问沙箱的标识符。 此值必须是唯一的，最佳实践是尽可能使其具有描述性。 此值不能包含任何空格或特殊字符。 |
| `title` | 用于平台用户界面中显示目的的可读名称。 |
| `type` | 要创建的沙箱类型。 `type`属性的值可以是开发或生产。 |

**响应**

成功的响应返回新创建的沙箱的详细信息，表明其`state`是“creating”。

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

## 创建生产沙箱

>[!NOTE]
>
>“多个制作沙箱”功能是测试版。

要创建生产沙箱，请向`/sandboxes`端点发出POST请求，并为属性`type`提供值`production`。

**API格式**

```http
POST /sandboxes
```

**请求**

以下请求将创建一个名为“test-prod-sandbox”的新生产沙箱。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "test-prod-sandbox",
    "title": "Test Production Sandbox",
    "type": "production"
}'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 将来请求中用于访问沙箱的标识符。 此值必须是唯一的，最佳实践是尽可能使其具有描述性。 此值不能包含任何空格或特殊字符。 |
| `title` | 用于平台用户界面中显示目的的可读名称。 |
| `type` | 要创建的沙箱类型。 `type`属性的值可以是开发或生产。 |

**响应**

成功的响应返回新创建的沙箱的详细信息，表明其`state`是“creating”。

```json
{
    "name": "test-production-sandbox",
    "title": "Test Production Sandbox",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```
