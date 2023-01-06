---
keywords: Experience Platform；主页；热门主题；数据摄取；数据位置；数据位置；数据管理；数据管理；谱系；谱系；批量；批量；摄取数据
solution: Experience Platform
title: 数据摄取概述
description: 本文档介绍了将数据摄取到平台的三种主要方式，以及指向其各自概述文档的链接，以获取更多详细信息。
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 14%

---

# 数据摄取概述

Adobe Experience Platform 将来自多个来源的数据整合在一起，以帮助营销人员更好地了解其客户的行为。Adobe Experience Platform数据摄取表示通过 [!DNL Platform] 从这些源摄取数据，以及该数据在数据湖中如何保留以供下游使用 [!DNL Platform] 服务。

本文档介绍了将数据摄取到的三种主要方式 [!DNL Platform]，以及其各自的概述文档链接以获取更多详细信息。

## 批量摄取

批量摄取允许您将数据摄取到 [!DNL Experience Platform] 作为批处理文件。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。摄取后，批量会提供元数据以描述已成功摄取的记录数量，以及任何失败记录和关联的错误消息。

使用此方法必须摄取手动上传的数据文件，如平面CSV文件（映射到XDM模式）和Parquet数据帧。

请参阅 [批量摄取概述](./batch-ingestion/overview.md) 以了解更多信息。

## 流式摄取

流式摄取允许您将数据从客户端和服务器端设备发送到 [!DNL Experience Platform] 实时。 [!DNL Platform] 支持使用数据入口来流传入的体验数据，该数据将保留在数据湖中启用流的数据集中。 数据入口可以配置为自动验证它们收集的数据，确保数据来自可信来源。

请参阅 [流摄取概述](./streaming-ingestion/overview.md) 以了解更多信息。

## 源

[!DNL Experience Platform] 允许您设置与各种数据提供程序的源连接。 通过这些连接，您可以对外部数据源进行身份验证，设置摄取运行的时间，以及管理摄取吞吐量。

可以将源连接配置为从其他Adobe应用程序(如Adobe Analytics和Adobe Audience Manager)、第三方云存储源(如 [!DNL Azure Blob], [!DNL Amazon] S3、FTP服务器和SFTP服务器)以及第三方CRM系统(例如 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce])。

请参阅 [源概述](../sources/home.md) 以了解更多信息。

## 后续步骤和其他资源

本文件简要介绍 [!DNL Data Ingestion] in [!DNL Experience Platform]. 请继续阅读每种摄取方法的概述文档，以熟悉其不同功能、用例和最佳实践。 您还可以通过观看下面的摄取概述视频来补充您的学习。 有关如何 [!DNL Experience Platform] 跟踪已摄取记录的元数据，请参阅 [目录服务概述](../catalog/home.md).

>[!WARNING]
>
>以下视频中使用的术语“统一用户档案”已过期。 术语 [!DNL "Profile"] 或 [!DNL "Real-Time Customer Profile"] 是 [!DNL Experience Platform] 文档。 有关最新功能，请参阅相关文档。

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
