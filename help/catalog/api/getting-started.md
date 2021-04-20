---
keywords: Experience Platform；主页；热门主题；目录服务；目录服务；目录服务；目录
solution: Experience Platform
title: 目录服务API指南
topic: developer guide
description: Catalog Service API允许开发人员管理Adobe Experience Platform中的数据集元数据。 请按照本指南学习如何使用API执行关键操作。
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# [!DNL Catalog Service] API指南

[!DNL Catalog Service] 是Adobe Experience Platform中数据位置和谱系的记录系统。[!DNL Catalog] 充当元数据存储或“目录”，您可以在其中找到有关数据的信息， [!DNL Experience Platform]无需访问数据本身。有关详细信息，请参阅[[!DNL Catalog] 概述](../home.md)。

此开发人员指南提供了帮助您使用[!DNL Catalog] API进行开始的步骤。 然后，该指南提供了使用[!DNL Catalog]执行键操作的示例API调用。

## 先决条件

[!DNL Catalog] 跟踪中几种资源和操作的元数 [!DNL Experience Platform]据本开发人员指南要求您对创建和管理这些资源所涉及的各种[!DNL Experience Platform]服务有充分的了解：

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。
* [批量摄取](../../ingestion/batch-ingestion/overview.md):如 [!DNL Experience Platform] 何从CSV和Parke等数据文件收录和存储数据。
* [流摄取](../../ingestion/streaming-ingestion/overview.md):如 [!DNL Experience Platform] 何从客户端和服务器端设备实时摄取和存储数据。

以下各节提供您需要了解或掌握的其他信息，以便成功调用[!DNL Catalog Service] API。

## 读取示例API调用

本指南提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中关于如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

## 收集所需标题的值

要调用[!DNL Platform] API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

* 授权：承载`{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个头，该头指定操作将在中执行的沙箱的名称：

* x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

* 内容类型：application/json

## [!DNL Catalog] API调用的最佳实践

当执行对[!DNL Catalog] API的GET请求时，最佳做法是在请求中包含查询参数，以便仅返回所需的对象和属性。 未过滤的请求可能导致响应有效负载超过3GB大小，从而降低整体性能。

可以通过将特定对象的ID包含在请求路径中来对其进行视图，或使用查询参数（如`properties`和`limit`）来筛选响应。 过滤器可以作为标头和查询参数传递，而传递的查询参数优先。 有关详细信息，请参阅[筛选目录数据](filter-data.md)的文档。

由于某些查询可以给API加大负载，因此已对[!DNL Catalog]查询实施全局限制以进一步支持最佳做法。

## 后续步骤

此文档涵盖了对[!DNL Catalog] API进行调用所需的必备知识。 您现在可以继续查看本开发人员指南中提供的示例调用，并按照其说明进行操作。

本指南中的大多数示例使用`/dataSets`端点，但这些原则可以应用于[!DNL Catalog]内的其他端点（如`/batches`和`/accounts`）。 有关每个端点可用的所有调用和操作的完整列表，请参阅[目录服务API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)。

有关演示[!DNL Catalog] API如何与数据摄取相关的分步工作流程，请参阅有关创建数据集[的教程。](../datasets/create.md)
