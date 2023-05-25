---
title: 配额API端点
description: 通过数据卫生API中的/quota端点，您可以根据组织的每个作业类型的每月配额限制监控数据卫生使用情况。
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 1c6a5df6473e572cae88a5980fe0db9dfcf9944e
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 2%

---

# 配额终结点

>[!IMPORTANT]
>
>Adobe Experience Platform中的数据卫生功能目前仅适用于已购买的组织 **AdobeHealth Shield** 或 **Adobe隐私和安全防护**.

此 `/quota` 数据卫生API中的端点允许您根据组织对每个作业类型的配额限制监控数据卫生使用情况。

通过以下方式为每个数据卫生作业类型实施配额：

* 记录删除和更新限制为每月特定数量的请求。
* 数据集过期对并发活动作业的数量有统一限制，无论何时执行过期。

## 快速入门

本指南中使用的端点属于数据卫生API。 在继续之前，请查看 [概述](./overview.md) ，以了解以下信息：

* 相关文档的链接
* 阅读本文档中的示例API调用指南
* 有关成功调用任何Experience PlatformAPI所需的标头的重要信息

## 列出配额 {#list}

您可以通过向以下网站发出GET请求，查看贵组织的配额信息： `/quota` 端点。

**API格式**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{QUOTA_TYPE}` | 指定要检索的配额类型的可选查询参数。 如果否 `quotaType` 参数，则API响应中会返回所有配额值。 接受的类型值包括：<ul><li>`expirationDatasetQuota`：数据集过期时间</li><li>`deleteIdentityWorkOrderDatasetQuota`：记录删除</li><li>`fieldUpdateWorkOrderDatasetQuota`：记录更新</li></ul> |

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

成功响应将返回数据卫生配额的详细信息。

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
      "description": "The number of Record Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `quotas` | 列出每个数据卫生作业类型的配额信息。 每个配额对象都包含以下属性：<ul><li>`name`：数据卫生作业类型：<ul><li>`expirationDatasetQuota`：数据集过期时间</li><li>`deleteIdentityWorkOrderDatasetQuota`：记录删除</li></ul></li><li>`description`：数据卫生作业类型的描述。</li><li>`consumed`：在当前每月期间运行的此类作业数。</li><li>`quota`：此作业类型的配额限制。 对于记录删除和更新，这表示每个月期间可以运行的作业数。 对于数据集过期，这表示在任意给定时间可以同时处于活动状态的作业数。</li></ul> |

{style="table-layout:auto"}
