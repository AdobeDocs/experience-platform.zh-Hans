---
title: Adobe Experience Platform中的数据加密
description: 了解如何在Adobe Experience Platform中加密传输中数据和静态数据。
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 3%

---

# Adobe Experience Platform中的数据加密

Adobe Experience Platform是一个功能强大且可扩展的系统，它跨企业解决方案集中化和标准化客户体验数据。 Platform使用的所有数据在传输和静止时都经过加密，以确保您的数据安全。 本文档从较高层面介绍了Platform的加密过程。

以下流程图说明了如何摄取、加密和保留数据 [!DNL Experience Platform]：

![](../images/governance-privacy-security/encryption/flow.png)

## 正在传输的数据 {#in-transit}

在Platform和任何外部组件之间传输的所有数据都是使用HTTPS通过安全、加密的连接进行的 [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

通常，数据是通过三种方式引入Platform的：

* [数据收集](../../collection/home.md) 功能允许网站和移动应用程序将数据发送到Platform Edge Network以进行暂存和摄取准备。
* [源连接器](../../sources/home.md) 从Adobe Experience Cloud应用程序和其他企业数据源直接将数据流式传输到Platform。
* 非AdobeETL（提取、转换、加载）工具将数据发送到 [批量摄取API](../../ingestion/batch-ingestion/overview.md) 用于消费。

在将数据引入系统之后，以及 [静态加密](#at-rest)，然后可以通过Platform服务对其进行丰富，并通过以下方式从系统中引入：

* [目标](../../destinations/home.md) 允许您激活数据以Adobe应用程序和合作伙伴应用程序。
* 本机平台应用程序，例如 [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hans) 和 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) 还可以利用数据。

## 静态数据 {#at-rest}

Platform摄取和使用的数据存储在数据湖中，数据湖是一个高度精细化的数据存储区，包含由系统管理的所有数据，而不管其来源或文件格式如何。 所有保留在数据湖中的数据都在一个隔离的环境中进行加密、存储和管理 [[!DNL Microsoft Azure Data Lake] 存储](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) 特定于您组织的实例。

有关如何在Azure Data Lake Storage中加密静态数据的详细信息，请参阅 [Azure官方文档](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## 后续步骤

本文档提供了如何在Platform中加密数据的高级概述。 有关Platform中安全程序的更多信息，请参阅 [治理、隐私和安全](./overview.md) Experience League时，或查看 [平台安全白皮书](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
