---
keywords: Experience Platform；主页；热门主题；数据位置；数据位置；数据管理；数据管理；谱系；谱系；数据类型；数据类型；数据类型
solution: Experience Platform
title: 数据集概述
description: 本文档高度概括 Experience Platform 中的数据集。
user-guide-description: 通过本指南获取Experience Platform中数据集的高级概述。 在此处了解如何创建这些变量、对数据强制实施限制以及将数据摄取到数据集中。
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 4%

---

# 数据集概述

所有成功引入Adobe Experience Platform的数据将作为数据集保留在[!DNL Data Lake]中。 数据集是用于数据集合的存储和管理结构，通常是表格，其中包含架构（列）和字段（行）。数据集还包含描述其存储的数据的各个方面的元数据。

本文档提供了[!DNL Experience Platform]中数据集的高级概述。

## 创建数据集和跟踪元数据

[!DNL Catalog Service]是[!DNL Experience Platform]中数据位置和族系的记录系统，用于创建和管理数据集。 [!DNL Catalog]跟踪每个数据集的元数据，其中包括对数据集所符合[!DNL Experience Data Model] (XDM)架构的引用（下一节中有说明）以及摄取到该数据集的记录数。

有关详细信息，请参阅[目录服务概述](../home.md)。

## 对数据集数据实施约束

[!DNL Experience Data Model] (XDM)是[!DNL Experience Platform]用于组织客户体验数据的标准化框架。 摄取到[!DNL Experience Platform]中的所有数据必须符合预定义的XDM架构，然后才能作为数据集保留在[!DNL Data Lake]中。

所有数据集都包含对XDM架构的引用，该引用会限制它们可以存储的数据的格式和结构。 尝试将数据上传到不符合数据集的XDM架构的数据集会导致摄取失败。

有关XDM的更多信息，请参阅[XDM系统概述](../../xdm/home.md)。

## 将数据引入数据集

Adobe Experience Platform Data Ingestion表示[!DNL Experience Platform]从各种来源摄取数据的多种方法。 无论采用何种摄取方法，所有成功摄取的数据都会转换为批处理文件。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。 然后，将这些批处理文件添加到专用数据集并保留在[!DNL Data Lake]中。

有关详细信息，请参阅[数据引入概述](../../ingestion/home.md)。

## 应用于架构中数据集的标签

Adobe Experience Platform数据管理允许您管理客户数据，以确保遵守适用于数据使用的法规、限制和策略。 数据管理框架允许您应用使用标签，以根据应用于数据的使用策略对数据进行分类。 标签可应用于单个架构、这些架构中的字段以及整个单个数据集。 当标签直接应用于架构时，这些标签会传播到基于该架构的所有现有和未来数据集。

>[!IMPORTANT]
>
>标签无法再应用于数据集级别的字段。 此工作流已弃用，支持在架构级别应用标签。 在2024年5月31日之前，之前在数据集对象级别应用的任何标签仍将通过Experience Platform UI受到支持。 要确保您的标签在所有架构中保持一致，在未来一年中，必须将之前附加到数据集级别字段的任何标签迁移到架构级别。 有关如何迁移先前应用的标签[&#128279;](../../data-governance/e2e.md#migrate-labels)的说明，请参阅部分。

有关该服务的更多信息，请参阅[数据管理概述](../../data-governance/home.md)。 有关如何使用[!DNL Experience Platform]中的使用标签的步骤，请参阅以下指南：

* [在UI中管理标签](../../data-governance/labels/user-guide.md)
* [在API中管理数据集标签](../../data-governance/labels/dataset-api.md)

## 下游[!DNL Experience Platform]服务中的数据集

数据集一旦用于存储提取的数据，下游[!DNL Experience Platform]服务就会使用这些数据集更新客户配置文件，通过机器学习获取洞察信息，等等。

以下是下游服务的列表，这些服务使用数据集进行各种操作。 请查看每项服务的文档以了解更多信息。

* [[!DNL Data Access API]](../../data-access/home.md)：允许您访问和下载存储在数据集中的文件的内容。
* [Adobe Experience Platform Identity服务](../../identity-service/home.md)：跨设备和系统桥接身份，根据数据集所遵循的XDM架构定义的身份字段将数据集链接在一起。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：利用[!DNL Identity Service]从您的数据集实时创建详细的客户配置文件。 [!DNL Real-Time Customer Profile]从[!DNL Data Lake]中提取数据并将客户配置文件保留在其自己的单独数据存储中。
* [Adobe Experience Platform分段服务](../../segmentation/home.md)：允许您根据[!DNL Real-Time Customer Profile]数据构建区段并生成受众。 然后，可以将这些受众导出到[!DNL Data Lake]中他们自己的数据集。
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md)：使用机器学习和人工智能发掘大型数据集中的见解。
* [Adobe Experience Platform查询服务](../../query-service/home.md)：允许您使用标准SQL查询[!DNL Experience Platform]中的数据，加入[!DNL Data Lake]内的任何数据集，并将查询结果捕获为新的数据集，以用于报表、[!DNL Data Science Workspace]或[!DNL Real-Time Customer Profile]。
* [Adobe Experience Platform目标服务](../../destinations/home.md)：允许您[将数据集](/help/destinations/ui/export-datasets.md)导出到所需的云存储或电子邮件营销目标，以用于报表或数据科学活动。

## 后续步骤

通过阅读本文档，您已了解[!DNL Experience Platform]中数据集的核心用途，以及使用数据集的各种[!DNL Experience Platform]服务。 有关[!DNL Experience Platform]中使用数据集的多种方式的更多详细信息，请查看本概述中链接的服务文档。

有关如何与[!DNL Experience Platform] UI中的数据集交互的步骤，请参阅[数据集用户指南](user-guide.md)。
