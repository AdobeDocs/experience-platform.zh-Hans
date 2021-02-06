---
keywords: Experience Platform；主页；热门主题；数据摄取；数据定位；数据定位；数据管理;数据管理；世系；世系；批处理；批处理；摄取的数据
solution: Experience Platform
title: 数据摄取概述
topic: overview
description: 本文档介绍了将数据引入平台的三种主要方式，其中包含指向各自概述文档的链接，以获得更多详细信息。
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 9%

---


# 数据摄取概述

Adobe Experience Platform将来自多个来源的数据整合在一起，以帮助营销人员更好地了解其客户的行为。 Adobe Experience Platform数据摄取表示[!DNL Platform]从这些源中摄取数据的多种方法，以及该数据如何在数据湖中保留以供下游[!DNL Platform]服务使用。

本文档介绍了将数据引入[!DNL Platform]的三种主要方法，其中包含指向各自概述文档的链接，以获得更多详细信息。

## 批量摄取

批处理摄取允许您将数据作为批处理文件摄取到[!DNL Experience Platform]中。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。摄取后，批量会提供元数据以描述已成功摄取的记录数量，以及任何失败记录和关联的错误消息。

必须使用此方法摄取手动上传的数据文件，如平面CSV文件(映射到XDM模式)和Parke。

有关详细信息，请参阅[批处理摄取概述](./batch-ingestion/overview.md)。

## 流摄取

流式摄取允许您将数据从客户端和服务器端设备实时发送到[!DNL Experience Platform]。 [!DNL Platform] 支持使用数据入口来流传入的体验数据，这些数据会保留在数据湖中支持流的数据集中。数据入口可以配置为自动验证它们收集的数据，确保数据来自可信源。

有关详细信息，请参阅[流摄取概述](./streaming-ingestion/overview.md)。

## 源

[!DNL Experience Platform] 允许您设置与各种数据提供者的源连接。这些连接使您能够验证到外部数据源、设置摄取运行的时间以及管理摄取吞吐量。

源连接可配置为从其他Adobe应用程序(如Adobe Analytics和Adobe Audience Manager)、第三方云存储源（如[!DNL Azure Blob]、[!DNL Amazon] S3、FTP服务器和SFTP服务器）以及第三方CRM系统（如[!DNL Microsoft Dynamics]和[!DNL Salesforce]）收集数据。

有关详细信息，请参阅[源概述](../sources/home.md)。

## 后续步骤和其他资源

本文档简要介绍了[!DNL Experience Platform]中[!DNL Data Ingestion]的不同方面。 请继续阅读每种摄取方法的概述文档，以熟悉其不同功能、使用案例和最佳实践。 您还可以通过观看下面的摄取概述视频来补充您的学习。 有关[!DNL Experience Platform]如何跟踪所摄取记录的元数据的信息，请参阅[目录服务概述](../catalog/home.md)。

>[!WARNING]
>
>以下视频中使用的术语“统一用户档案”已过期。 术语[!DNL "Profile"]或[!DNL "Real-time Customer Profile"]是[!DNL Experience Platform]文档中使用的正确术语。 有关最新功能，请参阅文档。

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)