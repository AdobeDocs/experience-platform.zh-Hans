---
keywords: Experience Platform；首頁；熱門主題；API；屬性型存取控制；屬性型存取控制
solution: Experience Platform
title: 產品API端點
description: 屬性式存取控制API中的/products端點可讓您以程式設計方式管理Adobe Experience Platform中的產品。
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---

# 產品端點

>[!NOTE]
>
>如果傳遞的是使用者權杖，則權杖的使用者必須具有請求組織的「組織管理員」角色。

此 `/products` 屬性型存取控制API中的端點可讓您以程式設計方式管理產品，以及與組織中產品相關聯的許可權類別和許可權集。

## 快速入门

本指南中使用的API端點是以屬性為基礎的存取控制API的一部分。 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

## 擷取已授權產品的清單 {#list}

您可以透過向以下網站發出GET請求，擷取已授權產品的清單： `/products` 端點。

**API格式**

```http
GET /products/
```

**请求**

下列請求會擷取屬於您組織的已授權產品清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的回應會傳回屬於您組織的已授權產品清單。

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
| `id` | 查詢產品的對應ID。 |
| `name` | 查詢產品的名稱。 |
| `serviceCode` | 查詢產品的對應服務代碼。 |

## 依產品ID查詢許可權類別

您可以透過向「 」發出GET要求，查詢指定產品的許可權類別 `/products/{PRODUCT_ID}/categories` 端點（指定您的產品ID時）。

**API格式**

```http
GET /products/{PRODUCT_ID}/categories
```

| 参数 | 描述 |
| --- | --- |
| {PRODUCT_ID} | 與您要查閱的許可權類別相關聯的產品識別碼。 |

**请求**

以下請求會擷取與關聯的許可權類別 `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/categories \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的回應會傳回與您查詢的產品ID相關聯的許可權類別。

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
| `category` | 查詢的產品ID中可用的許可權類別。 |
| `name` | 許可權類別的名稱。 |

## 依產品ID查詢許可權集

您可以透過向以下網站發出GET要求，查詢指定產品的許可權集： `/products/{PRODUCT_ID}/permission-sets` 端點（指定您的產品ID時）。

**API格式**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| 参数 | 描述 |
| --- | --- |
| {PRODUCT_ID} | 與您要查閱的許可權集相關聯的產品的ID。 |

**请求**

以下請求會擷取與關聯的許可權集 `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/permission-sets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的回應會傳回與您查詢的產品ID相關聯的許可權集。

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
| `permission-sets` | 許可權集代表管理員可套用至角色的一組許可權。 管理員可以將許可權集指派給角色，而不是指派個別許可權。 這可讓您從包含一組許可權的預定義角色建立自訂角色。 |
| `id` | 查詢許可權集的對應ID。 |
| `name` | 查詢許可權集的對應名稱。 |
| `category` | 可用的許可權類別。 |
| `permissions` | 許可權包括檢視和/或使用Platform功能，例如建立沙箱、定義結構描述和管理資料集的能力。 |
| `permissions.resource` | 主體可以或無法存取的資產或物件。 資源可以是檔案、應用程式、伺服器，甚至API。 |
| `permissions.actions` | 允許主體對查詢的資源執行的動作。 可能的值包括： `view`， `read`， `create`， `edit`、和 `delete` |
