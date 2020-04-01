---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 目录服务开发人员指南
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# 目录服务开发人员指南

Catalog Service是Adobe Experience Platform中用于数据位置和世系的记录系统。 Catalog充当元数据存储或“目录”，您可以在Experience Platform中查找有关数据的信息，而无需访问数据本身。 有关详细 [信息，请参阅](../home.md) “目录”概述。

此开发人员指南提供了帮助您使用目录API进行开始的步骤。 然后，该指南提供了使用Catalog执行键操作的示例API调用。

## 先决条件

Catalog跟踪Experience Platform中几种资源和操作的元数据。 此开发人员指南需要对创建和管理这些资源所涉及的各种Experience Platform服务有良好的了解：

* [体验数据模型(XDM)](../../xdm/home.md):平台通过标准化框架组织客户体验数据。
* [批量摄取](../../ingestion/batch-ingestion/overview.md):Experience Platform如何从CSV和Parke等数据文件摄取和存储数据。
* [流摄取](../../ingestion/streaming-ingestion/overview.md):Experience Platform如何从客户端和服务器端设备实时摄取和存储数据。

以下各节提供了成功调用目录服务API所需了解或现有的其他信息。

## 读取示例API调用

本指南提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

## 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权：承载人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

* 内容类型：application/json

## 目录API调用的最佳实践

在对目录API执行GET请求时，最佳实践是在请求中包含查询参数，以便仅返回所需的对象和属性。 未过滤的请求可能导致响应负载大小超过3GB，从而降低总体性能。

您可以通过将特定对象的ID包含在请求路径中来视图这些对象，或使用查询参数（如和） `properties` 来筛选 `limit` 响应。 过滤器可以作为标题和查询参数传递，而作为查询参数传递的参数优先。 有关详细信息，请参 [阅筛选目录数据文档](filter-data.md) 。

由于某些查询可以对API进行大量加载，因此已对目录查询实施全局限制以进一步支持最佳做法。

## 后续步骤

本文档涵盖了调用目录API所需的入门知识。 您现在可以继续阅读本开发人员指南中提供的示例调用，并按照其说明进行操作。

本指南中的大多数示例都使用端 `/dataSets` 点，但这些原则可以应用于目录内的其他端点(如和 `/batches` ) `/accounts`。 有关每个 [端点可用的所有调用和操作的完整列表](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) ，请参阅Catalog Service API参考。

有关演示目录API如何与数据摄取相关的分步工作流，请参阅有关创建数据集 [的教程](../datasets/create.md)。
