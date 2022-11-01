---
title: 配额API端点
description: 利用数据卫生API中的/quota端点，可根据组织针对每种作业类型的每月配额限制来监控数据卫生使用情况。
source-git-commit: 6453ec6c98d90566449edaa0804ada260ae12bf6
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 3%

---

# 配额端点

>[!IMPORTANT]
>
>Adobe Experience Platform中的数据卫生功能目前仅适用于已购买的组织 **Adobe医疗保健盾** 或 **Adobe隐私和安全防护**.

的 `/quota` 数据卫生API中的端点允许您根据组织针对每种作业类型的配额限制监控数据卫生使用情况。

每种数据卫生作业类型的配额通过以下方式强制执行：

* 用户删除和字段更新限制为每月发送一定数量的请求。
* 数据集过期对并发活动作业的数量具有固定限制，无论何时执行过期。

## 快速入门

本指南中使用的端点是数据卫生API的一部分。 在继续之前，请查看 [概述](./overview.md) 以下信息：

* 相关文档的链接
* 本文档中有关读取示例API调用的指南
* 有关成功调用任何Experience PlatformAPI所需标头的重要信息

## 列出配额 {#list}

您可以通过向 `/quota` 端点。

**API格式**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{QUOTA_TYPE}` | 可选查询参数，用于指定要检索的配额类型。 如果否 `quotaType` 参数，则API响应中会返回所有配额值。 接受的类型值包括：<ul><li>`expirationDatasetQuota`:数据集过期</li><li>`deleteIdentityWorkOrderDatasetQuota`:用户删除</li><li>`fieldUpdateWorkOrderDatasetQuota`:字段更新</li></ul> |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/quota \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
```

**响应**

成功的响应会返回数据卫生配额的详细信息。

```json
{
  "quotas": [
    {
      "name": "expirationDatasetQuota",
      "description": "The number of concurrently active Expiration Dataset Delete Work Order requests for the organization.",
      "consumed": 3154,
      "quota": 10000
    },
    {
      "name": "deleteIdentityWorkOrderQuota",
      "description": "The number of Consumer Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `quotas` | 列出每个数据卫生作业类型的配额信息。 每个配额对象都包含以下属性：<ul><li>`name`:数据卫生作业类型：<ul><li>`expirationDatasetQuota`:数据集过期</li><li>`deleteIdentityWorkOrderDatasetQuota`:用户删除</li></ul></li><li>`description`:数据卫生作业类型的描述。</li><li>`consumed`:此类型的作业在当前每月期间运行。</li><li>`quota`:此作业类型的配额限制。 对于消费者删除和字段更新，此值表示每月可运行的作业数。 对于数据集过期，此值表示在任何给定时间可同时处于活动状态的作业数。</li></ul> |

{style=&quot;table-layout:auto&quot;}
