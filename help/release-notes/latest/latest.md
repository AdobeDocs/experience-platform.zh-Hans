---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年6月10日
doc-type: release notes
last-update: June 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 35af498a41d779cc155cff7f030cccb57f68b8fa
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 5%

---


# Adobe Experience Platform 发行说明

**发布日期：2020 年 6 月 10 日**

对Adobe Experience Platform中现有功能的更新：

- [数据科学工作区](#dsw)
- [区段](#segmentation)
- [源](#sources)

## 数据科学工作区 {#dsw}

数据科学工作区使用机器学习和人工智能从数据中释放洞察。 数据科学工作区集成到Adobe Experience Platform中，可帮助您跨Adobe解决方案使用内容和数据资产进行预测。

数据科学工作区一直致力于通过使用实时机器学习来提供更好的体验和预测。 实时机器学习提供以行业标准可互操作的模型格式创作、测试和部署自定义或导入的预先培训的机器学习模型的能力，以便通过API端点进行实时评分/激活。

请注意，实时机器学习是alpha中的一种，目前仍在开发中。

| 功能 | 描述 |
|--- | ---|
| JupyterLab Launcher实时ML启动器 | JupyterLab Launcher现在包括一个用于实时机器学习(Alpha)的Python笔记本启动器。 |

有关实时机器学习alpha的更多信息，请参 [阅实时机器学习概述](../../data-science-workspace/real-time-machine-learning/home.md)。

## 区段 {#segmentation}

Adobe Experience Platform Segmentation Service提供用户界面和RESTful API，使您能够构建细分并根据实时客户受众数据生成用户档案。 这些细分在平台上集中配置和维护，使任何Adobe应用程序都能轻松访问。

分段服务通过描述区分客户群中可销售人群的标准来定义特定的用户档案子集。 细分可以基于记录数据（如人口统计信息）或表示客户与您品牌互动的时间序列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 日期字段 | 添加了日期功能的“周年”功能，使用户能够评估不带年份的日期。 |

有关分段的详细信息，请参阅分 [段概述](../../segmentation/home.md)

## 源 {#sources}

Adobe Experience Platform可以从外部源收集数据，同时允许您使用平台服务构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)收集数据。

Experience Platform提供REST风格的API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 对云存储系统的更多API和UI支持 | Apache HDFS的新源连接器 |
| 对数据库的其他API和UI支持 | Couchbase的新源连接器。 |

要进一步了解源，请参阅 [源概述](../../sources/home.md)。
