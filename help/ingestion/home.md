---
keywords: Experience Platform；主页；热门主题；数据摄取；数据位置；数据管理；数据管理；谱系；谱系；批次；批次；摄取的数据
solution: Experience Platform
title: 数据摄取概述
description: 本文档介绍了将数据摄取到Platform的三种主要方式，并提供了指向各自概述文档的链接，以详细了解相关信息。
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 15%

---

# 数据引入概述

Adobe Experience Platform 将来自多个来源的数据整合在一起，以帮助营销人员更好地了解其客户的行为。Adobe Experience Platform数据摄取表示多种方法，其中 [!DNL Platform] 从这些源摄取数据，以及这些数据如何保留在数据湖中以供下游使用 [!DNL Platform] 服务。

本文档介绍了将数据摄取的三种主要方式 [!DNL Platform]，并带有指向其各自概述文档的链接，以获取更多详细信息。

## 批量摄取

批量摄取允许您将数据摄取到 [!DNL Experience Platform] 作为批处理文件。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。摄取后，批量会提供元数据以描述已成功摄取的记录数量，以及任何失败记录和关联的错误消息。

必须使用此方法摄取手动上传的数据文件，例如平面CSV文件（映射到XDM架构）和Parquet数据帧。

请参阅 [批量摄取概述](./batch-ingestion/overview.md) 了解更多信息。

## 流式摄取

流式摄取允许您将数据从客户端和服务器端设备发送到 [!DNL Experience Platform] 实时。 [!DNL Platform] 支持使用数据入口来流式传输传入体验数据，该数据会保留在数据湖内支持流式传输的数据集中。 可以配置数据入口以自动验证他们收集的数据，确保数据来自可信来源。

请参阅 [流式摄取概述](./streaming-ingestion/overview.md) 了解更多信息。

## 源

[!DNL Experience Platform] 允许您设置到各种数据提供程序的源连接。 通过这些连接，可对外部数据源进行身份验证、设置摄取运行时间并管理摄取吞吐量。

可以将源连接配置为从其他Adobe应用程序(例如Adobe Analytics和Adobe Audience Manager)和第三方云存储源(例如 [!DNL Azure Blob]， [!DNL Amazon] S3、FTP服务器和SFTP服务器)以及第三方CRM系统(例如 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce])。

请参阅 [源概述](../sources/home.md) 了解更多信息。

## 后续步骤和其他资源

本文档简要介绍了 [!DNL Data Ingestion] 在 [!DNL Experience Platform]. 请继续阅读每种摄取方法的概述文档，以熟悉其不同的功能、用例和最佳实践。 您还可以通过观看下面的摄取概述视频来补充您的学习。 有关以下方面的信息： [!DNL Experience Platform] 跟踪所摄取记录的元数据，请参见 [目录服务概述](../catalog/home.md).

>[!WARNING]
>
>以下视频中使用的“统一配置文件”一词已过期。 条款 [!DNL "Profile"] 或 [!DNL "Real-Time Customer Profile"] 中使用的术语是否正确 [!DNL Experience Platform] 文档。 请参阅文档以了解最新功能。

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
