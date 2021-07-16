---
title: 应用程序配置端点
description: 了解如何在Reactor API中调用/app_configurations端点。
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 7%

---

# 应用程序配置端点

>[!WARNING]
>
>`/app_configurations`端点的实现在通量中，因为添加、删除和重新工作了功能。

应用程序配置允许存储和检索凭据以供日后使用。 Reactor API中的`/app_configurations`端点允许您以编程方式管理体验应用程序中的应用程序配置。

## 快速入门

本指南中使用的端点是[Reactor API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml)的一部分。 在继续操作之前，请查看[快速入门指南](../getting-started.md) ，以了解有关如何对API进行身份验证的重要信息。

## 检索应用程序配置列表 {#list}

**API格式**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| 参数 | 描述 |
| --- | --- |
| `COMPANY_ID` | 拥有应用程序配置的[公司](./companies.md)的`id`。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>使用查询参数，可以根据以下属性过滤列出的应用程序配置：<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>有关更多信息，请参阅[筛选响应](../guides/filtering.md)指南。

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/app_configurations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应会返回应用程序配置的列表。

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

您可以通过在GET请求的路径中提供应用程序配置的ID来查找该配置。

**API格式**

```http
GET /app_configurations/{APP_CONFIGURATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 要查找的应用程序配置的`id`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应会返回应用程序配置的详细信息。

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
| `COMPANY_ID` | 要在下定义应用程序配置的[公司](./companies.md)的`id`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X POST \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
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
| `platform` | 应用程序在（Web或移动设备）上运行的平台。 这可确定哪些消息传送服务可用。 |
| `messaging_service` | 与应用程序关联的消息传送服务，如[Apple推送通知服务(APNs)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html)和[Firebase Cloud Messaging(FCM)](https://firebase.google.com/docs/cloud-messaging)。 这可确定可以使用哪些键类型。 |
| `key_type` | 表示推送服务供应商支持的协议，并确定`push_credential`对象的格式。 随着报文传送服务协议的不断发展，将创建新的`key_type`值以支持更新的协议。 |
| `push_credential` | 实际凭据值，在静态时加密。 此字段通常不会解密或包含在API响应中。 只有某些Adobe服务才能获取包含解密的推送凭据的响应。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回新创建的应用程序配置的详细信息。

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

您可以通过在应用程序请求的路径中包含应用程序配置的ID来更新PUT配置。

**API格式**

```http
PUT /app_configurations/{APP_CONFIGURATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 要更新的应用程序配置的`id`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求会更新现有应用程序配置的`app_id`。

```shell
curl -X PUT \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
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
| `attributes` | 一个对象，其属性表示要为应用程序配置更新的属性。 每个键值都表示要更新的特定应用程序配置属性，以及应将其更新到的相应值。<br><br>可以为应用程序配置更新以下属性：<ul><li>`app_id`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`push_credential`</li></ul> |
| `id` | 要更新的应用程序配置的`id`。 这应该与请求路径中提供的`{APP_CONFIGURATION_ID}`值匹配。 |
| `type` | 要更新的资源类型。 对于此端点，值必须为`app_configurations`。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回更新的应用程序配置的详细信息。

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

您可以删除应用程序配置，方法是将其ID包含在DELETE请求的路径中。

**API格式**

```http
DELETE /app_configurations/{APP_CONFIGURATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 要删除的应用程序配置的`id`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**响应**

成功的响应会返回没有响应正文的HTTP状态204（无内容），表示应用程序配置已被删除。
