---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据集概述
topic: datasets
translation-type: tm+mt
source-git-commit: 06733eb374d1b9409102a7cf13d61ed266cedaad

---


# 数据集概述

成功引入Adobe Experience Platform的所有数据将作为数据集保留在Data Lake中。 数据集是数据集合（通常是表）的存储和管理构造，它包含模式（列）和字段（行）。 数据集还包含描述其存储的数据各个方面的元数据。

此文档提供了Experience Platform中数据集的高级概述。

## 创建数据集和跟踪元数据

Catalog Service是Experience Platform中用于记录数据位置和谱系的系统，用于创建和管理数据集。 Catalog可跟踪每个数据集的元数据，包括对体验数据模型(XDM)的引用，该数据集符合该模式（如下一节所述），以及摄取到该数据集中的记录数。

有关详细 [信息，请参阅Catalog Service](../home.md) overview。

## 对数据集数据实施限制

Experience Data Model(XDM)是Platform组织客户体验数据的标准化框架。 所有摄取到平台中的数据都必须符合预定义的XDM模式，才能作为数据集在数据湖中保留。

所有数据集都包含对XDM模式的引用，该引用限制了它们可以存储的数据的格式和结构。 尝试将数据上传到不符合数据集XDM模式的数据集将导致摄取失败。

有关XDM的详细信息，请参阅 [XDM系统概述](../../xdm/home.md)。

## 将数据引入数据集

Adobe Experience Platform数据摄取代表平台从各种来源获取数据的多种方法。 无论采用哪种摄取方法，所有成功摄取的数据都会转换为批处理文件。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。 然后，这些批处理文件将添加到专用数据集并保留在“数据湖”中。

有关详细 [信息，请参阅](../../ingestion/home.md) “数据摄取”概述。

## 将使用标签应用于数据集

Adobe Experience Platform数据管理允许您管理客户数据，以确保符合适用于数据使用的法规、限制和政策。 使用数据使用标签和强制执行(DULE)作为其核心框架，数据管理允许您应用使用标签根据适用于该数据的使用策略对数据进行分类。

数据使用标签可以应用于整个数据集或单个数据集字段。 在数据集级别添加的标签由该数据集内的所有字段继承。

有关该服 [务的更多信息](../../data-governance/home.md) ，请参阅数据管理概述。 有关如何在Experience Platform UI中使用使用标签的步骤，请参阅数 [据使用标签用户指南](../../data-governance/labels/user-guide.md)。

## 下游平台服务中的数据集

使用数据集存储摄取的数据后，下游平台服务会使用这些数据集更新客户用户档案、通过机器学习获得洞察等。

以下是下游服务的列表，这些服务将数据集用于各种操作。 请查阅每项服务的文档以了解更多信息。

* [数据访问API](../../data-access/home.md):允许您访问和下载存储在数据集中的文件的内容。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md):跨设备和系统建立标识桥梁，根据数据集符合的XDM模式定义的标识字段将数据集链接在一起。
* [实时客户用户档案](../../profile/home.md):利用Identity Service从数据集实时创建详细的客户用户档案。 实时客户从数据湖中提取数据，并将客户用户档案保留在其自己的单独数据存储中。
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md):允许您根据实时客户用户档案数据构建细分并生成受众。 然后，这些受众可以导出到数据湖中自己的数据集。
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md):使用机器学习和人工智能在大数据集中发掘洞察。
* [Adobe Experience Platform查询服务](../../query-service/home.md):允许您使用标准SQL在Experience Platform中查询数据，加入Data Lake中的任何数据集，并将查询结果捕获为新数据集以用于报告、数据科学工作区或实时客户用户档案。
* [Adobe Experience Platform决策服务](../../decisioning-service/home.md):利用实时客户用户档案，根据用户档案从启用的数据集中提取的行为数据，从一组选项中确定客户最可能的选择。

## 后续步骤

通过阅读此文档，您已经介绍了Experience Platform中数据集的核心用途以及利用数据集的各种平台服务。 有关数据集在平台中使用的多种方式的详细信息，请查看本概述中链接的服务文档。

有关如何在Experience Platform UI中与数据集交互的步骤，请参阅数 [据集用户指南](user-guide.md)。