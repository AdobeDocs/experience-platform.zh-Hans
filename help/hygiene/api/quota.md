---
title: 配额API端点
description: 通过数据卫生API中的/quota端点，您可以根据组织的每个作业类型的每月配额限制监控高级数据生命周期管理的使用情况。
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 2c2907c5ed38ce4c87b1b73f96e1a0e64586cb97
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 2%

---

# 配额终结点

使用数据卫生API中的`/quota`端点检查您组织的当前使用情况和限制。 配额因权利而异，例如Privacy and Security Shield或Healthcare Shield。

监视当前配额消耗，以确保符合每个作业类型的组织限制。

## 快速入门

本指南中使用的端点属于数据卫生API。 在继续之前，请查看[概述](./overview.md)以了解以下信息：

* 相关文档链接
* 如何读取示例API调用
* Experience Platform API调用所需的标头

## 配额和处理时间线 {#quotas}

记录删除请求受基于您的许可证授权的配额和服务级别期望值约束。 这些限制同时适用于基于UI和基于API的删除请求。

>[!TIP]
>
>本文档说明如何根据基于权利的限制查询您的使用情况。 有关配额层、记录删除权利和SLA行为的完整说明，请参阅基于[UI的记录删除](../ui/record-delete.md#quotas)或基于[API的记录删除](./workorder.md#quotas)文档。

## 列出配额 {#list}

您可通过向`/quota`端点发出GET请求来查看组织的配额信息。

**API格式**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

>[!NOTE]
>
>配额使用情况会在每月的第一天00:00 GMT进行每日和每月重置。
>
>只有接受的请求才计入您的配额。 被拒绝的工作单不会减少您的配额。

| 参数 | 描述 |
| --- | --- |
| `{QUOTA_TYPE}` | 一个可选的查询参数，它指定要检索的配额类型。 如果未提供`quotaType`参数，则API响应中会返回所有配额值。 接受的值包括：<ul><li>`datasetExpirationQuota`：活动数据集过期的数量和您的总允许。</li><li>`dailyConsumerDeleteIdentitiesQuota`：今天删除的记录数和每日配额。</li><li>`monthlyConsumerDeleteIdentitiesQuota`：本月删除的记录数和您的每月配额。</li></ul> |

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

成功的响应将返回数据生命周期配额的详细信息。

```json
{
  "quotas": [
    {
      "name": "datasetExpirationQuota",
      "description": "The number of concurrently active dataset-expiration delete operations in all work order requests for the organization.",
      "consumed": 11,
      "quota": 75
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization for today.",
      "consumed": 314,
      "quota": 700000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization this month.",
      "consumed": 2764,
      "quota": 12000000
    }
  ]
}
```

| 属性 | 描述 |
| -------- | ------- |
| `quotas` | 列出每个数据生命周期作业类型的配额信息。 每个配额对象包含以下属性：<ul><li>`name`</li><li>`description`</li><li>`consumed`</li><li>`quota`</li></ul> |
| `name` | 配额类型标识符。 |
| `description` | 此配额限制的描述。 |
| `consumed` | 当前使用的配额量。 对于每日配额，使用量将于当月1日重置为00:00 GMT和00:00 GMT。 |
| `quota` | 贵组织此配额类型的最大配额。 |
