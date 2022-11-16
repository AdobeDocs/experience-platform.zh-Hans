---
title: Adobe Experience Platform中的数据加密
topic-legacy: data protection
description: 了解数据在传输中和在Adobe Experience Platform中存放时如何加密。
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: d99a9081edc483831d56af3d838b67d9aba25bea
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 3%

---

# Adobe Experience Platform中的数据加密

Adobe Experience Platform是一个功能强大且可扩展的系统，可跨企业解决方案集中化和标准化客户体验数据。 Platform使用的所有数据在传输过程中和静态时都经过加密，以保证数据的安全。 本文档从高级别介绍了平台的加密流程。

以下流程图说明了如何摄取、加密和保留数据 [!DNL Experience Platform]:

![](../images/governance-privacy-security/encryption/flow.png)

## 在途数据 {#in-transit}

平台与任何外部组件之间传输的所有数据均通过使用HTTPS的安全加密连接进行传输 [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

通常，数据通过三种方式引入平台：

* [数据收集](../../collection/home.md) 功能允许网站和移动设备应用程序将数据发送到Platform Edge Network以进行暂存和准备摄取。
* [源连接器](../../sources/home.md) 将数据从Adobe Experience Cloud应用程序和其他企业数据源直接流到平台。
* 非AdobeETL（提取、转换、加载）工具会将数据发送到 [批量摄取API](../../ingestion/batch-ingestion/overview.md) 消费。

在将数据导入系统后和 [已加密](#at-rest)，则可以通过Platform服务对其进行扩充，并通过以下方式从系统中引出：

* [目标](../../destinations/home.md) 允许您激活数据以Adobe应用程序和合作伙伴应用程序。
* 本机平台应用程序，例如 [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hans) 和 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=zh-Hans) 也可以利用数据。

## 静态数据 {#at-rest}

平台摄取和使用的数据存储在数据湖中，这是一个高度精细的数据存储，包含系统管理的所有数据，无论其来源或文件格式如何。 在数据湖中保留的所有数据都会在隔离的中进行加密、存储和管理 [[!DNL Microsoft Azure Data Lake] 存储](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) 您的组织特有的实例。

有关Azure数据湖存储中静态数据如何加密的详细信息，请参阅 [官方Azure文档](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## 后续步骤

本文档概要介绍了如何在Platform中加密数据。 有关Platform中安全过程的更多信息，请参阅 [管理、隐私和安全](./overview.md) Experience League，或查看 [平台安全白皮书](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
