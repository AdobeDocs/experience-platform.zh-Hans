---
title: Adobe Experience Platform发行说明2020年12月
description: Adobe Experience Platform 2020年12月版发行说明。
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 8%

---

# Adobe Experience Platform 发行说明

**发行日期： 2020年12月9日**

Adobe Experience Platform中的新增功能：

- [[!DNL Dataflows]](#dataflows)

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

数据流是跨平台移动数据的数据作业的表示方法。这些数据流在不同的服务中配置，可帮助将数据从源连接器移动到目标数据集、身份和配置文件服务以及目标。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据流透明度 | 您可以监视源数据流和目标数据流。 欲知更多信息，请阅读 [有关监控源的教程](../../dataflows/ui/monitor-sources.md) 或 [有关监视目标的教程](../../dataflows/ui/monitor-destinations.md). |

要了解有关数据流的更多信息，请阅读 [数据流概述](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

数据科学工作区使用机器学习和人工智能从您的数据创建见解。 数据科学工作区集成到Adobe Experience Platform中，可帮助您跨Adobe解决方案使用内容和数据资源做出预测。

**主要功能**

| 功能 | 描述 |
| --- | ---|
| Adobe Experience Platform Intelligence包加载项 | Adobe Experience Platform Intelligence包加载项是数据科学工作区升级，可解锁其他关键功能，例如： <li> UI驱动的模型实验与评估。</li><li> 能够通过计划的培训和引用作业来部署和操作模型。</li><li> 支持Tensorflow模型中的深度学习（GPU计算）。</li><li> 基于Spark的分布式计算，针对大型数据集（10MM +行）进行训练和评分。</li><li>等等</li> |

要了解有关Adobe Experience Platform Intelligence包加载项的更多信息，请参阅以下文档： [数据科学工作区访问和功能](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用来构建、标记和增强这些数据 [!DNL Platform] 服务。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

[!DNL Experience Platform] 提供了一个RESTful API和一个交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 更新流源的帐户和连接详细信息 | 您现在可以使用更新现有流连接的名称、描述和凭据 [!DNL Flow Service] API和UI。 有关更多信息，请参阅以下教程： [使用API更新连接](../../sources/tutorials/api/update.md) 和 [使用UI编辑帐户详细信息](../../sources/tutorials/ui/monitor.md). |
| 删除数据流 | 现在可以使用删除包含错误或变得不必要的流数据流 [!DNL Flow Service] API和UI。 有关更多信息，请参阅以下教程： [使用API删除数据流](../../sources/tutorials/api/delete-dataflows.md) 和 [使用UI删除数据流](../../sources/tutorials/ui/delete.md). |

要了解有关源的更多信息，请参阅 [源概述](../../sources/home.md).
