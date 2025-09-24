---
title: 数据卫生API指南
description: 了解如何在Adobe Experience Platform中以编程方式更正或删除客户存储的个人数据。
role: Developer
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 8aa8a1c42e9656716be746ba447a5f77a8155b4c
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 6%

---

# 数据卫生API指南

数据卫生API允许您以编程方式更正或删除客户在Adobe Experience Platform中存储的个人数据，以及安排数据集的到期日期。 本指南介绍了使用API的先决步骤，并提供了指向更多特定于端点的文档的链接。

## 快速入门

您可以通过以下根路径访问数据卫生API： `https://platform.adobe.io/data/core/hygiene/`

以下各节概述了您在尝试调用API之前需要了解的核心概念。

### 收集所需标头的值

要调用数据卫生API，您必须首先收集身份验证凭据。 按照[API身份验证指南](../../landing/api-authentication.md)为数据卫生API的每个必需标头生成值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

包含负载 (POST、PUT、PATCH) 的所有请求都需要额外的标头：

* `Content-Type: application/json`

### 正在读取示例 API 调用

本文档提供了一个示例API调用，用于演示如何格式化请求。 有关示例API调用文档中使用的约定的信息，请参阅Experience Platform API快速入门指南中有关[如何读取示例API调用](../../landing/api-guide.md#sample-api)的部分。

## 数据集有效期限

数据集到期是一种时间延迟的“删除数据集”操作。 通过创建数据集过期，您可以指定在未来的某个时间删除该数据集。 有关在API中安排数据集过期时间的详细信息，请参阅[数据集过期端点指南](./dataset-expiration.md)。

## 记录删除

>[!IMPORTANT]
>
>记录删除旨在用于数据清理、匿名数据删除或数据最小化。 它们&#x200B;**不是**&#x200B;用于数据主体权利请求（合规性），因为它与《通用数据保护条例》(GDPR)等隐私法规相关。 对于所有合规性用例，请改用[Adobe Experience Platform Privacy Service](../../privacy-service/home.md)。

数据卫生API允许您在一个或所有数据集中删除与某个身份关联的所有记录。 所有删除身份的数据生命周期任务均由称为工作单的构造表示。 有关在API中使用记录删除的详细信息，请参阅[工作单终结点指南](./workorder.md)。

## 配额

您的组织受限于每个类型的数据生命周期操作的预定每月任务配额，该配额可能因许可而有所不同。 有关查看数据生命周期进程的当前配额状态的详细信息，请参阅[配额终结点指南](./quota.md)。

## 后续步骤

本指南介绍了如何使用API调用管理数据生命周期请求。 有关如何在Experience Platform UI中执行这些操作的信息，请参阅[数据生命周期UI指南](../ui/overview.md)。
