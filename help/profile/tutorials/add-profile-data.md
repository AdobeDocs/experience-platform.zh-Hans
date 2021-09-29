---
keywords: Experience Platform；配置文件；实时客户配置文件；故障诊断；API；启用配置文件；启用配置文件
title: 将数据添加到实时客户资料
topic-legacy: tutorial
type: Tutorial
description: 本教程概述了向实时客户用户档案添加数据所需的步骤。
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 3b34cf37182ae98545651a7b54f586df7d811f34
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# 将数据添加到[!DNL Real-time Customer Profile]

本教程概述了向[!DNL Real-time Customer Profile]添加数据所需的步骤。

## 为[!DNL Real-time Customer Profile]启用架构

被摄取到[!DNL Experience Platform]以供[!DNL Real-time Customer Profile]使用的数据必须符合为[!DNL Profile]启用的[!DNL Experience Data Model](XDM)架构。 要为配置文件启用架构，它必须实现[!DNL XDM Individual Profile]或[!DNL XDM ExperienceEvent]类。

您可以使用[!DNL Schema Registry] API或[!DNL Schema Editor]用户界面启用架构以在[!DNL Real-time Customer Profile]中使用。 要开始使用此功能，请按照[的教程，使用API](../../xdm/tutorials/create-schema-api.md)或[使用架构编辑器UI](../../xdm/tutorials/create-schema-ui.md)创建架构。

## 使用批量摄取添加数据

使用批量摄取上传到[!DNL Platform]的所有数据都会上传到单个数据集。 在[!DNL Real-time Customer Profile]使用此数据之前，必须专门配置相关数据集。 有关完整说明，请参阅[为配置文件和Identity Service](dataset-configuration.md)配置数据集的教程。

配置数据集后，您可以开始向其中摄取数据。 有关如何上传不同格式文件的详细步骤，请参阅[批量摄取开发人员指南](../../ingestion/batch-ingestion/api-overview.md)。

## 使用流摄取添加数据

任何与启用了[!DNL Profile]的XDM架构兼容的流摄取数据将自动在[!DNL Real-time Customer Profile]中添加或覆盖相应的记录。 如果记录中提供了多个标识，或使用了时间系列数据，则这些标识将在标识图中映射，而无需额外配置。 请参阅[流摄取开发人员指南](../../ingestion/tutorials/streaming-record-data.md)以了解更多信息。

## 确认上传成功

首次将数据上传到新数据集时，或在涉及新ETL或数据源的过程中，建议仔细检查数据以确保数据已正确上传。

使用[!DNL Real-time Customer Profile]访问API，可以在批量数据加载到数据集时检索该数据。 如果无法检索您期望的任何实体，则可能无法为[!DNL Profile]启用您的数据集。 确认您的数据集已启用后，请确保源数据格式和标识符支持您的预期。

有关如何使用[!DNL Real-time Customer Profile] API访问实体的详细说明，请参阅[实体端点指南](../api/entities.md)，也称为“[!DNL Profile Access] API”。

## 更新配置文件存储数据

有时可能需要更新贵组织的用户档案存储区中的数据。 例如，您可能需要更正记录或更改属性值。 这可以通过批量摄取或流式摄取完成，并且需要一个启用了配置文件的数据集，该数据集配置了一个更新标记。 有关如何配置数据集以进行属性更新的更多信息，请参阅[启用数据集以进行配置文件和Upsert](../../catalog/datasets/enable-upsert.md)的教程。
