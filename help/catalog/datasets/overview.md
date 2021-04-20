---
keywords: Experience Platform；主页；热门主题；数据位置；数据管理；数据位置；数据管理；世系；世系；数据类型；数据类型；数据类型；数据类型
solution: Experience Platform
title: 数据集概述
topic: datasets
description: 本文档概括介绍了Experience Platform中的数据集。
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 2%

---


# 数据集概述

成功引入Adobe Experience Platform的所有数据将作为数据集保留在[!DNL Data Lake]中。 数据集是存储和管理构建，用于模式集合，通常是表格，其中包含（列）和字段（行）。 数据集还包含描述其存储数据各个方面的元数据。

此文档提供[!DNL Experience Platform]中数据集的高级概述。

## 创建数据集和跟踪元数据

[!DNL Catalog Service] 是记录数据位置和谱系的系统， [!DNL Experience Platform]用于创建和管理数据集。[!DNL Catalog] 跟踪每个数据集的元数据，包括对数据集符合的( [!DNL Experience Data Model] XDM)模式的引用（在下一节中说明）以及摄取到该数据集中的记录数。

有关详细信息，请参阅[目录服务概述](../home.md)。

## 对数据集数据实施约束

[!DNL Experience Data Model] (XDM)是组织客户体验数据 [!DNL Platform] 的标准化框架。所有被收录到[!DNL Platform]中的模式必须符合预定义的XDM数据，才能在[!DNL Data Lake]中作为数据集进行保留。

所有数据集都包含对XDM模式的引用，该引用限制了可以存储的数据的格式和结构。 尝试将数据上传到不符合数据集的XDM模式的数据集将导致摄取失败。

有关XDM的详细信息，请参阅[XDM系统概述](../../xdm/home.md)。

## 将数据引入数据集

Adobe Experience Platform数据摄取表示[!DNL Platform]从各种源中摄取数据的多种方法。 无论采用何种摄取方法，所有成功摄取的数据都将转换为批处理文件。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。然后，这些批处理文件将添加到专用数据集并保留在[!DNL Data Lake]中。

有关详细信息，请参阅[数据摄取概述](../../ingestion/home.md)。

## 将使用标签应用于数据集

Adobe Experience Platform [!DNL Data Governance]允许您管理客户数据，以确保符合适用于数据使用的法规、限制和政策。 [!DNL Data Governance]框架允许您应用使用标签以根据应用于该数据的使用策略对数据进行分类。

数据使用标签可以应用于整个数据集或单个数据集字段。 在数据集级别添加的标签由该数据集中的所有字段继承。

有关该服务的详细信息，请参阅[数据治理概述](../../data-governance/home.md)。 有关如何使用[!DNL Platform]中的使用标签的步骤，请参阅以下指南：

* [在UI中管理标签](../../data-governance/labels/user-guide.md)
* [管理API中的数据集标签](../../data-governance/labels/dataset-api.md)

## 下游[!DNL Platform]服务中的数据集

使用数据集存储摄取的数据后，下游[!DNL Platform]服务会使用这些数据集更新客户用户档案、通过机器学习获得洞察等。

以下是使用数据集进行各种操作的下游服务列表。 有关更多信息，请查看每项服务的文档。

* [[!DNL Data Access API]](../../data-access/home.md):允许您访问和下载存储在数据集中的文件的内容。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md):跨设备和系统构建身份桥梁，根据符合的XDM模式定义的身份字段将数据集链接在一起。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):利 [!DNL Identity Service] 用数据集实时创建详细的客户用户档案。[!DNL Real-time Customer Profile] 从数据中提取数 [!DNL Data Lake] 据，并将客户用户档案保留在其自己的独立数据存储中。
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md):允许您构建细分并根据数据生成 [!DNL Real-time Customer Profile] 受众。然后，这些受众可以导出到[!DNL Data Lake]中它们自己的数据集。
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md):使用机器学习和人工智能在大数据集中挖掘洞察。
* [Adobe Experience Platform查询服务](../../query-service/home.md):允许您使用标准SQL查询中的数据， [!DNL Experience Platform]将查询中的任何数据集 [!DNL Data Lake] 连接起来，并将结果捕获为新数据集以用于 [!DNL Data Science Workspace]报告、或 [!DNL Real-time Customer Profile]。

## 后续步骤

通过阅读此文档，您已被引入[!DNL Experience Platform]中数据集的核心使用以及利用数据集的各种[!DNL Platform]服务。 有关[!DNL Platform]中使用数据集的多种方式的详细信息，请查看本概述中链接的服务文档。

有关如何与[!DNL Experience Platform] UI中的数据集交互的步骤，请参阅[数据集用户指南](user-guide.md)。