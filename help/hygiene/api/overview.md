---
title: 数据卫生API指南
description: 了解如何以编程方式更正或删除客户在Adobe Experience Platform中存储的个人数据。
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 1%

---

# 数据卫生API指南

>[!IMPORTANT]
>
>Adobe Experience Platform中的数据卫生功能目前仅适用于已购买Healthcare Shield的组织。

数据卫生API允许您以编程方式更正或删除客户在Adobe Experience Platform中存储的个人数据，并为数据集计划生存时间(TTL)协议。 本指南介绍了使用API的先决步骤，并提供了指向更多特定于端点的文档的链接。

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

<!-- ## Work orders

A work order is a representation of a data hygiene task that deletes consumer identities from a specific dataset or all datasets. See the [work order endpoint guide](./workorder.md) for details on working with work orders in the API. -->

## 数据集的生存时间(TTL)

数据集TTL是一项时间延迟的“删除数据集”操作。 通过创建TTL，您可以指定将来应删除该数据集的时间。 请参阅 [数据集TTL端点指南](./ttl.md) 有关在API中计划数据集TTL的详细信息。

## 后续步骤

本指南介绍了如何使用API调用管理数据卫生请求。 有关如何在Platform UI中执行这些操作的信息，请参阅 [数据卫生UI指南](../ui/overview.md).
