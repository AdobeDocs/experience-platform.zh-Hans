---
title: 配置文件端点
description: 了解如何在Reactor API中调用/profiles端点。
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 5%

---

# 配置文件端点

在Reactor API中，配置文件表示Adobe Experience Platform用户。 Reactor API不维护其自己的用户和权限Adobe库，而是依赖由[Adobe的身份管理系统(IMS)](https://helpx.adobe.com/cn/enterprise/using/identity.html)管理的ID。

配置文件包含有关已登录用户的所有信息，包括其所属的所有IMS组织、其所属的每个组织中的产品配置文件，以及他们从每个产品配置文件中拥有的权限。

## 快速入门

本指南中使用的端点是[Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)的一部分。 在继续操作之前，请查看[快速入门指南](../getting-started.md) ，以了解有关如何对API进行身份验证的重要信息。

## 检索当前配置文件 {#lookup}

通过向`/profile`端点发出GET请求，可以检索当前已登录配置文件的详细信息。

**API格式**

```http
GET /profile
```

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应会返回用户档案的详细信息。

```json
{
  "data": {
    "id": "UR0bd696624e844d6ba5bfc248ba1eca11",
    "type": "users",
    "attributes": {
      "active_org": "{IMS_ORG_1}",
      "expires_in": 0,
      "display_name": "John Smith",
      "job_function": null,
      "email": "jsmith@example.com",
      "organizations": {
        "{IMS_ORG_1}": {
          "name": "Example IMS Org A",
          "admin": true,
          "active": true,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_audiencemanager_int",
            "dma_tartan",
            "dma_dtm",
            "dma_reactor",
            "dma_auditor"
          ],
          "tenant_id": "{TENANT_ID_1}"
        },
        "{IMS_ORG_2}": {
          "name": "Example IMS Org B",
          "admin": false,
          "active": false,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_reactor",
            "dma_auditor",
            "dma_tartan"
          ],
          "tenant_id": "{TENANT_ID_2}"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/profile"
    },
    "meta": {
      "rights": [
        "manage_companies"
      ]
    }
  }
}
```

