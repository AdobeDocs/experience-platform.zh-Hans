---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;enable profile;Enable profile
title: 将数据添加到实时客户用户档案
topic: tutorial
type: Tutorial
description: 本教程概述了向实时客户用户档案添加数据所需的步骤。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# 将数据添加到 [!DNL Real-time Customer Profile]

本教程概述了向添加数据所需的步骤 [!DNL Real-time Customer Profile]。

## 启用模式 [!DNL Real-time Customer Profile]

被引入供 [!DNL Experience Platform] 使用的 [!DNL Real-time Customer Profile] 模式必须符 [!DNL Experience Data Model] 合启用的(XDM) [!DNL Profile]。 要启用模式进行用户档案，它必须实现或 [!DNL XDM Individual Profile] 类 [!DNL XDM ExperienceEvent] 。

您可以启用模式以 [!DNL Real-time Customer Profile] 在使用 [!DNL Schema Registry] API或用 [!DNL Schema Editor] 户界面中。 要开始，请按照教程使 [用API创建模式](../../xdm/tutorials/create-schema-api.md) , [或使用模式编辑器UI创建模式](../../xdm/tutorials/create-schema-ui.md)。

## 使用批量摄取添加数据

使用批量摄取上传 [!DNL Platform] 到的所有数据都上传到单个数据集。 在此数据可供使用之 [!DNL Real-time Customer Profile]前，必须明确配置相关数据集。 有关完整说明，请参阅有关为 [用户档案和标识服务配置数据集的教程](dataset-configuration.md)。

配置数据集后，您可以将开始引入数据。 有关如何上 [传不同格式文件的详细步骤](../../ingestion/batch-ingestion/api-overview.md) ，请参阅批处理摄取开发人员指南。

## 使用流摄取添加数据

任何符合启用XDM模式的流 [!DNL Profile]摄取的数据将自动在中添加或覆盖相应的记录 [!DNL Real-time Customer Profile]。 如果记录中提供了多个标识，或使用了时间序列数据，则这些标识将在标识图中映射，而无需额外配置。 请参阅流 [式摄取开发人员指南](../../ingestion/tutorials/streaming-record-data.md) ，了解更多信息。

## 确认上载成功

首次将数据上传到新数据集时，或者作为涉及新ETL或数据源的流程的一部分，建议仔细检查数据以确保其正确上传。

使用 [!DNL Real-time Customer Profile] Access API，您可以在批处理数据加载到数据集时检索它。 如果无法检索任何您期望的实体，则可能未启用您的数据集 [!DNL Profile]。 确认已启用数据集后，请确保源数据格式和标识符支持您的预期。

有关如何使用API访问实体的详细说 [!DNL Real-time Customer Profile] 明，请参阅实 [体端点指南](../api/entities.md)，也称为“[!DNL Profile Access] API”。