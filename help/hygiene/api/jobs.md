---
title: 使用数据卫生API删除记录
description: 了解如何以编程方式更正或删除客户在Adobe Experience Platform中存储的个人数据。
hide: true
hidefromtoc: true
exl-id: d80a4be3-e072-4bb4-a56d-b34a20f88c78
source-git-commit: da8b5d9fffdf8a176a4d70be5df5b3021cf0df7b
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---

# 使用数据卫生API删除记录

>[!IMPORTANT]
>
>此端点表示用于记录删除的测试版功能。 要获取最新功能，请使用 [`/workorder` 端点](./workorder.md) 中。

数据卫生API允许您以编程方式更正或删除客户在Adobe Experience Platform中存储的个人数据。

您可以通过与 [Privacy ServiceAPI](../../privacy-service/api/overview.md): `https://platform.adobe.io/data/core/privacy/`

## 快速入门

本节简要介绍在尝试调用数据卫生API之前需要了解的核心概念。

### 收集所需标题的值

要调用数据卫生API，您必须先收集身份验证凭据。 这些凭据与用于访问Privacy ServiceAPI的凭据相同。 请参阅 [API概述](./overview.md#getting-started) 为数据卫生API的每个所需标头生成值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

* `Content-Type: application/json`

### 读取示例API调用

本文档提供了一个示例API调用，用于演示如何设置请求的格式。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/api-guide.md#sample-api) 中的Experience PlatformAPI快速入门指南。

## 创建删除作业

您可以通过发出删除请求来创建POST作业。

**API格式**

```http
POST /jobs
```

**请求**

请求有效负载的结构与请求有效负载的结构类似 [删除API中的Privacy Service请求](../../privacy-service/api/privacy-jobs.md#access-delete). 它包括 `users` 其对象表示要删除其数据的用户的数组。

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
| `companyContexts` | 包含贵组织的身份验证信息的数组。 它必须包含具有以下属性的单个对象： <ul><li>`namespace`:必须设置为 `imsOrgID`.</li><li>`value`:您的IMS组织ID。 此值与 `x-gw-ims-org-id` 标题。</li></ul> |
| `users` | 一个数组，其中包含至少一个用户的集合，您要删除其信息。 每个用户对象包含以下信息： <ul><li>`key`:用户的标识符，用于限定响应数据中单独的作业ID。 最好为此值选择一个唯一且易于识别的字符串，以便以后可以引用或查找该字符串。</li><li>`action`:一个数组，其中列出了对用户数据执行的所需操作。 必须包含单个字符串值： `delete`.</li><li>`userIDs`:用户的标识集合。 单个用户可以拥有的身份数量最多为9个。 每个标识都包含以下属性： <ul><li>`namespace`:的 [标识命名空间](../../identity-service/namespaces.md) 与ID关联。 这可以是 [标准命名空间](../../privacy-service/api/appendix.md#standard-namespaces) 可由平台识别，或者它可以是由您的组织定义的自定义命名空间。 使用的命名空间类型必须反映在 `type` 属性。</li><li>`value`:标识值。</li><li>`type`:必须设置为 `standard` 如果使用全局识别的命名空间，或 `custom` 如果您使用的是由您的组织定义的命名空间。</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回已创建作业的详细信息。

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
