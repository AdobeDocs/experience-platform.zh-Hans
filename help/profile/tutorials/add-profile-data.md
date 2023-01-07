---
keywords: Experience Platform；配置文件；实时客户配置文件；故障诊断；API；启用配置文件；启用配置文件
title: 将数据添加到实时客户资料
type: Tutorial
description: 本教程概述了向实时客户用户档案添加数据所需的步骤。
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# 将数据添加到 [!DNL Real-Time Customer Profile]

本教程概述了将数据添加到 [!DNL Real-Time Customer Profile].

## 为 [!DNL Real-Time Customer Profile]

摄取到的数据 [!DNL Experience Platform] 供使用 [!DNL Real-Time Customer Profile] 必须符合 [!DNL Experience Data Model] (XDM)已为 [!DNL Profile]. 要为用户档案启用架构，必须实施 [!DNL XDM Individual Profile] 或 [!DNL XDM ExperienceEvent] 类。

您可以启用架构以在中使用 [!DNL Real-Time Customer Profile] 使用 [!DNL Schema Registry] API或 [!DNL Schema Editor] 用户界面。 要开始配置，请按照 [使用API创建模式](../../xdm/tutorials/create-schema-api.md) 或 [使用架构编辑器UI创建架构](../../xdm/tutorials/create-schema-ui.md).

## 使用批量摄取添加数据

上传到的所有数据 [!DNL Platform] 使用批量摄取会上传到单个数据集。 此数据在 [!DNL Real-Time Customer Profile]，则必须专门配置相关数据集。 有关完整说明，请参阅 [为配置文件和标识服务配置数据集](dataset-configuration.md).

配置数据集后，您可以开始向其中摄取数据。 请参阅 [批量获取开发人员指南](../../ingestion/batch-ingestion/api-overview.md) 以了解有关如何上传不同格式文件的详细步骤。

## 使用流摄取添加数据

任何与 [!DNL Profile]-enabled XDM架构将自动在 [!DNL Real-Time Customer Profile]. 如果记录中提供了多个标识，或使用了时间系列数据，则这些标识将在标识图中映射，而无需额外配置。 请参阅 [流式引入开发人员指南](../../ingestion/tutorials/streaming-record-data.md) 以了解更多。

## 确认上传成功

首次将数据上传到新数据集时，或在涉及新ETL或数据源的过程中，建议仔细检查数据以确保数据已正确上传。

使用 [!DNL Real-Time Customer Profile] 访问API时，您可以在批量数据加载到数据集中时对其进行检索。 如果无法检索您期望的任何实体，则可能未为 [!DNL Profile]. 确认您的数据集已启用后，请确保源数据格式和标识符支持您的预期。

有关如何使用 [!DNL Real-Time Customer Profile] API，请参阅 [entities endpoint指南](../api/entities.md)，也称为“[!DNL Profile Access] API”。

## 更新配置文件存储数据

有时可能需要更新贵组织的用户档案存储区中的数据。 例如，您可能需要更正记录或更改属性值。 这可以通过批量摄取完成，并且需要一个启用了配置文件的数据集，该数据集配置了一个更新标记。 有关如何配置数据集以进行属性更新的更多信息，请参阅 [为配置文件启用数据集并重新插入](../../catalog/datasets/enable-upsert.md).
