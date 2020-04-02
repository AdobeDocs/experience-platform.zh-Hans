---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据获取教程
topic: tutorial
translation-type: tm+mt
source-git-commit: 2020f4b88f81f2d4fe3cfbd91cd18119ae580f4f

---


# 将数据引入Experience Platform

Adobe Experience Platform将来自多个来源的数据整合在一起，以帮助营销人员更好地了解其客户的行为。 Adobe Experience Platform数据摄取表示平台从这些来源获取数据的多种方法，以及数据在数据湖中持续保存以供下游平台服务使用的方式。 数据摄取包括使用源连接器的批量摄取、流摄取和摄取。 要了解更多信息，请阅读 [数据摄取概述](../ingestion/home.md) ，或直接转到 [Sources文档](../source-connectors/home.md)。

## 在UI和API中创建源连接器

源连接器允许您从多个源中摄取数据，然后在这些源中使用平台服务进行标记、结构化和增强。 要开始使用UI创建连接器，请访问UI概 [述中的创建源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/sources-ui-tutorial.md)。 要使用API创建源连接器，请访 [问使用Flow Service API概述创建源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/sources-api-tutorial.md)。

## 摄取批量数据

Adobe Experience Platform允许您将数据作为批处理文件轻松导入到平台中。 要摄取的数据的示例可包括来自CRM系统（例如镶木文件）中的平面文件的用户档案数据或符合模式注册表中的已知体验数据模型(XDM)模式的数据。 要开始，请访问平台 [教程中的摄取数据](../ingestion/tutorials/ingest-batch-data.md)。

## 将CSV文件映射到XDM模式

要将CSV数据引入Adobe Experience Platform，必须将数据映射到体验数据模型(XDM)模式。 有关如何使用Experience Platform用户界面将CSV文件映射到XDM模式的步骤，请按照将CSV文件映 [射到XDM模式教程中的步骤操作](../ingestion/tutorials/map-a-csv-file.md)。

## 创建流连接

要将流数据开始到Experience Platform，您必须首先创建流HTTP连接。 创建流连接时，您需要提供关键详细信息，如流数据源，以及您是否打算从受信任的（已验证）源还是不受信任的（未验证）源发送数据。 这可以使用平台用户界面或Experience Platform API来完成。 要了解更多信息，请按照教程 [使用UI创建流连接](../ingestion/tutorials/create-streaming-connection-ui.md) ，或 [使用API创建流连接](../ingestion/tutorials/create-streaming-connection.md)。

## 创建经过身份验证的流连接

通过身份验证的数据收集，Adobe Experience Platform服务(如实时客户用户档案和身份)可区分来自可信来源和不可信来源的记录。 要开始，请按照教程创建经过 [身份验证的流连接](../ingestion/tutorials/create-authenticated-streaming-connection.md)。

## 流记录和时间序列数据

在数据集和流连接到位后，您可以将记录或时间序列数据流化到平台中。 要开始流记录数据，请按照流记录 [数据到平台教程中](../ingestion/tutorials/streaming-record-data.md)。 要开始流式传输时间序列数据，请将流 [式时间序列数据传输到平台中](../ingestion/tutorials/streaming-time-series-data.md)。

## 在一个HTTP请求中流化多个消息

将数据流化到Adobe Experience Platform时，进行大量HTTP调用可能非常昂贵。 例如，创建1KB负载的200个HTTP请求，而不是创建1KB负载的200个HTTP请求，创建1个HTTP请求，每个消息200条，单个负载200KB，效率更高。 正确使用时，在一个请求中对多个消息进行分组是优化发送到Experience Platform的数据的极好方法。 要了解如何使用流摄取在单个HTTP请求中向Experience Platform发送多条消息，请遵循发送 [多条消息教程](../ingestion/tutorials/streaming-multiple-messages.md)。



