---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API；启用配置文件；启用配置文件
title: 将数据添加到实时客户个人资料
type: Tutorial
description: 本教程概述了将数据添加到Real-Time Customer Profile所需的步骤。
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# 将数据添加到 [!DNL Real-Time Customer Profile]

本教程概述了向添加数据所需的步骤 [!DNL Real-Time Customer Profile].

## 为以下项启用架构 [!DNL Real-Time Customer Profile]

正在引入的数据 [!DNL Experience Platform] 供使用 [!DNL Real-Time Customer Profile] 必须符合 [!DNL Experience Data Model] (XDM)架构已启用，用于 [!DNL Profile]. 要为配置文件启用架构，它必须实施 [!DNL XDM Individual Profile] 或 [!DNL XDM ExperienceEvent] 类。

您可以启用架构以用于 [!DNL Real-Time Customer Profile] 使用 [!DNL Schema Registry] API或 [!DNL Schema Editor] 用户界面。 要开始配置，请观看的教程 [使用API创建架构](../../xdm/tutorials/create-schema-api.md) 或 [使用架构编辑器UI创建架构](../../xdm/tutorials/create-schema-ui.md).

## 使用批量摄取添加数据

所有数据已上传至 [!DNL Platform] 使用批量摄取会上载到单个数据集。 在可以使用此数据之前， [!DNL Real-Time Customer Profile]，必须专门配置相关数据集。 有关完整说明，请参阅 [为配置文件和Identity服务配置数据集](dataset-configuration.md).

配置数据集后，您可以开始将数据摄取到其中。 请参阅 [批量摄取开发人员指南](../../ingestion/batch-ingestion/api-overview.md) 有关如何上传不同格式文件的详细步骤。

## 使用流式摄取添加数据

任何与 [!DNL Profile]-enabled XDM架构将自动添加或覆盖中的相应记录 [!DNL Real-Time Customer Profile]. 如果记录中提供了多个身份，或者使用了时序数据，则这些身份将在身份图中进行映射，而无需其他配置。 请参阅 [流式摄取开发人员指南](../../ingestion/tutorials/streaming-record-data.md) 了解更多信息。

## 确认上传成功

首次将数据上载到新数据集时，或者作为涉及新ETL或数据源的流程的一部分，建议仔细检查数据，以确保数据已正确上载。

使用 [!DNL Real-Time Customer Profile] 访问API，您可以在批量数据加载到数据集时检索该数据。 如果无法检索任何预期的实体，则可能无法为启用数据集 [!DNL Profile]. 确认已启用数据集后，请确保源数据格式和标识符支持您的期望。

有关如何使用访问实体的详细说明 [!DNL Real-Time Customer Profile] API，请参阅 [实体端点指南](../api/entities.md)，也称为“[!DNL Profile Access] API”。

## 更新配置文件存储数据

有时候，可能需要更新您组织的配置文件存储区中的数据。 例如，您可能需要更正记录或更改属性值。 这可以通过批量摄取完成，并且需要为启用了配置文件的数据集配置更新插入标记。 有关如何配置数据集以进行属性更新的更多信息，请参阅的教程 [为配置文件和更新插入启用数据集](../../catalog/datasets/enable-upsert.md).
