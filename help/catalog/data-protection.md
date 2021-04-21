---
keywords: Experience Platform；主页；热门主题；目录；数据保护；加密数据湖
solution: Experience Platform
title: Adobe Experience Platform中的数据保护
topic-legacy: data protection
description: 在数据湖中保留的所有数据都经过加密、存储和管理，而Microsoft Azure Data Lake存储帐户是您的组织特有的。 以下流程图说明了Experience Platform如何摄取、处理、加密和保留数据。
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Adobe Experience Platform中的数据保护

Adobe Experience Platform摄取和使用的所有数据都存储在[!DNL Data Lake]中，这是一个高度粒度的数据存储，包含由[!DNL Platform]管理的所有数据，而不管来源或文件格式。 在[!DNL Data Lake]中保留的所有数据都经过加密、存储和管理，并且是在您的组织特有的隔离的[!DNL Microsoft Azure Data Lake]存储帐户中。

以下流程图说明了[!DNL Experience Platform]如何摄取、处理、加密和保留数据：

![](images/data-protection/flow.png)

有关在[!DNL Data Lake Storage]中如何加密静态存储的详细信息，请参阅Azure Data Lake ](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)中关于[数据加密的文档。 有关在[!DNL Cosmos DB]中如何加密静态数据的信息，请参阅Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)中关于[数据加密的文档。
