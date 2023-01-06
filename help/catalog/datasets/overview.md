---
keywords: Experience Platform；主页；热门主题；数据位置；数据位置；数据管理；世系；世系；数据类型；数据类型；数据类型；数据类型
solution: Experience Platform
title: 数据集概述
description: 本文档全面概述了 Experience Platform 中的数据集。
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 8%

---

# 数据集概述

成功摄取到Adobe Experience Platform的所有数据都将保留在 [!DNL Data Lake] 作为数据集。 数据集是用于数据集合的存储和管理结构，通常是表格，其中包含架构（列）和字段（行）。数据集还包含描述其存储的数据的各方面特性的元数据。

本文档提供了 [!DNL Experience Platform].

## 创建数据集和跟踪元数据

[!DNL Catalog Service] 是中数据位置和谱系的记录系统 [!DNL Experience Platform]、和用于创建和管理数据集。 [!DNL Catalog] 跟踪每个数据集的元数据，其中包括对 [!DNL Experience Data Model] (XDM)数据集符合的模式（在下一节中有说明）以及摄取到该数据集中的记录数。

请参阅 [目录服务概述](../home.md) 以了解更多信息。

## 对数据集数据实施限制

[!DNL Experience Data Model] (XDM)是标准化框架， [!DNL Platform] 组织客户体验数据。 所有摄取到 [!DNL Platform] 必须符合预定义的XDM架构，才能将其持久保留在 [!DNL Data Lake] 作为数据集。

所有数据集都包含对XDM架构的引用，该架构可限制可存储数据的格式和结构。 如果尝试将数据上传到与数据集的XDM架构不符的数据集，则会导致摄取失败。

有关XDM的更多信息，请参阅 [XDM系统概述](../../xdm/home.md).

## 将数据摄取到数据集

Adobe Experience Platform数据摄取表示通过 [!DNL Platform] 从各种源摄取数据。 无论采用何种摄取方法，所有成功摄取的数据都会转换为批处理文件。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。然后，这些批处理文件会添加到专用数据集并保留在 [!DNL Data Lake].

请参阅 [数据摄取概述](../../ingestion/home.md) 以了解更多信息。

## 将使用情况标签应用于数据集

Adobe Experience Platform数据管理允许您管理客户数据，以确保遵守适用于数据使用的法规、限制和政策。 数据管理框架允许您应用使用标签，以根据应用于该数据的使用策略对数据进行分类。

>[!IMPORTANT]
>
>仅支持在数据集级别应用标签用于数据管理用例。 如果您尝试为数据创建访问策略，则必须 [将标签应用到架构](../../xdm/tutorials/labels.md) 数据集所基于的信息。 请参阅 [基于属性的访问控制](../../access-control/abac/overview.md) 以了解更多信息。

数据使用情况标签可以应用于整个数据集或单个数据集字段。 数据集级别添加的标签将由该数据集内的所有字段继承。

请参阅 [数据管理概述](../../data-governance/home.md) 以了解有关该服务的详细信息。 有关如何使用 [!DNL Platform]，请参阅以下指南：

* [在UI中管理标签](../../data-governance/labels/user-guide.md)
* [在API中管理数据集标签](../../data-governance/labels/dataset-api.md)

## 下游数据集 [!DNL Platform] 服务

使用数据集存储摄取的数据后，下游会使用这些数据集 [!DNL Platform] 更新客户配置文件、通过机器学习获得洞察等服务。

以下是使用数据集进行各种操作的下游服务列表。 有关更多信息，请查看每项服务的文档。

* [[!DNL Data Access API]](../../data-access/home.md):允许您访问和下载数据集中存储的文件内容。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md):跨设备和系统构建身份桥梁，根据数据集符合的XDM架构定义的身份字段，将数据集链接在一起。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md):利用 [!DNL Identity Service] 从数据集实时创建详细的客户用户档案。 [!DNL Real-Time Customer Profile] 从中提取数据 [!DNL Data Lake] 并将客户配置文件保留在其自己的单独数据存储中。
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md):允许您从 [!DNL Real-Time Customer Profile] 数据。 然后，可以将这些受众导出到 [!DNL Data Lake].
* [Adobe Experience Platform数据科学工作区](../../data-science-workspace/home.md):使用机器学习和人工智能来揭示大数据集中的洞察。
* [Adobe Experience Platform查询服务](../../query-service/home.md):允许您使用标准SQL在中查询数据 [!DNL Experience Platform]，加入 [!DNL Data Lake] 并捕获查询结果作为新数据集以用于报告， [!DNL Data Science Workspace]或 [!DNL Real-Time Customer Profile].
* [Adobe Experience Platform目标服务](../../destinations/home.md):允许您 [导出数据集](/help/destinations/ui/export-datasets.md) 到所需的云存储或电子邮件营销目标，以便进行报表或数据科学活动。

## 后续步骤

通过阅读本文档，您已介绍中数据集的核心用法 [!DNL Experience Platform]，以及 [!DNL Platform] 利用数据集的服务。 有关中使用数据集的多种方式的更多详细信息 [!DNL Platform]，请查看在此概述中链接的服务文档。

有关如何与 [!DNL Experience Platform] UI，请参阅 [datasets用户指南](user-guide.md).
