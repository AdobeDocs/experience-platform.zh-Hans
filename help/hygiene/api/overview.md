---
title: 数据卫生API指南
description: 了解如何以编程方式更正或删除客户在Adobe Experience Platform中存储的个人数据。
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 7679de9d30c00873b279c5315aa652870d8c34fd
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# 数据卫生API指南

>[!IMPORTANT]
>
>Adobe Experience Platform中的数据卫生功能目前仅适用于已购买的组织 **Adobe医疗保健盾** 或 **Adobe隐私和安全防护**.

数据卫生API允许您以编程方式更正或删除客户在Adobe Experience Platform中存储的个人数据，并计划数据集的过期日期。 本指南介绍了使用API的先决步骤，并提供了指向更多特定于端点的文档的链接。

## 快速入门

您可以通过以下根路径访问数据卫生API: `https://platform.adobe.io/data/core/hygiene/`

以下各节概述了在尝试调用API之前需要了解的核心概念。

### 收集所需标题的值

要调用数据卫生API，您必须先收集身份验证凭据。 关注 [API身份验证指南](../../landing/api-authentication.md) 为数据卫生API的每个所需标头生成值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

* `Content-Type: application/json`

### 读取示例API调用

本文档提供了一个示例API调用，用于演示如何设置请求的格式。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/api-guide.md#sample-api) 中的Experience PlatformAPI快速入门指南。

## 数据集过期

数据集过期是一项时间延迟的“删除数据集”操作。 通过创建数据集过期，您可以指定将来应删除该数据集的时间。 请参阅 [数据集过期端点指南](./dataset-expiration.md) 有关在API中计划数据集过期的详细信息。

## 消费者删除

>[!IMPORTANT]
>
>消费者删除请求仅适用于已购买的组织 **Adobe医疗保健盾**.
>
>
>消费者删除用于数据清理、删除匿名数据或数据最小化。 是 **not** 用于与《通用数据保护条例》(GDPR)等隐私法规相关的数据主体权利请求（合规）。 对于所有法规遵从性用例，请使用 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 中。

数据卫生API允许您删除一个或多个数据集中与消费者身份关联的所有记录。 所有删除消费者身份的数据卫生任务都由称为工作单的结构来代表。 请参阅 [《工作单终端指南》](./workorder.md) 有关在API中使用消费者删除的详细信息。

## 配额

贵组织针对每种类型的数据卫生操作限制为预定的每月工作配额，具体操作类型可能因许可而异。 请参阅 [配额端点指南](./quota.md) 有关查看数据卫生流程的当前配额状态的详细信息。

## 后续步骤

本指南介绍了如何使用API调用管理数据卫生请求。 有关如何在Platform UI中执行这些操作的信息，请参阅 [数据卫生UI指南](../ui/overview.md).
