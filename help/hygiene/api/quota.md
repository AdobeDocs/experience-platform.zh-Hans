---
title: 配额API端点
description: 通过数据卫生API中的/quota端点，您可以根据组织的每个作业类型的每月配额限制监控高级数据生命周期管理的使用情况。
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 4d34ae1885f8c4b05c7bb4ff9de9c0c0e26154bd
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# 配额终结点

数据卫生API中的`/quota`端点允许您根据组织对每个作业类型的配额限制监控高级数据生命周期管理的使用情况。

跟踪每个数据生命周期作业类型的配额使用情况。 您的实际配额限制取决于您组织的权利并可定期审查。 数据集过期时间受并发活动作业数量的硬限制。

## 快速入门

本指南中使用的端点属于数据卫生API。 在继续之前，请查看[概述](./overview.md)以了解以下信息：

* 相关文档的链接
* 本文档中有关阅读示例API调用的指南
* 有关调用任何Experience Platform API所需的标头的重要信息

## 配额和处理时间线 {#quotas}

记录删除请求受基于您的许可证授权的配额和服务级别期望值约束。 这些限制同时适用于基于UI和基于API的删除请求。

>[!TIP]
> 
>本文档说明如何根据基于权利的限制查询您的使用情况。 有关配额层、记录删除权限和SLA行为的完整说明，请参阅基于[UI的记录删除](../ui/record-delete.md#quotas)或基于[API的记录删除](./workorder.md#quotas)文档。

## 列出配额 {#list}

您可通过向`/quota`端点发出GET请求来查看组织的配额信息。

**API格式**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{QUOTA_TYPE}` | 一个可选的查询参数，它指定要检索的配额类型。 如果未提供`quotaType`参数，则API响应中会返回所有配额值。 接受的类型值包括：<ul><li>`datasetExpirationQuota`：此对象显示贵组织并发活动数据集过期的数量，以及您的总允许过期时间。 </li><li>`dailyConsumerDeleteIdentitiesQuota`：此对象显示贵组织今天发出的记录删除请求总数和每日津贴总额。<br>注意：只计算已接受的请求。 如果工作单因验证失败而被拒绝，则这些标识删除不会计入您的配额。</li><li>`monthlyConsumerDeleteIdentitiesQuota`：此对象显示贵组织本月发出的记录删除请求总数和每月津贴总额。</li><li>`monthlyUpdatedFieldIdentitiesQuota`：此对象显示贵组织本月发出的记录更新请求总数和每月津贴总额。</li></ul> |

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
      "description": "The number of concurrently active Expiration Dataset Delete in all workorder requests for the organization.",
      "consumed": 12,
      "quota": 50
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for today.",
      "consumed": 0,
      "quota": 1000000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for this month.",
      "consumed": 841,
      "quota": 2000000
    },
    {
      "name": "monthlyUpdatedFieldIdentitiesQuota",
      "description": "The consumed number of updated identities in all workorder requests for the organization for this month.",
      "consumed": 0,
      "quota": 0
    }
  ]
}
```

| 属性 | 描述 |
| -------- | ------- |
| `quotas` | 列出每个数据生命周期作业类型的配额信息。 每个配额对象包含以下属性：<ul><li>`name`：数据生命周期作业类型：<ul><li>`expirationDatasetQuota`：数据集过期</li><li>`deleteIdentityWorkOrderDatasetQuota`：记录删除</li></ul></li><li>`description`：数据生命周期作业类型的描述。</li><li>`consumed`：在当前时段中运行的此类型的作业数。 对象名称指示配额周期。</li><li>`quota`：贵组织此作业类型的配额。 对于记录删除和更新，配额表示每个月期间可以运行的作业数。 对于数据集过期，配额表示在任意给定时间可同时处于活动状态的作业数。</li></ul> |
