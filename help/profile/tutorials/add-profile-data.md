---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API；启用配置文件；启用配置文件
title: 将数据添加到实时客户个人资料
type: Tutorial
description: 本教程概述了将数据添加到Real-Time Customer Profile所需的步骤。
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# 将数据添加到[!DNL Real-Time Customer Profile]

本教程概述了向[!DNL Real-Time Customer Profile]添加数据所需的步骤。

## 为[!DNL Real-Time Customer Profile]启用架构

被摄取到[!DNL Experience Platform]中以供[!DNL Real-Time Customer Profile]使用的数据必须符合为[!DNL Profile]启用的[!DNL Experience Data Model] (XDM)架构。 要为配置文件启用架构，它必须实现[!DNL XDM Individual Profile]或[!DNL XDM ExperienceEvent]类。

您可以使用[!DNL Schema Registry] API或[!DNL Schema Editor]用户界面启用要在[!DNL Real-Time Customer Profile]中使用的架构。 若要开始，请按照以下教程操作：[使用API创建架构](../../xdm/tutorials/create-schema-api.md)或[使用架构编辑器UI创建架构](../../xdm/tutorials/create-schema-ui.md)。

## 使用批量摄取添加数据

使用批次摄取上载到[!DNL Experience Platform]的所有数据都会上载到单个数据集。 在[!DNL Real-Time Customer Profile]能够使用此数据之前，必须专门配置相关数据集。 有关完整说明，请参阅有关[为配置文件和身份服务配置数据集](dataset-configuration.md)的教程。

配置数据集后，您可以开始将数据摄取到其中。 有关如何上传不同格式文件的详细步骤，请参阅[批量摄取开发人员指南](../../ingestion/batch-ingestion/api-overview.md)。

## 使用流式摄取添加数据

任何与启用了[!DNL Profile]的XDM架构兼容的流摄取数据都将自动添加或覆盖[!DNL Real-Time Customer Profile]中的相应记录。 如果记录中提供了多个身份，或者使用了时序数据，则这些身份将在身份图中进行映射，而无需其他配置。 请参阅[流式摄取开发人员指南](../../ingestion/tutorials/streaming-record-data.md)以了解详情。

## 确认上传成功

首次将数据上载到新数据集时，或者作为涉及新ETL或数据源的流程的一部分，建议仔细检查数据，以确保数据已正确上载。

使用[!DNL Real-Time Customer Profile]访问API，您可以在批次数据加载到数据集时检索批次数据。 如果无法检索任何预期的实体，则可能无法为[!DNL Profile]启用数据集。 确认已启用数据集后，请确保源数据格式和标识符支持您的期望。

有关如何使用[!DNL Real-Time Customer Profile] API访问实体的详细说明，请参阅[实体端点指南](../api/entities.md)，也称为“[!DNL Profile Access] API”。

## 更新配置文件存储数据

有时候，可能需要更新您组织的配置文件存储区中的数据。 例如，您可能需要更正记录或更改属性值。 这可以通过批量摄取完成，并且需要为启用了配置文件的数据集配置更新插入标记。 有关如何为属性更新配置数据集的更多信息，请参阅[为配置文件和更新插入](../../catalog/datasets/enable-upsert.md)启用数据集的教程。
