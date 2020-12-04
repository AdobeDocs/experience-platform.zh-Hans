---
keywords: Experience Platform;home;popular topics;catalog service;catalog;Catalog service;Catalog
solution: Experience Platform
title: 目录服务开发人员指南
topic: developer guide
description: 此开发人员指南提供帮助您使用目录API进行开始的步骤。 然后，该指南提供了使用Catalog执行关键操作的示例API调用。
translation-type: tm+mt
source-git-commit: c8e53a25c5b22e8d840658fe26ff47875947a6d0
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---


# [!DNL Catalog Service] 开发人员指南

[!DNL Catalog Service] 是Adobe Experience Platform境内数据定位和谱系记录系统。 [!DNL Catalog] 充当元数据存储或“目录”，您可以在其中找到有关数据的信息， [!DNL Experience Platform]无需访问数据本身。 See the [[!DNL Catalog] overview](../home.md) for more information.

此开发人员指南提供帮助您使用API进行开始 [!DNL Catalog] 的步骤。 然后，该指南提供了使用执行关键操作的示例API调 [!DNL Catalog]用。

## 先决条件

[!DNL Catalog] 跟踪中几种资源和操作的元数据 [!DNL Experience Platform]。 本开发人员指南需要对创建和管理这些 [!DNL Experience Platform] 资源所涉及的各种服务有一个有效的了解：

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。
* [批量摄取](../../ingestion/batch-ingestion/overview.md):如何 [!DNL Experience Platform] 从数据文件（如CSV和Parke）中摄取和存储数据。
* [流摄取](../../ingestion/streaming-ingestion/overview.md):如 [!DNL Experience Platform] 何从客户端和服务器端设备实时摄取和存储数据。

以下各节提供了成功调用API所需或现有的其他信 [!DNL Catalog Service] 息。

## 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

## 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

* 授权：承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

* 内容类型：application/json

## API调用的 [!DNL Catalog] 最佳实践

执行对API的GET请 [!DNL Catalog] 求时，最佳做法是在请求中包含查询参数，以便仅返回所需的对象和属性。 未过滤的请求可能导致响应有效负载超过3GB，从而降低整体性能。

您可以通过将特定对象的ID包含在请求路径中来视图特定对象，或使用查询参数(如 `properties` 和筛 `limit` 选响应)。 过滤器可以作为标题和查询参数传递，而传递的查询参数优先。 有关详细信息，请 [参阅筛选目录数](filter-data.md) 据文档。

由于某些查询可以给API加大负载，因此已对查询实施全局限制，以进 [!DNL Catalog] 一步支持最佳实践。

## 后续步骤

此文档涵盖调用API所需的必备知 [!DNL Catalog] 识。 您现在可以继续访问本开发人员指南中提供的示例调用，并按照其说明进行操作。

本指南中的大多数示例都使用 `/dataSets` 端点，但这些原则可应用于内的其 [!DNL Catalog] 他端点( `/batches` 如和 `/accounts`)。 有关每个 [端点可用的所有调用](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) 和操作的完整列表，请参阅目录服务API参考。

有关演示API如何与数据获取相关的分步 [!DNL Catalog] 工作流程，请参阅有关创建数 [据集的教程](../datasets/create.md)。
