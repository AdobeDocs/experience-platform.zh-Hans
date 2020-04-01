---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform数据摄取概述
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# 数据摄取概述

Adobe Experience Platform将来自多个来源的数据整合在一起，以帮助营销人员更好地了解其客户的行为。 Adobe Experience Platform数据摄取表示平台从这些来源获取数据的多种方法，以及数据在数据湖中持续保存以供下游平台服务使用的方式。

本文档介绍了将数据引入平台的三种主要方式，并提供了相应概述文档的链接以获取更多详细信息。

## 批量摄取

批量摄取允许您将数据作为批量文件摄取到Experience Platform中。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。 摄取后，批处理将提供描述成功摄取的记录数以及任何失败记录和关联的错误消息的元数据。

必须使用此方法摄取手动上传的数据文件，如平面CSV文件(映射到XDM模式)和Parce数据帧。

有关详细 [信息，请参阅批摄取概述](./batch-ingestion/overview.md) 。

## 流摄取

流摄取允许您将数据从客户端和服务器端设备实时发送到Experience Platform。 平台支持使用数据入口来流化传入的体验数据，该数据保留在数据湖内支持流化的数据集中。 数据入口可以配置成自动验证它们收集的数据，确保数据来自可信源。

有关更多 [信息，请参阅流摄取概述](./streaming-ingestion/overview.md) 。

## 来源

Experience Platform允许您设置与各种数据提供商的源连接。 这些连接使您能够验证到外部数据源、设置摄取运行的时间以及管理摄取吞吐量。

可以将源连接配置为从其他Adobe应用程序(如Adobe Analytics和Adobe受众管理器)、第三方云存储源（如Azure Blob、Amazon S3、FTP服务器和SFTP服务器）和第三方CRM系统（如Microsoft Dynamics和Salesforce）收集数据。

有关详细 [信息，请参阅](../source-connectors/home.md) “源”概述。

## 后续步骤

本文档简要介绍了Experience Platform中数据摄取的不同方面。 请继续阅读每种摄取方法的概述文档，以熟悉其不同功能、用例和最佳实践。 有关Experience Platform如何跟踪所摄取记录的元数据的信息，请参阅 [Catalog Service概述](../catalog/home.md)。