---
title: Snowflake概述
description: 了解Adobe Experience Platform中的事件转发Snowflake。
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: abddf0c4-3d4c-4f66-a6e0-c10b54ea3430
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# [!DNL Snowflake] 概述

[[!DNL Snowflake]](https://www.snowflake.com/en/)是一个云数据仓库，它可以在一个位置存储和分析您的所有数据记录。 它可以用于数据仓库、数据湖、数据工程、数据科学、数据应用开发，以及实时或共享数据的安全共享和使用。

[!DNL Snowflake]基于Amazon Web Services (AWS)、Microsoft Azure (Azure)和Google Cloud Platform (GCP)构建。

![显示[!DNL Snowflake]数据体系结构的图表。](../../../images/extensions/server/snowflake/snowflake.png)

## 我们的Snowflake集成

可以在以下任何云平台上托管Snowflake帐户：

- [Amazon Web Services ([!DNL AWS])](https://aws.amazon.com/) - [!DNL AWS]是一个云计算平台，可提供多种服务，如分布式计算、数据库存储、内容交付，以及用于客户关系管理(CRM)和企业资源规划(ERP)的软件即服务(SaaS)集成服务。

有关安装扩展和配置事件转发规则的更多信息，请参阅[[!DNL AWS] 概述](../aws/overview.md)。

- [Microsoft Azure ([!DNL Azure])](https://azure.microsoft.com/en-us/products/event-hubs/#overview) - [!DNL Azure]是一个云计算平台和一个在线门户，它允许您访问和管理Microsoft提供的云服务和资源。

有关安装扩展和配置事件转发规则的更多信息，请参阅[[!DNL Azure] 概述](../azure/overview.md)。

- [[!DNL Google Cloud Platform]](https://cloud.google.com/) - [!DNL Google Cloud Platform]是一个云计算平台，可提供多种服务，如分布式计算、数据库存储、内容交付，以及用于客户关系管理(CRM)和企业资源规划(ERP)的软件即服务(SaaS)集成服务。

有关安装扩展和配置事件转发规则的更多信息，请参阅[[!DNL Google Cloud Platform] 概述](../google-cloud-platform/overview.md)。

我们的本机[[!DNL AWS]](../aws/overview.md)、[[!DNL Azure]](../azure/overview.md)和[[!DNL Google Cloud Platform]](../google-cloud-platform/overview.md)事件转发扩展使客户能够实时收集、扩充其事件数据，并将其转发到其云服务，以供[!DNL Snowflake]使用。 请参阅下文：

![显示[!DNL AWS]和[!DNL Azure]之间链接的[!DNL Snowflake]报告图表。](../../../images/extensions/server/snowflake/snowflake-workflow.png)

## 后续步骤

本指南概述了[!DNL Snowflake]以及[!DNL AWS]和[!DNL Azure]事件转发扩展的使用。

有关Experience Platform中[!DNL AWS]和[!DNL Azure]事件转发功能的详细信息，请参阅[[!DNL AWS] 扩展概述](../aws/overview.md)和[[!DNL Azure] 扩展概述](../azure/overview.md)。
