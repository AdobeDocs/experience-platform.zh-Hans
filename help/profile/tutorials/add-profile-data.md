---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 将数据添加到实时客户用户档案
topic: tutorial
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea

---


# 将数据添加到实时客户用户档案

本教程概述了向实时客户用户档案添加数据所需的步骤。

## 为实时客户模式启用用户档案

被收录到Experience Platform以供实时客户用户档案使用的数据必须符合启用用户档案的体验数据模型(XDM)模式。 要启用模式进行用户档案，它必须实现XDM单个用户档案或XDM ExperienceEvent类。

您可以启用模式，以便使用模式注册API或模式编辑器用户界面在实时客户用户档案中使用。 要开始，请按照教程使用API [创建模式](../../xdm/tutorials/create-schema-api.md) ，或 [使用模式编辑器UI创建模式](../../xdm/tutorials/create-schema-ui.md)。

## 使用批量摄取添加数据

使用批量摄取上传到平台的所有数据都上传到各个数据集。 在实时客户用户档案能够使用此数据之前，必须对相关数据集进行专门配置。 有关完整说明，请参阅有关为 [用户档案和标识服务配置数据集的教程](dataset-configuration.md)。

配置数据集后，您可以将数据开始到数据集中。 有关如何上 [传不同格式文件的详细步骤](../../ingestion/batch-ingestion/api-overview.md) ，请参阅批量摄取开发人员指南。

## 使用流摄取添加数据

任何符合支持用户档案的XDM模式的流摄取的数据将自动在实时客户用户档案中添加或覆盖相应的记录。 如果在记录中提供了多个标识，或者使用了时间序列数据，则这些标识将在标识图中映射，而不需要额外的配置。 请参阅流 [式摄取开发人员指南](../../ingestion/tutorials/streaming-record-data.md) ，了解更多信息。

## 确认上传成功

首次将数据上传到新数据集时，或者作为涉及新ETL或数据源的流程的一部分，建议仔细检查数据，以确保正确上传。

使用实时客户用户档案访问API，您可以在将批量数据加载到数据集中时检索批量数据。 如果无法检索您期望的任何实体，则可能未启用数据集进行用户档案。 确认已启用数据集后，请确保源数据格式和标识符支持您的预期。

有关如何使用实时客户用户档案API访问实体的详细说明，请参阅有关实体的子指南(也称为“用户档案访问API”) [](../api/entities.md)。