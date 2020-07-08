---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 目录服务开发人员指南
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# 目录服务开发人员指南

目录服务是Adobe Experience Platform内数据位置和谱系的记录系统。 Catalog充当元数据存储或“目录”，您可以在Experience Platform中查找有关数据的信息，而无需访问数据本身。 有关更多 [信息](../home.md) ，请参阅目录概述。

此开发人员指南提供帮助您使用目录API进行开始的步骤。 然后，该指南提供了使用Catalog执行关键操作的示例API调用。

## 先决条件

目录跟踪Experience Platform中几种资源和操作的元数据。 本开发人员指南要求您对创建和管理这些资源所涉及的各种Experience Platform服务有一个有效的了解：

* [体验数据模型(XDM)](../../xdm/home.md): 平台组织客户体验数据的标准化框架。
* [批量摄取](../../ingestion/batch-ingestion/overview.md): Experience Platform如何从数据文件（如CSV和Parke）中摄取和存储数据。
* [流摄取](../../ingestion/streaming-ingestion/overview.md): Experience Platform如何从客户端和服务器端设备实时摄取和存储数据。

以下各节提供您需要了解或掌握的其他信息，以便成功调用目录服务API。

## 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的章节。

## 收集所需标题的值

要调用平台API，您必须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* 授权： 承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都隔离到特定虚拟沙箱。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

* 内容类型： application/json

## 目录API调用的最佳实践

在对目录API执行GET请求时，最佳实践是在请求中包含查询参数，以便仅返回所需的对象和属性。 未过滤的请求可能导致响应有效负载超过3GB，从而降低整体性能。

您可以通过将特定对象的ID包含在请求路径中来视图特定对象，或使用查询参数(如 `properties` 和筛 `limit` 选响应)。 过滤器可以作为标题和查询参数传递，而传递的查询参数优先。 有关详细信息，请 [参阅筛选目录数](filter-data.md) 据文档。

由于某些查询可以对API进行大量加载，因此已对目录查询实施全局限制以进一步支持最佳实践。

## 后续步骤

此文档涵盖调用目录API所需的必备知识。 您现在可以继续访问本开发人员指南中提供的示例调用，并按照其说明进行操作。

本指南中的大多数示例都使用 `/dataSets` 端点，但这些原则可以应用于目录中的其他端点(如 `/batches` 和 `/accounts`)。 有关每个 [端点可用的所有调用](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) 和操作的完整列表，请参阅目录服务API参考。

有关演示目录API如何与数据摄取相关的分步工作流，请参阅有关创建数据集 [的教程](../datasets/create.md)。
