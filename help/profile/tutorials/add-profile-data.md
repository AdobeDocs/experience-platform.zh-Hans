---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API；启用用户档案；启用用户档案
title: 将数据添加到实时客户用户档案
topic-legacy: tutorial
type: Tutorial
description: 本教程概述了向实时客户用户档案添加数据所需的步骤。
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# 向[!DNL Real-time Customer Profile]添加数据

本教程概述了向[!DNL Real-time Customer Profile]添加数据所需的步骤。

## 为[!DNL Real-time Customer Profile]启用模式

被收录到[!DNL Experience Platform]以供[!DNL Real-time Customer Profile]使用的数据必须符合为[!DNL Profile]启用的[!DNL Experience Data Model](XDM)模式。 要启用模式进行用户档案，它必须实现[!DNL XDM Individual Profile]或[!DNL XDM ExperienceEvent]类。

您可以使用[!DNL Schema Registry] API或[!DNL Schema Editor]用户界面启用在[!DNL Real-time Customer Profile]中使用的模式。 要开始，请按照以下教程操作：使用API](../../xdm/tutorials/create-schema-api.md)或[使用模式编辑器UI](../../xdm/tutorials/create-schema-ui.md)创建模式。[

## 使用批量摄取添加数据

使用批处理摄取上载到[!DNL Platform]的所有数据都上载到各个数据集。 在[!DNL Real-time Customer Profile]可以使用此数据之前，必须专门配置相关数据集。 有关完整说明，请参阅教程[配置用户档案和标识服务的数据集](dataset-configuration.md)。

配置数据集后，您可以将收录数据开始到其中。 有关如何上传不同格式文件的详细步骤，请参阅[批量摄取开发人员指南](../../ingestion/batch-ingestion/api-overview.md)。

## 使用流摄取添加数据

任何符合[!DNL Profile]启用的XDM模式的流摄取的数据将自动在[!DNL Real-time Customer Profile]中添加或覆盖相应的记录。 如果在记录中提供多个标识，或使用时间序列数据，则这些标识将在标识图中映射，而不需要额外配置。 有关详细信息，请参阅[流式摄取开发人员指南](../../ingestion/tutorials/streaming-record-data.md)。

## 确认上载成功

首次将数据上载到新数据集时，或作为涉及新ETL或数据源的流程的一部分，建议仔细检查数据，以确保正确上载。

使用[!DNL Real-time Customer Profile] Access API，您可以在批处理数据加载到数据集中时检索它。 如果无法检索您期望的任何实体，则可能未为[!DNL Profile]启用数据集。 确认已启用数据集后，请确保您的源数据格式和标识符支持您的预期。

有关如何使用[!DNL Real-time Customer Profile] API访问实体的详细说明，请参阅[entities endpoint guide](../api/entities.md)（也称为“[!DNL Profile Access] API”）。
