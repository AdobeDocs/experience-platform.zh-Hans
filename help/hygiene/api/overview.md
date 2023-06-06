---
title: 数据卫生API指南
description: 了解如何以编程方式在Adobe Experience Platform中更正或删除客户存储的个人数据。
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: da8b5d9fffdf8a176a4d70be5df5b3021cf0df7b
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# 数据卫生API指南

>[!IMPORTANT]
>
>Adobe Experience Platform中的数据卫生功能目前仅适用于已购买的组织 **AdobeHealth Shield** 或 **Adobe隐私和安全防护**.

数据卫生API允许您以编程方式更正或删除客户在Adobe Experience Platform中存储的个人数据，以及安排数据集的过期日期。 本指南介绍了使用API的先决条件步骤，并提供了指向更多特定于端点的文档的链接。

## 快速入门

您可以通过以下根路径访问数据卫生API： `https://platform.adobe.io/data/core/hygiene/`

以下各节概述了您在尝试调用API之前需要了解的核心概念。

### 收集所需标题的值

要调用数据卫生API，您必须首先收集身份验证凭据。 请遵循 [API身份验证指南](../../landing/api-authentication.md) 为数据卫生API的每个所需标头生成值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的标头：

* `Content-Type: application/json`

### 正在读取示例API调用

本文档提供了一个示例API调用，以演示如何设置请求的格式。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/api-guide.md#sample-api) 《Experience PlatformAPI快速入门指南》中的。

## 数据集过期时间

数据集到期是一种延迟的“删除数据集”操作。 通过创建数据集过期，可指定在未来的某个时间删除该数据集。 请参阅 [数据集到期端点指南](./dataset-expiration.md) 有关在API中计划数据集过期的详细信息。

## 记录删除

>[!IMPORTANT]
>
>记录删除请求仅适用于已购买的组织 **AdobeHealth Shield**.
>
>
>记录删除旨在用于数据清理、匿名数据删除或数据最小化。 它们是 **非** 用于数据主体权利请求（合规性），与通用数据保护条例(GDPR)等隐私法规相关。 对于所有合规性用例，使用 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 而是。

数据卫生API允许您在一个或所有数据集中删除与某个身份关联的所有记录。 删除身份的所有数据卫生任务都由称为工作单的构造表示。 请参阅 [工单终结点指南](./workorder.md) 有关在API中使用记录删除的详细信息。

## 配额

您的组织受限于每个类型数据卫生操作的预定每月工作配额，这可能因许可而异。 请参阅 [配额终结点指南](./quota.md) 以了解有关查看数据卫生进程的当前配额状态的详细信息。

## 后续步骤

本指南介绍了如何使用API调用管理数据卫生请求。 有关如何在Platform UI中执行这些操作的信息，请参阅 [数据卫生UI指南](../ui/overview.md).
