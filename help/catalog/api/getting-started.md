---
keywords: Experience Platform；主页；热门主题；目录服务；目录服务；目录服务
solution: Experience Platform
title: 目录服务API指南
description: 目录服务API允许开发人员在Adobe Experience Platform中管理数据集元数据。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 3%

---

# [!DNL Catalog Service] API指南

[!DNL Catalog Service] 是Adobe Experience Platform中数据位置和谱系的记录系统。 [!DNL Catalog] 充当元数据存储或“目录”，您可以在其中找到有关数据的信息 [!DNL Experience Platform]，而无需访问数据本身。 请参阅 [[!DNL Catalog] 概述](../home.md) 以了解更多信息。

本开发人员指南提供了帮助您开始使用 [!DNL Catalog] API。 然后，该指南提供了用于使用执行键操作的示例API调用 [!DNL Catalog].

## 先决条件

[!DNL Catalog] 跟踪内多种资源和操作的元数据 [!DNL Experience Platform]. 本开发人员指南需要对 [!DNL Experience Platform] 与创建和管理这些资源相关的服务：

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):标准化框架， [!DNL Platform] 组织客户体验数据。
* [批量摄取](../../ingestion/batch-ingestion/overview.md):如何 [!DNL Experience Platform] 从数据文件（如CSV和Parquet）中摄取和存储数据。
* [流式摄取](../../ingestion/streaming-ingestion/overview.md):如何 [!DNL Experience Platform] 实时从客户端和服务器端设备摄取和存储数据。

以下各节提供了您需要了解或掌握的其他信息，以便成功调用 [!DNL Catalog Service] API。

## 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

## 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

* 授权：持有者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

* Content-Type:application/json

## 的最佳实践 [!DNL Catalog] API调用

对执行GET请求时 [!DNL Catalog] API，最佳做法是在请求中包含查询参数，以便仅返回您需要的对象和属性。 未过滤的请求可能会导致响应负载的大小超过3GB，从而降低整体性能。

您可以通过在请求路径中包含特定对象的ID来查看特定对象，或使用查询参数，例如 `properties` 和 `limit` 来筛选响应。 过滤器可以作为标题和查询参数进行传递，并且优先作为查询参数进行传递。 请参阅 [筛选目录数据](filter-data.md) 以了解更多信息。

由于某些查询可能会给API带来沉重负载，因此已对 [!DNL Catalog] 查询以进一步支持最佳实践。

## 后续步骤

本文档介绍了调用 [!DNL Catalog] API。 您现在可以继续阅读本开发人员指南中提供的示例调用并按照其说明进行操作。

本指南中的大多数示例都使用 `/dataSets` 端点，但原则可以应用于内的其他端点 [!DNL Catalog] (例如 `/batches` 和 `/accounts`)。 请参阅 [目录服务API参考](https://www.adobe.io/experience-platform-apis/references/catalog/) 以获取每个端点可用的所有调用和操作的完整列表。

用于演示 [!DNL Catalog] API与数据摄取相关，请参阅 [创建数据集](../datasets/create.md).
