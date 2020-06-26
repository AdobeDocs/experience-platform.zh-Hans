---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 将数据添加到实时客户用户档案
topic: tutorial
translation-type: tm+mt
source-git-commit: 93aae0e394e1ea9b6089d01c585a94871863818e
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---


# 将数据添加到实时客户用户档案

本教程概述了向实时客户用户档案添加数据所需的步骤。

## 启用模式以实时用户档案客户

被引入Experience Platform以供实时客户用户档案使用的数据必须符合启用用户档案的体验数据模型(XDM)模式。 要启用模式进行用户档案，它必须实现XDM单个用户档案或XDM ExperienceEvent类。

您可以使用模式注册表API或模式编辑器用户界面启用模式以在实时客户用户档案中使用。 要开始，请按照教程使 [用API创建模式](../../xdm/tutorials/create-schema-api.md) , [或使用模式编辑器UI创建模式](../../xdm/tutorials/create-schema-ui.md)。

## 使用批量摄取添加数据

所有使用批量摄取上传到平台的数据都上传到单个数据集。 在实时客户用户档案能够使用此数据之前，必须具体配置相关数据集。 有关完整说明，请参阅有关为 [用户档案和标识服务配置数据集的教程](dataset-configuration.md)。

配置数据集后，您可以将开始引入数据。 有关如何上 [传不同格式文件的详细步骤](../../ingestion/batch-ingestion/api-overview.md) ，请参阅批处理摄取开发人员指南。

## 使用流摄取添加数据

任何符合启用用户档案的XDM模式的流摄取的数据将自动在实时客户用户档案中添加或覆盖相应的记录。 如果记录中提供了多个标识，或使用了时间序列数据，则这些标识将在标识图中映射，而无需额外配置。 请参阅流 [式摄取开发人员指南](../../ingestion/tutorials/streaming-record-data.md) ，了解更多信息。

## 确认上载成功

首次将数据上传到新数据集时，或者作为涉及新ETL或数据源的流程的一部分，建议仔细检查数据以确保其正确上传。

使用实时客户用户档案访问API，您可以在批数据加载到数据集中时检索批数据。 如果无法检索任何期望的实体，则可能未启用数据集进行用户档案。 确认已启用数据集后，请确保源数据格式和标识符支持您的预期。

有关如何使用实时客户用户档案API访问实体的详细说明，请参阅实 [体端点指南](../api/entities.md)，也称为“用户档案访问API”。