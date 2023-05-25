---
title: 应用程序配置端点
description: 了解如何在Reactor API中调用/app_configurations端点。
exl-id: 88a1ec36-b4d2-4fb6-92cb-1da04268492a
source-git-commit: 36320addc790e844a1102314890e8692841dc5d0
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 4%

---

# 应用程序配置端点

>[!WARNING]
>
>实施 `/app_configurations` 端点在添加、删除和重新加工特征时处于动态变化状态。

应用程序配置允许存储和检索凭据以供将来使用。 此 `/app_configurations` Reactor API中的端点允许您以编程方式管理体验应用程序中的应用程序配置。

## 快速入门

本指南中使用的端点是 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/). 在继续之前，请查看 [快速入门指南](../getting-started.md) 有关如何对API进行身份验证的重要信息。

## 检索应用程序配置列表 {#list}

**API格式**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| 参数 | 描述 |
| --- | --- |
| `COMPANY_ID` | 此 `id` 的 [公司](./companies.md) 拥有应用程序配置的所有者。 |

{style="table-layout:auto"}

>[!NOTE]
>
>使用查询参数，可以根据以下属性筛选列出的应用程序配置：<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>请参阅指南，网址为 [筛选响应](../guides/filtering.md) 了解更多信息。

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

成功的响应将返回应用程序配置的列表。

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

## 查找应用程序配置 {#lookup}

您可以通过在GET请求的路径中提供其ID来查找应用程序配置。

**API格式**

```http
GET /app_configurations/{APP_CONFIGURATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 此 `id` 要查找的应用程序配置的属性。 |

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

成功响应将返回应用程序配置的详细信息。

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

## 创建应用程序配置 {#create}

您可以通过发出POST请求来创建新的应用程序配置。

**API格式**

```http
POST /companies/{COMPANY_ID}/app_configurations
```

| 参数 | 描述 |
| --- | --- |
| `COMPANY_ID` | 此 `id` 的 [公司](./companies.md) 您正在其下定义应用程序配置。 |

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
| `platform` | 应用程序运行所在的平台（Web或移动设备）。 这决定了可用的报文传送服务。 |
| `messaging_service` | 与应用程序关联的消息服务，例如 [Apple推送通知服务(APN)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) 和 [Firebase Cloud Messaging (FCM)](https://firebase.google.com/docs/cloud-messaging). 这决定了可以使用哪些键类型。 |
| `key_type` | 表示推送服务供应商支持的协议并确定的格式 `push_credential` 对象。 随着报文传送服务的协议不断发展，新的 `key_type` 创建值以支持更新的协议。 |
| `push_credential` | 静态加密的实际凭据值。 此字段通常不会解密或包含在API响应中。 只有某些Adobe服务才能获得包含解密推送凭据的响应。 |

{style="table-layout:auto"}

**响应**

成功响应将返回新创建的应用程序配置的详细信息。

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

## 更新应用程序配置

您可以通过在PATCH请求的路径中包含应用程序ID来更新应用程序配置。

**API格式**

```http
PATCH /app_configurations/{APP_CONFIGURATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 此 `id` 要更新的应用程序配置的属性。 |

{style="table-layout:auto"}

**请求**

以下请求将更新 `app_id` 对于现有应用程序配置。

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
| `attributes` | 一个对象，其属性表示要针对应用程序配置更新的属性。 每个键代表要更新的特定应用程序配置属性以及应更新到的相应值。<br><br>可以为应用程序配置更新以下属性：<ul><li>`app_id`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`push_credential`</li></ul> |
| `id` | 此 `id` 要更新的应用程序配置的属性。 这应该与 `{APP_CONFIGURATION_ID}` 请求路径中提供的值。 |
| `type` | 正在更新的资源类型。 对于此端点，值必须为 `app_configurations`. |

{style="table-layout:auto"}

**响应**

成功响应将返回更新的应用程序配置的详细信息。

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

## 删除应用程序配置

您可以在DELETE请求的路径中包含应用程序配置ID来删除该应用程序配置。

**API格式**

```http
DELETE /app_configurations/{APP_CONFIGURATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 此 `id` 要删除的应用程序配置的属性。 |

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

成功的响应返回HTTP状态204（无内容），没有响应正文，这表示应用程序配置已被删除。
