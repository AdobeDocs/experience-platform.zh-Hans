---
keywords: Experience Platform;home;popular topics;catalog;data protection;encryption data lake
solution: Experience Platform
title: Adobe Experience Platform的数据保护
topic: data protection
description: 在数据湖中保留的所有数据都经过加密、存储和管理，并且使用一个独立的Microsoft Azure Data Lake存储帐户，该帐户对您的组织是独一无二的。 以下流程图说明了Experience Platform如何摄取、处理、加密和保留数据。
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Adobe Experience Platform的数据保护

Adobe Experience Platform摄取和使用的所有数据都存储在一个高度细 [!DNL Data Lake]粒度的数据存储中，它包含所有由管理的数据， [!DNL Platform]而不管来源或文件格式。 在单位独有的 [!DNL Data Lake] 隔离存储帐户中，对保留在该帐户中的所 [!DNL Microsoft Azure Data Lake] 有数据进行加密、存储和管理。

以下流程图说明了数据的摄取、处理、加密和保留方式 [!DNL Experience Platform]:

![](images/data-protection/flow.png)

有关静态数据如何在中加密的详细信 [!DNL Data Lake Storage]息，请参阅Azure数 [据湖存储中的数据加密文档](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)。 有关静态数据如何在中加密的信 [!DNL Cosmos DB]息，请参阅Azure Cosmos [DB中的文档数据加密](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)。