---
title: 使用数据卫生API删除记录
description: 了解如何在Adobe Experience Platform中以编程方式更正或删除客户存储的个人数据。
role: Developer
hide: true
hidefromtoc: true
exl-id: d80a4be3-e072-4bb4-a56d-b34a20f88c78
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 5%

---

# 使用数据卫生API删除记录

<!-- >[!IMPORTANT]
>
>This endpoint represents the beta functionality for record deletes. For the latest functionality, please use the [`/workorder` endpoint](./workorder.md) instead. -->

数据卫生API允许您以编程方式更正或删除客户在Adobe Experience Platform中存储的个人数据。

您可以通过与[Privacy Service API](../../privacy-service/api/overview.md)相同的根路径访问该API： `https://platform.adobe.io/data/core/privacy/`

## 快速入门

本节介绍了在尝试调用数据卫生API之前需要了解的核心概念。

### 收集所需标头的值

要调用数据卫生API，您必须首先收集身份验证凭据。 这些是用于访问Privacy Service API的相同凭据。 请参阅[API概述](./overview.md#getting-started)，为数据卫生API的每个所需标头生成值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

包含负载 (POST、PUT、PATCH) 的所有请求都需要额外的标头：

* `Content-Type: application/json`

### 正在读取示例 API 调用

本文档提供了一个示例API调用，用于演示如何格式化请求。 有关示例API调用文档中使用的约定的信息，请参阅Experience Platform API快速入门指南中有关[如何读取示例API调用](../../landing/api-guide.md#sample-api)的部分。

## 创建删除作业

您可以通过发出POST请求来创建删除作业。

**API格式**

```http
POST /jobs
```

**请求**

请求有效负载的结构与Privacy Service API[&#128279;](../../privacy-service/api/privacy-jobs.md#access-delete)中删除请求的有效负载类似。 它包含一个`users`数组，其对象表示要删除其数据的用户。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{ORG_ID}"
          }
        ],
        "users": [
          {
            "key": "John Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "email",
                "value": "johnd@example.com",
                "type": "standard",
              },
              {
                "namespace": "ECID",
                "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
                "type": "standard"
              }
            ]
          },
          {
            "key": "Jane Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "Loyalty ID",
                "value": "30583967185734",
                "type": "custom"
              }
            ]
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `companyContexts` | 包含您组织的身份验证信息的数组。 它必须包含具有以下属性的单个对象： <ul><li>`namespace`：必须设置为`imsOrgID`。</li><li>`value`：您的组织ID。 此值与`x-gw-ims-org-id`标头中提供的值相同。</li></ul> |
| `users` | 一个数组，其中包含您要删除其信息的至少一个用户的集合。 每个用户对象包含以下信息： <ul><li>`key`：用于限定响应数据中各个作业ID的用户的标识符。 最好为此值选择一个唯一的、易于识别的字符串，以便稍后可以引用或查找。</li><li>`action`：一个数组，列出了要对用户数据执行的所需操作。 必须包含单个字符串值： `delete`。</li><li>`userIDs`：用户的标识集合。 单个用户可以拥有的身份数限制为9个。 每个标识都包含以下属性： <ul><li>`namespace`：与ID关联的[身份命名空间](../../identity-service/features/namespaces.md)。 这可以是Experience Platform识别的[标准命名空间](../../privacy-service/api/appendix.md#standard-namespaces)，也可以是您的组织定义的自定义命名空间。 使用的命名空间类型必须反映在`type`属性中。</li><li>`value`：标识值。</li><li>`type`：如果使用全局可识别的命名空间，则必须设置为`standard`；如果使用组织定义的命名空间，则必须设置为`custom`。</li></ul></li></ul> |

{style="table-layout:auto"}

**响应**

成功的响应将返回已创建作业的详细信息。

```json
{
  "requestId": "16318094870430026RX-334",
  "totalRecords": 2,
  "jobs": [
    {
      "jobId": "c9b5fd82-db14-4c27-8bec-64a06e1fbda4",
      "customer": {
        "user": {
          "key": "John Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "email",
              "value": "johnd@example.com",
              "type": "standard",
              "namespaceId": 6,
              "isDeletedClientSide": false
            },
            {
              "namespace": "ECID",
              "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
              "type": "standard",
              "namespaceId": 4,
              "isDeletedClientSide": false
            }
          ]
        }
      }
    },
    {
      "jobId": "8ddc8e73-cecc-4be3-ae44-cdba127f7c70",
      "customer": {
        "user": {
          "key": "Jane Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "Loyalty ID",
              "value": "30583967185734",
              "type": "custom",
              "isDeletedClientSide": false
            }
          ]
        }
      }
    }
  ]
}
```
