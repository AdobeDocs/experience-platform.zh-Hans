---
keywords: Experience Platform;home;popular topics;data location;Data Location;Data management;data management;Lineage;lineage;data type;data types;Data types;Data type
solution: Experience Platform
title: 数据集概述
topic: datasets
description: 此文档提供了Experience Platform中数据集的高级概述。
translation-type: tm+mt
source-git-commit: 0f3a4ba6ad96d2226ae5094fa8b5073152df90f7
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 2%

---


# 数据集概述

成功引入Adobe Experience Platform的所有数据都作为数据集保留 [!DNL Data Lake] 在内。 数据集是存储和管理构建，用于模式集合，通常是表，其中包含（列）和字段（行）。 数据集还包含描述其存储数据各个方面的元数据。

此文档提供了中数据集的高级概述 [!DNL Experience Platform]。

## 创建数据集和跟踪元数据

[!DNL Catalog Service] 是数据位置和谱系的记录系 [!DNL Experience Platform]统，用于创建和管理数据集。 [!DNL Catalog] 跟踪每个数据集的元数据，包括对数据集所符合的( [!DNL Experience Data Model] XDM)模式的引用（在下一节中说明），以及摄取到该数据集中的记录数。

有关详细 [信息，请参阅](../home.md) “目录服务”概述。

## 对数据集数据实施限制

[!DNL Experience Data Model] (XDM)是组织客户体验数据的 [!DNL Platform] 标准化框架。 所有被摄取的数 [!DNL Platform] 据都必须符合预定义的XDM模式，才能作为数据集 [!DNL Data Lake] 在中保留。

所有数据集都包含对XDM模式的引用，该引用约束了可存储数据的格式和结构。 尝试将数据上传到不符合数据集的XDM模式的数据集将导致摄取失败。

有关XDM的详细信息，请参 [阅XDM系统概述](../../xdm/home.md)。

## 将数据引入数据集

Adobe Experience Platform数据摄取表示从各种来源 [!DNL Platform] 收集数据的多种方法。 无论采用何种摄取方法，所有成功摄取的数据都会转换为批处理文件。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。然后，这些批处理文件会添加到专用数据集并在中保留 [!DNL Data Lake]。

有关更多 [信息，请参阅](../../ingestion/home.md) “数据摄取概述”。

## 将使用标签应用于数据集

Adobe Experience Platform [!DNL Data Governance] 允许您管理客户数据，以确保遵守适用于数据使用的法规、限制和政策。 该 [!DNL Data Governance] 框架允许您应用使用标签以根据应用于该数据的使用策略对数据进行分类。

数据使用标签可以应用于整个数据集或单个数据集字段。 在数据集级别添加的标签由该数据集中的所有字段继承。

有关该 [服务的更多信息](../../data-governance/home.md) ，请参阅数据管理概述。 有关如何在中使用使用标签的 [!DNL Platform]步骤，请参阅以下指南：

* [在UI中管理标签](../../data-governance/labels/user-guide.md)
* [在API中管理数据集标签](../../data-governance/labels/dataset-api.md)

## 下游服务中的数 [!DNL Platform] 据集

一旦使用数据集存储摄取的数据，下游服务就会使用这些数据集 [!DNL Platform] 更新客户用户档案，通过机器学习获得洞察，等等。

以下是使用数据集进行各种操作的下游服务列表。 请查阅每项服务的文档以了解更多信息。

* [[!DNL数据访问API]](../../data-access/home.md):允许您访问和下载存储在数据集中的文件的内容。
* [Adobe Experience Platform身份服务](../../identity-service/home.md):跨设备和系统建立身份桥梁，根据XDM模式定义的身份字段将数据集链接在一起。
* [[!DNL实时客户用户档案]](../../profile/home.md):利 [!DNL Identity Service] 用数据集实时创建详细的客户用户档案。 [!DNL Real-time Customer Profile] 从客户用户档案中 [!DNL Data Lake] 提取数据，并将客户保留在其自己的单独数据存储中。
* [Adobe Experience Platform细分服务](../../segmentation/home.md):允许您根据数据构建细分和生成 [!DNL Real-time Customer Profile] 受众。 然后，这些受众可以导出到其自己的数据集中 [!DNL Data Lake]。
* [Adobe Experience Platform数据科学工作区](../../data-science-workspace/home.md):使用机器学习和人工智能在大数据集中发掘洞察。
* [Adobe Experience Platform查询服务](../../query-service/home.md):允许您使用标准SQL查询数据，加 [!DNL Experience Platform]入查询中的任何数据集，并将结果捕获为新数据集，以便在报告、 [!DNL Data Lake] 或中使用 [!DNL Data Science Workspace][!DNL Real-time Customer Profile]。
* [Adobe Experience Platform决策服务](../../decisioning-service/home.md):利用 [!DNL Real-time Customer Profile] 根据从启用的数据集中提取的行为数据，从一组选项中确定客户最可能 [!DNL Profile] 做出的选择。

## 后续步骤

通过阅读此文档，您已被引入了数据集的核心使用， [!DNL Experience Platform]以及利用数据集的 [!DNL Platform] 各种服务。 有关数据集使用方式的更多详细信 [!DNL Platform]息，请查看本概述中链接的服务文档。

有关如何在UI中与数据集交互的 [!DNL Experience Platform] 步骤，请参阅 [数据集用户指南](user-guide.md)。