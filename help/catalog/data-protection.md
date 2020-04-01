---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform中的数据保护
topic: data protection
translation-type: tm+mt
source-git-commit: edf7cef0991ceef0465d5c1d750bd1885754f716

---


# Adobe Experience Platform中的数据保护

Adobe Experience Platform摄取和使用的所有数据都存储在数据湖中，数据湖是一个高度粒度的数据存储库，它包含由平台管理的所有数据，而不考虑来源或文件格式。 在数据湖中保留的所有数据都经过加密、存储和管理，并且使用的是单位特有的孤立Microsoft Azure数据湖存储帐户。

以下流程图说明了Experience Platform如何摄取、处理、加密和保留数据：

![](images/data-protection/flow.png)

有关在数据湖存储中如何加密静态数据的详细信息，请参阅Azure数据湖存储 [中数据加密的文档](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)。 有关如何在Cosmos DB中加密静态数据的信息，请参阅Azure Cosmos DB中 [的数据加密文档](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)。