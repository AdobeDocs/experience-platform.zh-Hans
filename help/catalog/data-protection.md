---
keywords: Experience Platform；主页；热门主题；目录；数据保护；加密数据湖
solution: Experience Platform
title: Adobe Experience Platform的数据保护
topic: data protection
description: 在数据湖中保留的所有数据都经过加密、存储和管理，并且使用一个独立的Microsoft Azure Data Lake存储帐户，该帐户对您的组织是独一无二的。 以下流程图说明了Experience Platform如何摄取、处理、加密和保留数据。
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Adobe Experience Platform的数据保护

Adobe Experience Platform摄取和使用的所有数据都存储在[!DNL Data Lake]中，这是一个高度精细的数据存储，包含由[!DNL Platform]管理的所有数据，而不管来源或文件格式。 在您的组织特有的隔离的[!DNL Microsoft Azure Data Lake]存储帐户中，对[!DNL Data Lake]中保留的所有数据进行加密、存储和管理。

以下流程图说明了[!DNL Experience Platform]如何摄取、处理、加密和保留数据：

![](images/data-protection/flow.png)

有关在[!DNL Data Lake Storage]中如何加密静态数据的详细信息，请参阅Azure数据湖存储](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)中关于[数据加密的文档。 有关在[!DNL Cosmos DB]中如何加密静态数据的信息，请参见Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)中关于[数据加密的文档。