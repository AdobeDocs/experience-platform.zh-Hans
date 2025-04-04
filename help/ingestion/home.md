---
keywords: Experience Platform；主页；热门主题；数据摄取；数据位置；数据管理；数据管理；谱系；谱系；批次；批次；摄取的数据
solution: Experience Platform
title: 数据引入概述
description: 本文档介绍了将数据摄取到Experience Platform的三种主要方式，并提供了指向各自概述文档的链接，以详细了解相关信息。
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# 数据引入概述

Adobe Experience Platform将来自多个来源的数据整合在一起，以帮助营销人员更好地了解其客户的行为。 Adobe Experience Platform Data Ingestion表示Experience Platform从这些来源摄取数据的多种方法，以及该数据如何在Data Lake中保留以供下游Experience Platform服务使用。

本文档介绍了将数据摄取到Experience Platform的三种主要方式，并提供了指向各自概述文档的链接，以详细了解相关信息。

## 批量摄取

批量摄取允许您将数据作为批处理文件摄取到[!DNL Experience Platform]。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。 摄取后，批量会提供元数据以描述已成功摄取的记录数，以及任何失败记录和关联的错误消息。

必须使用此方法摄取手动上传的数据文件，如映射到XDM架构的平面CSV文件和Parquet Dataframe。

有关详细信息，请参阅[批次摄取概述](./batch-ingestion/overview.md)。

>[!TIP]
>
>使用单行JSON而不是多行JSON作为批量摄取的输入。 单行JSON可以提高性能，因为系统可以将一个输入文件划分为多个块并并行处理，而多行JSON无法拆分。 这可以显着降低数据处理成本并改善批处理延迟。

## 流式摄取

流式摄取允许您实时将数据从客户端和服务器端设备发送到[!DNL Experience Platform]。 Experience Platform支持使用数据入口来流式传输传入体验数据，这些数据会保留在数据湖内启用流式传输的数据集中。 可将数据入口配置为自动验证其收集的数据，确保数据来自可信来源。

有关详细信息，请参阅[流式摄取概述](./streaming-ingestion/overview.md)。

## 源

[!DNL Experience Platform]允许您设置到各种数据提供程序的源连接。 利用这些连接，可对外部数据源进行身份验证，设置摄取运行时间并管理摄取吞吐量。

可以将Source连接配置为从其他Adobe应用程序(如Adobe Analytics和Adobe Audience Manager)、第三方云存储源（如[!DNL Azure Blob]、[!DNL Amazon] S3、FTP服务器和SFTP服务器）以及第三方CRM系统（如[!DNL Microsoft Dynamics]和[!DNL Salesforce]）收集数据。

有关详细信息，请参阅[源概述](../sources/home.md)。

### ML辅助模式创建 {#ml-assisted-schema-creation}

为了快速集成新数据源，您现在可以使用机器学习算法从示例数据生成架构。 此自动化可简化准确架构的创建，减少错误，并加快从数据收集到分析和洞察的进程。

有关此工作流的详细信息，请参阅[ML辅助模式创建指南](../xdm/ui/ml-assisted-schema-creation.md)。

## 后续步骤和其他资源

本文档简要介绍了[!DNL Experience Platform]中[!DNL Data Ingestion]的各个方面。 请继续阅读每种摄取方法的概述文档，以熟悉其不同的功能、用例和最佳实践。 您还可以通过观看下方的摄取概述视频来补充学习。 有关[!DNL Experience Platform]如何跟踪所摄取记录的元数据的信息，请参阅[目录服务概述](../catalog/home.md)。

>[!WARNING]
>
>以下视频中使用的“统一配置文件”一词已过期。 术语[!DNL "Profile"]或[!DNL "Real-Time Customer Profile"]是[!DNL Experience Platform]文档中使用的正确术语。 请参阅文档以了解最新功能。

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
