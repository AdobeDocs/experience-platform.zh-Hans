---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform中的数据保护
topic: data protection
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Adobe Experience Platform中的数据保护

Adobe Experience Platform摄取和使用的所有数据都存储在一个高度粒度的数据存储 [!DNL Data Lake]中，它包含由所有管理的所有数据， [!DNL Platform]而不管来源或文件格式。 在单位独有的 [!DNL Data Lake] 隔离存储帐户中，对保留在该帐户中的所 [!DNL Microsoft Azure Data Lake] 有数据进行加密、存储和管理。

以下流程图说明了数据的摄取、处理、加密和保留方式 [!DNL Experience Platform]:

![](images/data-protection/flow.png)

有关静态数据如何在中加密的详细信 [!DNL Data Lake Storage]息，请参阅Azure数 [据湖存储中的数据加密文档](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)。 有关静态数据如何在中加密的信 [!DNL Cosmos DB]息，请参阅Azure Cosmos [DB中的文档数据加密](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)。