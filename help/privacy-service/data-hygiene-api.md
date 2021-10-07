---
title: 数据卫生API(Alpha)
description: 了解如何以编程方式更正或删除客户在Adobe Experience Platform中存储的个人数据。
hide: true
hidefromtoc: true
source-git-commit: dd8978566730975f0bde36f3af490cd33362b3ba
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 1%

---

# 数据卫生API(Alpha)

>[!IMPORTANT]
>
>数据卫生API当前位于alpha中，且您的组织可能尚未访问该API。 本文档中描述的功能可能会发生更改。

数据卫生API允许您以编程方式更正或删除客户在Adobe Experience Platform中存储的个人数据。 与Privacy ServiceAPI不同，这些操作不需要与法律隐私法规关联，并且只能用于保持数据干净准确。

## 快速入门

本节简要介绍在尝试调用数据卫生API之前需要了解的核心概念。

### 收集所需标题的值

要调用数据卫生API，您必须先收集身份验证凭据。 这些凭据与用于访问Privacy ServiceAPI的凭据相同。 按照Privacy ServiceAPI的[入门指南](./api/getting-started.md)为数据卫生API的每个所需标头生成值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

* `Content-Type: application/json`

### 读取示例API调用

本文档提供了一个示例API调用，用于演示如何设置请求的格式。 有关示例API调用文档中使用的约定的信息，请参阅Experience PlatformAPI快速入门指南中[如何阅读示例API调用](../landing/api-guide.md#sample-api)一节。

## 创建删除作业

您可以通过发出删除请求来创建POST作业。

**API格式**

```http
POST /jobs
```

**请求**

请求负载的结构与Privacy ServiceAPI](./api/privacy-jobs.md#access-delete)中[删除请求的结构类似。 它包括一个`users`数组，其对象表示要删除其数据的用户。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{IMS_ORG}"
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
| `companyContexts` | 包含贵组织的身份验证信息的数组。 它必须包含具有以下属性的单个对象： <ul><li>`namespace`:必须设置为 `imsOrgID`。</li><li>`value`:您的IMS组织ID。该值与`x-gw-ims-org-id`标头中提供的值相同。</li></ul> |
| `users` | 一个数组，其中包含至少一个用户的集合，您要删除其信息。 每个用户对象包含以下信息： <ul><li>`key`:用户的标识符，用于限定响应数据中单独的作业ID。最好为此值选择一个唯一且易于识别的字符串，以便以后可以引用或查找该字符串。</li><li>`action`:一个数组，其中列出了对用户数据执行的所需操作。必须包含单个字符串值：`delete`。</li><li>`userIDs`:用户的标识集合。单个用户可以拥有的身份数量最多为9个。 每个标识都包含以下属性： <ul><li>`namespace`:与 [ID](../identity-service/namespaces.md) 关联的身份名称包。这可以是平台可识别的[标准命名空间](./api/appendix.md#standard-namespaces)，也可以是您的组织定义的自定义命名空间。 使用的命名空间类型必须反映在`type`属性中。</li><li>`value`:标识值。</li><li>`type`:如果使用全局识 `standard` 别的命名空间，或者您使 `custom` 用的是由您的组织定义的命名空间，则必须将设置为。</li></ul></li></ul> |

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
