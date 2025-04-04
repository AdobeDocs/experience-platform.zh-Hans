---
keywords: Experience Platform；主页；热门主题；目录服务；目录；目录服务；目录
solution: Experience Platform
title: 目录服务API指南
description: 目录服务API允许开发人员在Adobe Experience Platform中管理数据集元数据。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 22%

---

# [!DNL Catalog Service] API指南

[!DNL Catalog Service]是Adobe Experience Platform中数据位置和族系的记录系统。 [!DNL Catalog]充当元数据存储或“目录”，您可以在[!DNL Experience Platform]中找到有关您的数据的信息，而无需访问数据本身。 有关详细信息，请参阅[[!DNL Catalog] 概述](../home.md)。

本开发人员指南提供了帮助您开始使用 [!DNL Catalog] API 的步骤。然后，该指南提供了使用[!DNL Catalog]执行关键操作的示例API调用。

## 先决条件

[!DNL Catalog]跟踪[!DNL Experience Platform]中多种资源和操作的元数据。 此开发人员指南需要深入了解与创建和管理这些资源有关的各种[!DNL Experience Platform]服务：

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
* [批量摄取](../../ingestion/batch-ingestion/overview.md)： [!DNL Experience Platform]如何从数据文件（如CSV和Parquet）摄取和存储数据。
* [流式引入](../../ingestion/streaming-ingestion/overview.md)： [!DNL Experience Platform]如何从客户端和服务器端设备实时引入和存储数据。

以下部分提供了您需要了解或拥有的其他信息，以便成功调用[!DNL Catalog Service] API。

## 正在读取示例 API 调用

本指南提供了示例 API 调用来演示如何格式化请求。这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

## 收集所需标头的值

要调用[!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

* 授权：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

包含负载 (POST、PUT、PATCH) 的所有请求都需要额外的标头：

* Content-Type： application/json

## [!DNL Catalog] API调用的最佳实践

对[!DNL Catalog] API执行GET请求时，最佳实践是在请求中包含查询参数，以便仅返回所需的对象和属性。 未过滤的请求可能会导致响应有效负载的大小超过3GB，这会降低整体性能。

您可以在请求路径中包含特定对象的ID来查看它们，或者使用查询参数（如`properties`和`limit`）来筛选响应。 过滤器可作为标头和查询参数传递，以作为查询参数传递的过滤器优先。 有关详细信息，请参阅有关[筛选目录数据](filter-data.md)的文档。

由于某些查询可能会对API施加大量负载，因此已在[!DNL Catalog]个查询上实施全局限制，以进一步支持最佳实践。

## 后续步骤

本文档介绍了调用 [!DNL Catalog] API 所需的必备知识。您现在可以继续进行本开发人员指南中提供的示例调用，并按照其说明进行操作。

本指南中的大多数示例都使用`/dataSets`端点，但原则可以应用于[!DNL Catalog]内的其他端点（如`/batches`）。 有关每个端点可用的所有调用和操作的完整列表，请参阅[目录服务API引用](https://www.adobe.io/experience-platform-apis/references/catalog/)。

有关演示[!DNL Catalog] API如何与数据引入有关的分步工作流，请参阅有关[创建数据集](../datasets/create.md)的教程。
