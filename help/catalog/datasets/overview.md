---
keywords: Experience Platform；主页；热门主题；数据位置；数据位置；数据管理；数据管理；谱系；谱系；数据类型；数据类型；数据类型
solution: Experience Platform
title: 数据集概述
description: 本文档高度概括 Experience Platform 中的数据集。
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: dca5c9df82434d75238a0a80f15e5562cf2fa412
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 8%

---

# 数据集概述

所有成功引入Adobe Experience Platform的数据将保留在 [!DNL Data Lake] 作为数据集。 数据集是用于数据集合的存储和管理结构，通常是表格，其中包含架构（列）和字段（行）。数据集还包含描述其存储的数据的各方面特性的元数据。

本文档提供了中数据集的高级概述 [!DNL Experience Platform].

## 创建数据集和跟踪元数据

[!DNL Catalog Service] 是数据位置记录系统和中的谱系 [!DNL Experience Platform]，用于创建和管理数据集。 [!DNL Catalog] 跟踪每个数据集的元数据，其中包括对 [!DNL Experience Data Model] 数据集符合的(XDM)架构（在下一节中有说明）以及摄取到该数据集中的记录数。

请参阅 [目录服务概述](../home.md) 以了解更多信息。

## 对数据集数据实施约束

[!DNL Experience Data Model] (XDM)是标准化的框架，通过它 [!DNL Platform] 组织客户体验数据。 摄取到的所有数据 [!DNL Platform] 必须符合预定义的XDM架构，然后才能将其保留在 [!DNL Data Lake] 作为数据集。

所有数据集都包含对XDM架构的引用，该引用会限制它们可以存储的数据的格式和结构。 尝试将数据上传到不符合数据集的XDM架构的数据集会导致摄取失败。

有关XDM的更多信息，请参见 [XDM系统概述](../../xdm/home.md).

## 将数据引入数据集

Adobe Experience Platform数据摄取表示多种方法，其中 [!DNL Platform] 从各种来源摄取数据。 无论采用何种摄取方法，所有成功摄取的数据都会转换为批处理文件。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。然后，将这些批处理文件添加到专用数据集并保留在 [!DNL Data Lake].

请参阅 [数据引入概述](../../ingestion/home.md) 以了解更多信息。

## 应用于架构中数据集的标签

Adobe Experience Platform数据管理允许您管理客户数据，以确保遵守适用于数据使用的法规、限制和策略。 数据管理框架允许您应用使用标签，以根据应用于数据的使用策略对数据进行分类。 标签可应用于单个架构、这些架构中的字段以及整个单个数据集。 当标签直接应用于架构时，这些标签会传播到基于该架构的所有现有和未来数据集。

>[!IMPORTANT]
>
>标签无法再应用于数据集级别的字段。 此工作流已弃用，支持在架构级别应用标签。 在2024年5月31日之前，之前在数据集对象级别应用的任何标签仍将通过Platform UI受到支持。 要确保您的标签在所有架构中保持一致，在未来一年中，必须将之前附加到数据集级别字段的任何标签迁移到架构级别。 请参阅以下部分 [迁移以前应用的标签](../../data-governance/e2e.md#migrate-labels) 以获取有关如何执行此操作的说明。

请参阅 [数据管理概述](../../data-governance/home.md) 以了解有关该服务的更多信息。 有关如何在中使用使用使用标签的步骤 [!DNL Platform]，请参阅以下指南：

* [在UI中管理标签](../../data-governance/labels/user-guide.md)
* [在API中管理数据集标签](../../data-governance/labels/dataset-api.md)

## 下游数据集 [!DNL Platform] 服务

数据集用于存储提取的数据后，下游会使用这些数据集 [!DNL Platform] 服务，用于更新客户配置文件、通过机器学习获得见解等。

以下是下游服务的列表，这些服务使用数据集进行各种操作。 请查看每项服务的文档以了解更多信息。

* [[!DNL Data Access API]](../../data-access/home.md)：用于访问和下载存储在数据集中的文件的内容。
* [Adobe Experience Platform Identity服务](../../identity-service/home.md)：跨设备和系统桥接身份，根据数据集符合的XDM架构定义的身份字段将数据集链接在一起。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：利用 [!DNL Identity Service] 从数据集实时创建详细的客户配置文件。 [!DNL Real-Time Customer Profile] 从提取数据 [!DNL Data Lake] 并将客户配置文件保留在其自己的单独数据存储中。
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md)：用于生成区段并生成受众 [!DNL Real-Time Customer Profile] 数据。 然后，可以将这些受众导出到中他们自己的数据集 [!DNL Data Lake].
* [Adobe Experience Platform数据科学工作区](../../data-science-workspace/home.md)：使用机器学习和人工智能发掘大型数据集中的洞察。
* [Adobe Experience Platform查询服务](../../query-service/home.md)：允许您使用标准SQL在中查询数据 [!DNL Experience Platform]，连接内的任何数据集 [!DNL Data Lake] 以及将查询结果捕获为新的数据集以用于报告， [!DNL Data Science Workspace]，或 [!DNL Real-Time Customer Profile].
* [Adobe Experience Platform目标服务](../../destinations/home.md)：允许您 [导出数据集](/help/destinations/ui/export-datasets.md) 到所需的云存储或电子邮件营销目标，以用于报表或数据科学活动。

## 后续步骤

通过阅读本文档，我们向您介绍了中数据集的核心用途 [!DNL Experience Platform]以及各种 [!DNL Platform] 利用数据集的服务。 有关数据集的多种使用方式的更多详细信息 [!DNL Platform]中，请查看本概述中链接的服务文档。

有关如何与中的数据集交互的步骤 [!DNL Experience Platform] UI，请参阅 [数据集用户指南](user-guide.md).
