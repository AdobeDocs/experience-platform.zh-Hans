---
keywords: Experience Platform；主页；热门主题；目录服务；目录服务；目录服务
solution: Experience Platform
title: 目录服务API指南
topic-legacy: developer guide
description: 目录服务API允许开发人员在Adobe Experience Platform中管理数据集元数据。 请阅读本指南，了解如何使用API执行关键操作。
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# [!DNL Catalog Service] API指南

[!DNL Catalog Service] 是Adobe Experience Platform中数据位置和谱系的记录系统。[!DNL Catalog] 充当元数据存储或“目录”，您可以在中查找有关数据的信息，而 [!DNL Experience Platform]无需访问数据本身。有关更多信息，请参阅[[!DNL Catalog] 概述](../home.md)。

本开发人员指南提供了帮助您开始使用[!DNL Catalog] API的步骤。 然后，该指南提供了使用[!DNL Catalog]执行键操作的示例API调用。

## 先决条件

[!DNL Catalog] 跟踪中多种资源和操作的元数 [!DNL Experience Platform]据。本开发人员指南要求您对创建和管理这些资源所涉及的各种[!DNL Experience Platform]服务有一定的了解：

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):用于组织客户体验数 [!DNL Platform] 据的标准化框架。
* [批量摄取](../../ingestion/batch-ingestion/overview.md):如 [!DNL Experience Platform] 何从数据文件（如CSV和Parquet）中摄取和存储数据。
* [流摄取](../../ingestion/streaming-ingestion/overview.md):如何 [!DNL Experience Platform] 实时从客户端和服务器端设备摄取和存储数据。

以下各节提供了为成功调用[!DNL Catalog Service] API而需要了解或掌握的其他信息。

## 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅[!DNL Experience Platform]疑难解答指南中[如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

## 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程可为所有[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

* 授权：载体`{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

[!DNL Experience Platform]中的所有资源均与特定虚拟沙箱隔离。 对[!DNL Platform] API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

* Content-Type:application/json

## [!DNL Catalog] API调用的最佳实践

在对[!DNL Catalog] API执行GET请求时，最佳做法是在请求中包含查询参数，以便仅返回所需的对象和属性。 未过滤的请求可能会导致响应负载的大小超过3GB，从而降低整体性能。

您可以通过在请求路径中包含特定对象的ID来查看特定对象，或使用查询参数（如`properties`和`limit`）来筛选响应。 过滤器可以作为标题和查询参数进行传递，并且优先作为查询参数进行传递。 有关详细信息，请参阅[filtering Catalog data](filter-data.md)上的文档。

由于某些查询可能会给API带来沉重负载，因此已对[!DNL Catalog]查询实施了全局限制，以进一步支持最佳实践。

## 后续步骤

本文档介绍了调用[!DNL Catalog] API所需的先决知识。 您现在可以继续阅读本开发人员指南中提供的示例调用并按照其说明进行操作。

本指南中的大多数示例都使用`/dataSets`端点，但该原则可以应用于[!DNL Catalog]内的其他端点（如`/batches`和`/accounts`）。 有关每个端点可用的所有调用和操作的完整列表，请参阅[目录服务API引用](https://www.adobe.io/experience-platform-apis/references/catalog/)。

有关演示[!DNL Catalog] API如何与数据摄取相关的分步工作流，请参阅[创建数据集](../datasets/create.md)教程。
