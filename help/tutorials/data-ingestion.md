---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 数据获取教程
topic-legacy: tutorial
type: Tutorial
description: 数据摄取包括使用源连接器进行的批处理摄取、流摄取和摄取。
exl-id: 51627acf-e90b-4911-aa54-4a59f3b6a8f9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 4%

---

# 将数据收录到[!DNL Experience Platform]

Adobe Experience Platform 将来自多个来源的数据整合在一起，以帮助营销人员更好地了解其客户的行为。Adobe [!DNL Experience Platform Data Ingestion]表示[!DNL Platform]从这些源中收集数据的多种方法，以及该数据如何在数据湖中保留以供下游[!DNL Platform services]使用。 [!DNL Data Ingestion] 包括使用源连接器进行批处理、流式摄取和摄取。要了解更多信息，请阅读[数据摄取概述](../ingestion/home.md)或直接转到[源文档](../sources/home.md)。

## 在UI和API中创建源连接

源连接器允许您从多个源中摄取数据，然后使用[!DNL Platform services]对其进行标记、结构化和增强。 要开始创建源连接器，请参阅[源概述](../sources/home.md)。

## 收录批数据

Adobe Experience Platform允许您将数据作为批处理文件轻松导入[!DNL Platform]。 要摄取的用户档案的示例可包括来自CRM系统中的平面文件（如Parke文件）的模式数据或符合注册表中的已知[!DNL Experience Data Model](XDM)模式的数据。 要开始，请访问[向平台教程](../ingestion/tutorials/ingest-batch-data.md)中摄取数据。

## 将CSV文件映射到XDM模式

要将CSV数据引入Adobe Experience Platform中，必须将数据映射到[!DNL Experience Data Model](XDM)模式。 有关如何使用[!DNL Experience Platform]用户界面将CSV文件映射到XDM模式的步骤，请按照[将CSV文件映射到XDM模式教程](../ingestion/tutorials/map-a-csv-file.md)进行操作。

## 创建流连接

要将流数据开始到[!DNL Experience Platform]，必须首先请求HTTP端点。 您可以选择配置此端点以强制执行已验证的行为。 这可以使用[!DNL Platform]用户界面或[!DNL Experience Platform] API来完成。 要了解更多信息，请按照以下教程操作：使用UI](../ingestion/tutorials/create-streaming-connection-ui.md)或[使用API](../ingestion/tutorials/create-streaming-connection.md)创建流连接。[

## 创建经过身份验证的流连接

通过身份验证的数据收集，Adobe Experience Platform服务（如[!DNL Real-time Customer Profile]和[!DNL Identity]）可以区分来自可信源和不可信源的记录。 要开始，请按照教程中的[创建经过身份验证的流连接](../ingestion/tutorials/create-authenticated-streaming-connection.md)。

## 流记录和时间序列数据

在数据集和流连接到位后，您可以将记录或时间序列数据流化到[!DNL Platform]中。 要开始流记录数据，请按照[流记录数据到平台教程](../ingestion/tutorials/streaming-record-data.md)中。 要开始流式传输时间序列数据，请按照[流式传输时间序列数据到Platform](../ingestion/tutorials/streaming-time-series-data.md)中。

## 在一个HTTP请求中流化多条消息

将数据流化到Adobe Experience Platform时，进行大量HTTP调用可能会非常昂贵。 例如，创建1个HTTP请求（每个1KB消息200个，单个负载200KB）时，效率要高得多，而不是创建1KB负载的200个HTTP请求。 正确使用时，在单个请求内对多个消息进行分组是优化发送到[!DNL Experience Platform]的数据的最佳方法。 要了解如何使用流摄取在单个HTTP请求中向[!DNL Experience Platform]发送多条消息，请按照[发送多条消息教程](../ingestion/tutorials/streaming-multiple-messages.md)进行操作。
