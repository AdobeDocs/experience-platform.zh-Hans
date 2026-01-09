---
keywords: Experience Platform；查询服务；查询服务
title: Adobe Experience Platform查询服务快速入门
description: 全面利用Adobe Experience Platform查询服务的必要步骤的细分
exl-id: 36ab9354-23f9-4cb8-bcd4-00fe076386ab
source-git-commit: fa22a0ca0c79d5d62fd39de3a808f84a11a80c4d
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Adobe Experience Platform [!DNL Query Service]快速入门 {#getting-started}

使用Adobe Experience Platform查询服务对摄取的数据集运行SQL查询，联接来自多个源的数据，并生成用于分析、机器学习工作流或实时客户个人资料的派生数据集。 摄取数据后，通过UI访问查询服务以进行交互式分析和协作，或者通过API访问查询服务以进行自动化和程序化的查询执行。

## 先决条件 {#prerequisites}

在开始查询数据之前，请确保您具有：

- **所需权限**：您的用户帐户有权访问Experience Platform中的查询服务。 如果服务在UI中不可用，请查看[权限文档](../../access-control/home.md#permissions)并与系统管理员联系。
- **数据摄取**：您已将数据摄取到Experience Platform。

如果需要摄取数据，请查看[数据摄取教程视频](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=zh-Hans)，以了解有关数据集创建、架构映射、摄取和验证的概述。 有关更深入的信息和其他学习资源的链接，请阅读[引入概述文档](../../ingestion/home.md)。

## 快速入门路径

将数据引入Experience Platform后，您可以使用Experience Platform中的[!DNL Query Editor]或查询服务API开始使用查询服务。

### [!DNL Query Editor]

使用[!DNL Query Editor]进行分析、数据探索和协作查询开发。 有关UI功能的概述，请参阅[查询服务UI文档](../ui/overview.md)。 要了解如何在UI中编写和运行查询，请阅读[[!DNL Query Editor user guide]](../ui/user-guide.md)。

### 查询服务API

使用查询服务API实现自动化工作流、查询模板管理和程序集成。 有关使用查询服务API的详细说明，请参阅[查询服务开发人员指南](../api/getting-started.md)。

## 后续步骤

本文档介绍了在Experience Platform中使用[!DNL Query Service]功能所需的先决条件。 要快速开始使用查询服务功能，建议您阅读以下文档：

- [查询执行的一般指导](../best-practices/writing-queries.md)
- [查询服务中的SQL语法](../sql/syntax.md)
- [使用SQL创建派生数据集](../data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

或者，要详细了解查询服务如何有利于Experience Platform中的数据处理，请观看[放弃的Browse用例演示](../use-cases/abandoned-browse.md#video-example)。

以下资源有助于您更好地了解[!DNL Query Service]：

- [[!DNL Query Service] UI 概述](../ui/overview.md)
- [[!DNL Query Service]凭据](../ui/credentials.md)
- [客户端连接概述](../clients/overview.md)
