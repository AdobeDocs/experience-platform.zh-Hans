---
keywords: Experience Platform；主页；热门主题；API；基于属性的访问控制；基于属性的访问控制
solution: Experience Platform
title: 产品API端点
description: 基于属性的访问控制API中的/products端点允许您以编程方式管理Adobe Experience Platform中的产品。
role: Developer
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# 产品端点

>[!NOTE]
>
>如果传递的是用户令牌，则该令牌的用户必须具有所请求组织的“组织管理员”角色。

基于属性的访问控制API中的`/products`端点允许您以编程方式管理产品以及与组织中的产品关联的权限类别和权限集。

## 快速入门

本指南中使用的API端点属于基于属性的访问控制API。 在继续之前，请查看[快速入门指南](./getting-started.md)，以获取相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience Platform API所需的所需标头的重要信息。

## 检索授权产品的列表 {#list}

您可以通过向`/products`端点发出GET请求来检索授权产品的列表。

**API格式**

```http
GET /products/
```

**请求**

以下请求会检索属于您组织的授权产品的列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应将返回属于您组织的授权产品的列表。

```json
{
  "products": [
    {
      "id": "{ID}",
      "name": "Adobe Experience Platform",
      "serviceCode": "{SERVICE_CODE}"
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 查询的产品的对应ID。 |
| `name` | 查询产品的名称。 |
| `serviceCode` | 所查询产品的相应服务代码。 |

## 按产品ID查找权限类别

您可以查找给定产品的权限类别，方法是在指定产品ID时向`/products/{PRODUCT_ID}/categories`端点发出GET请求。

**API格式**

```http
GET /products/{PRODUCT_ID}/categories
```

| 参数 | 描述 |
| --- | --- |
| {PRODUCT_ID} | 与要查找的权限类别关联的产品的ID。 |

**请求**

以下请求检索与`{PRODUCT_ID}`关联的权限类别。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/categories \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应将返回与您查询的产品ID关联的权限类别。

```json
{
  "categories": [
    {
        "name": "Profile Management"
    },
    {
        "name": "Data Ingestion"
    },
    {
        "name": "Sandbox Administration"
    },
    {
        "name": "Query Service"
    },
    {
        "name": "Data Management"
    },
    {
        "name": "Identity Management"
    },
    {
        "name": "Data Modeling"
    },
    {
        "name": "Data Science Workspace"
    },
    {
        "name": "Dashboards"
    },
    {
        "name": "Alerts"
    },
    {
        "name": "Data Governance"
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `category` | 查询的产品ID中可用的权限类别。 |
| `name` | 权限类别的名称。 |

## 按产品ID查找权限集

您可以在指定产品ID时通过向`/products/{PRODUCT_ID}/permission-sets`端点发出GET请求来查找给定产品的权限集。

**API格式**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| 参数 | 描述 |
| --- | --- |
| {PRODUCT_ID} | 与要查找的权限集关联的产品的ID。 |

**请求**

以下请求检索与`{PRODUCT_ID}`关联的权限集。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/permission-sets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应将返回与您查询的产品ID关联的权限集。

```json
{
  "permission-sets": [
      {
          "id": "manage-schemas",
          "name": "Manage Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
      {
          "id": "view-schemas",
          "name": "View Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `permission-sets` | 权限集表示管理员可以应用于角色的一组权限。 管理员可以为角色分配权限集，而不是分配单个权限。 这允许您从包含一组权限的预定义角色创建自定义角色。 |
| `id` | 查询的权限集的对应ID。 |
| `name` | 查询的权限集的相应名称。 |
| `category` | 可用的权限类别。 |
| `permissions` | 权限包括查看和/或使用Experience Platform功能的功能，例如创建沙盒、定义架构和管理数据集。 |
| `permissions.resource` | 主体可以或无法访问的资源或对象。 资源可以是文件、应用程序、服务器甚至API。 |
| `permissions.actions` | 允许主体对查询的资源执行的操作。 可能的值包括： `view`、`read`、`create`、`edit`和`delete` |
