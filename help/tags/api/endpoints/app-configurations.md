---
title: 應用程式設定端點
description: 瞭解如何在Reactor API中呼叫/app_configurations端點。
exl-id: 88a1ec36-b4d2-4fb6-92cb-1da04268492a
source-git-commit: 36320addc790e844a1102314890e8692841dc5d0
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 4%

---

# 應用程式設定端點

>[!WARNING]
>
>實作 `/app_configurations` 端點會隨著特徵的加入、移除和重新加工而變動。

應用程式設定可儲存及擷取認證，以供日後使用。 此 `/app_configurations` Reactor API中的端點可讓您以程式設計方式管理體驗應用程式內的應用程式設定。

## 快速入门

本指南中使用的端點是 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/). 在繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 有關如何向API驗證的重要資訊。

## 擷取應用程式設定清單 {#list}

**API格式**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| 参数 | 描述 |
| --- | --- |
| `COMPANY_ID` | 此 `id` 的 [公司](./companies.md) 擁有應用程式設定的使用者。 |

{style="table-layout:auto"}

>[!NOTE]
>
>您可以使用查詢引數，根據下列屬性篩選列出的應用程式設定：<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>請參閱指南： [篩選回應](../guides/filtering.md) 以取得詳細資訊。

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/app_configurations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功回應會傳回應用程式設定清單。

```json
{
  "data": [
    {
      "id": "AC40c339ab80d24c958b90d67b698602eb",
      "type": "app_configurations",
      "attributes": {
        "created_at": "2020-12-14T17:31:10.626Z",
        "updated_at": "2020-12-14T17:31:10.626Z",
        "app_id": "com.adobe.test_app",
        "name": "Kessel Apns App",
        "platform": "mobile",
        "messaging_service": "apns",
        "key_type": "p8_file"
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## 查詢應用程式設定 {#lookup}

您可以在GET請求的路徑中提供其ID，以查詢應用程式設定。

**API格式**

```http
GET /app_configurations/{APP_CONFIGURATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 此 `id` ，屬於您要查閱的應用程式設定。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功回應會傳回應用程式設定的詳細資料。

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## 建立應用程式設定 {#create}

您可以發出POST要求，以建立新的應用程式設定。

**API格式**

```http
POST /companies/{COMPANY_ID}/app_configurations
```

| 参数 | 描述 |
| --- | --- |
| `COMPANY_ID` | 此 `id` 的 [公司](./companies.md) 您正於下方定義應用程式設定。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X POST \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Apns App",
            "app_id": "com.adobe.test_app",
            "platform": "mobile",
            "messaging_service": "apns",
            "key_type": "p8_file",
            "push_credential": {
              "bundleId": "com.adobe.test_app",
              "keyId": "{KEY_ID}",
              "p8": "{SECRET}",
              "teamId": "{TEAM_ID}"
            }
          },
          "type": "app_configurations"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `platform` | 應用程式執行所在的平台（網頁或行動裝置）。 這會決定可用的傳訊服務。 |
| `messaging_service` | 與應用程式相關聯的訊息服務，例如 [Apple推播通知服務(APN)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) 和 [Firebase Cloud Messaging (FCM)](https://firebase.google.com/docs/cloud-messaging). 這會決定可以使用哪些索引鍵型別。 |
| `key_type` | 代表推送服務廠商支援的通訊協定，並決定 `push_credential` 物件。 隨著通訊協定的發展，訊息服務將不斷更新， `key_type` 建立值以支援更新的通訊協定。 |
| `push_credential` | 靜態加密的實際認證值。 此欄位通常不會解密或包含在API回應中。 只有特定的Adobe服務才能取得包含解密推送認證的回應。 |

{style="table-layout:auto"}

**响应**

成功的回應會傳回新建立的應用程式設定的詳細資料。

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## 更新應用程式設定

您可以在PATCH請求的路徑中包含應用程式的ID來更新應用程式設定。

**API格式**

```http
PATCH /app_configurations/{APP_CONFIGURATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 此 `id` ，屬於您要更新的應用程式設定。 |

{style="table-layout:auto"}

**请求**

以下請求會更新 `app_id` 適用於現有應用程式設定。

```shell
curl -X PATCH \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "app_id": "com.adobe.test_app_2"
          },
          "id": "AC40c339ab80d24c958b90d67b698602eb",
          "type": "app_configurations"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `attributes` | 物件，其屬性代表應用程式設定中要更新的屬性。 每個索引鍵代表要更新的特定應用程式設定屬性，以及應更新到的對應值。<br><br>可針對應用程式設定更新下列屬性：<ul><li>`app_id`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`push_credential`</li></ul> |
| `id` | 此 `id` 要更新的應用程式設定。 這應該符合 `{APP_CONFIGURATION_ID}` 請求路徑中提供的值。 |
| `type` | 正在更新的資源型別。 此端點的值必須為 `app_configurations`. |

{style="table-layout:auto"}

**响应**

成功回應會傳回已更新應用程式設定的詳細資料。

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:21.787Z",
      "app_id": "com.adobe.test_app_2",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## 刪除應用程式設定

您可以在DELETE請求的路徑中包含應用程式的ID以刪除應用程式設定。

**API格式**

```http
DELETE /app_configurations/{APP_CONFIGURATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 此 `id` 要刪除的應用程式設定的ID。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回HTTP狀態204 （無內容），沒有回應內文，表示應用程式設定已刪除。
