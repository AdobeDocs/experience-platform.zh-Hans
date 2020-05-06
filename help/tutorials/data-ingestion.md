---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据获取教程
topic: tutorial
translation-type: tm+mt
source-git-commit: 0eecd802fc8d0ace3a445f3f188a7f095b97d0c8
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# 将数据引入Experience Platform

Adobe Experience Platform将来自多个来源的数据整合在一起，以帮助营销人员更好地了解其客户的行为。 Adobe Experience Platform数据摄取代表平台从这些来源收集数据的多种方法，以及数据如何在数据湖中保留以供下游平台服务使用。 数据摄取包括使用源连接器进行批量摄取、流式摄取和摄取。 要了解更多信息，请阅 [读数据摄取概述](../ingestion/home.md) ，或直接转到 [源文档](../sources/home.md)。

## 在UI和API中创建源连接器

源连接器允许您从多个源中摄取数据，然后使用平台服务对其进行标记、结构化和增强。 要开始创建源连接器，请参阅源 [概述](../sources/home.md)。

## 摄取批处理数据

Adobe Experience Platform允许您将数据作为批处理文件轻松导入Platform。 要摄取的用户档案的示例可以包括来自CRM系统中的平面文件（例如镶木地板文件）的模式数据或符合注册中的已知体验数据模型(XDM)模式的数据。 要开始，请访问 [平台教程中的Ingestion数据](../ingestion/tutorials/ingest-batch-data.md)。

## 将CSV文件映射到XDM模式

要将CSV数据引入Adobe Experience Platform，必须将数据映射到体验数据模型(XDM)模式。 有关显示如何使用Experience Platform用户界面将CSV文件映射到XDM模式的步骤，请 [按照CSV文件映射到XDM模式教程](../ingestion/tutorials/map-a-csv-file.md)。

## 创建流连接

要将流数据开始到Experience Platform，您必须先请求HTTP端点。 您可以选择配置此端点以强制实施身份验证行为。 这可以使用平台用户界面或Experience Platform API完成。 要了解更多信息，请按照教程 [使用UI创建流连接](../ingestion/tutorials/create-streaming-connection-ui.md) , [或使用API创建流连接](../ingestion/tutorials/create-streaming-connection.md)。

## 创建经过身份验证的流连接

通过实名数据收集，Adobe Experience Platform服务(如实时客户用户档案和身份)可以区分来自可信来源和不可信来源的记录。 要开始，请按照教程创建经 [身份验证的流连接](../ingestion/tutorials/create-authenticated-streaming-connection.md)。

## 流记录和时间序列数据

利用数据集和流式连接，您可以将记录或时间序列数据流化到平台。 要开始流记录数据，请按照流 [记录数据进入平台教程](../ingestion/tutorials/streaming-record-data.md)。 要开始流式传输时间序列数据，请 [按照流式传输时间序列数据到平台](../ingestion/tutorials/streaming-time-series-data.md)。

## 在一个HTTP请求中流化多条消息

将数据流化到Adobe Experience Platform时，进行大量HTTP调用可能会非常昂贵。 例如，创建1KB有效负荷的1个HTTP请求（每个消息200条，每个消息1KB）比创建200个HTTP请求（单个有效负荷200KB）效率更高。 正确使用时，在单个请求中对多个消息进行分组是优化发送到Experience Platform的数据的最佳方式。 要了解如何使用流摄取在单个HTTP请求中向Experience Platform发送多条消息，请遵循发 [送多条消息教程](../ingestion/tutorials/streaming-multiple-messages.md)。



