---
keywords: Experience Platform;home;popular topics;data ingestion;data location;Data Location;Data management;data management;Lineage;lineage;batch;Batch;ingested data
solution: Experience Platform
title: Adobe Experience Platform数据摄取概述
topic: overview
description: 本文档介绍了将数据引入平台的三种主要方式，其中包含指向各自概述文档的链接，以获得更多详细信息。
translation-type: tm+mt
source-git-commit: 6e4a3ebe84c82790f58f8ec54e6f72c2aca0b7da
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 9%

---


# 数据摄取概述

Adobe Experience Platform将来自多个来源的数据整合在一起，以帮助营销人员更好地了解其客户的行为。 Adobe Experience Platform数据摄取表示从这些 [!DNL Platform] 来源收集数据的多种方法，以及数据在数据湖中保留以供下游服务使 [!DNL Platform] 用。

本文档介绍了三种主要的数据摄取方式， [!DNL Platform]其中包含指向各自概述文档的链接，以获取更多详细信息。

## 批量摄取

批处理摄取允许您将数据作为批 [!DNL Experience Platform] 处理文件摄取。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。摄取后，批量会提供元数据以描述已成功摄取的记录数量，以及任何失败记录和关联的错误消息。

必须使用此方法摄取手动上传的数据文件，如平面CSV文件(映射到XDM模式)和Parke。

有关更多 [信息，请参阅](./batch-ingestion/overview.md) “批量摄取概述”。

## 流摄取

流摄取允许您将数据从客户端和服务器端设备 [!DNL Experience Platform] 实时发送到。 [!DNL Platform] 支持使用数据入口来流传入的体验数据，这些数据会保留在数据湖中支持流的数据集中。 数据入口可以配置为自动验证它们收集的数据，确保数据来自可信源。

有关更多 [信息，请参](./streaming-ingestion/overview.md) 阅流式摄取概述。

## 源

[!DNL Experience Platform] 允许您设置与各种数据提供者的源连接。 这些连接使您能够验证到外部数据源、设置摄取运行的时间以及管理摄取吞吐量。

源连接可配置为从其他Adobe应用程序(如Adobe Analytics和Adobe Audience Manager)、第三方云存储源(如 [!DNL Azure Blob]S3 [!DNL Amazon] 、FTP服务器和SFTP服务器)以及第三方CRM系统(如 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce])收集数据。

See the [Sources overview](../sources/home.md) for more information.

## 后续步骤和其他资源

本文档简要介绍了中的不同方 [!DNL Data Ingestion] 面 [!DNL Experience Platform]。 请继续阅读每种摄取方法的概述文档，以熟悉其不同功能、使用案例和最佳实践。 您还可以通过观看下面的摄取概述视频来补充您的学习。 有关如何跟踪所 [!DNL Experience Platform] 摄取记录的元数据的信息，请参 [阅目录服务概述](../catalog/home.md)。

>[!WARNING]
>
>以下视频中使用的术语“统一用户档案”已过期。 术语或 [!DNL "Profile"] 是文 [!DNL "Real-time Customer Profile"] 档中使用的正确术语 [!DNL Experience Platform] 。 有关最新功能，请参阅文档。

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)