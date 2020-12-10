---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年12月9日
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
translation-type: tm+mt
source-git-commit: ae353e6dda3f92647c32ee8e731be5785d24e5cb
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 6%

---


# Adobe Experience Platform 发行说明

**发布日期：2020年12月9日**

Adobe Experience Platform的新增功能：

- [[!DNL Dataflows]](#dataflows)

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

数据流是跨平台移动数据的数据作业的表示。 这些数据流是跨不同服务配置的，有助于将数据从源连接器移动到目标数据集、标识和用户档案服务以及目标。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据流的透明度 | 您可以监视源和目标的数据流。 有关详细信息，请阅读关 [于监视源的教程](../../dataflows/ui/monitor-sources.md) ，或 [者有关监视目标的教程](../../dataflows/ui/monitor-destinations.md)。 |

要进一步了解数据流，请阅读数 [据流概述](../../dataflows/home.md)。

## [!DNL Data Science Workspace] {#dsw}

数据科学工作区使用机器学习和人工智能从数据中获得洞察。 数据科学工作区集成到Adobe Experience Platform，可帮助您跨Adobe解决方案使用内容和数据资产进行预测。

**主要功能**

| 功能 | 描述 |
| --- | ---|
| Adobe Experience Platform情报程序包 | Adobe Experience Platform智能软件包加载项是数据科学工作区升级，可解锁其他主要功能，如： <li> UI驱动的模型试验和评估。</li><li> 能够部署模型并将其运行，同时进行定期培训和推荐作业。</li><li> 支持Tensorflow模型（GPU计算）中的深度学习。</li><li> 基于Spark的分布式计算，可针对大数据集（10MM +行）进行培训和评分。</li><li>等等</li> |

要进一步了解Adobe Experience Platform智能软件包加载项，请参阅有关数据科 [学工作区访问和功能的文档](../../data-science-workspace/access-features-dsw.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部来源收集数据，同时允许您使用服务来构建、标记和增强该 [!DNL Platform] 数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)收集数据。

[!DNL Experience Platform] 提供REST风格的API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置获取运行的时间，以及管理数据获取吞吐量。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 更新流源的帐户和连接详细信息 | 您现在可以使用API和UI更新现有流连接的名称、 [!DNL Flow Service] 说明和凭据。 有关详细信息，请参阅有关使用API [更新连接和使用UI编](../../sources/tutorials/api/update.md)[辑帐户详细信息的教程](../../sources/tutorials/ui/monitor.md)。 |
| 删除数据流 | 现在，可以使用API和UI删除包含错误或已变得不必 [!DNL Flow Service] 要的流数据流。 有关详细信息，请参阅有关使用 [API删除数据流和](../../sources/tutorials/api/delete-dataflows.md)[使用UI删除数据流的教程](../../sources/tutorials/ui/delete.md)。 |

要进一步了解源，请参阅 [源概述](../../sources/home.md)。

