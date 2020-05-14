---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年5月13日
doc-type: release notes
last-update: May 13, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: e6731b54840eaf9dd2cdaeff5205e14277e78a3b
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 4%

---


# Adobe Experience Platform 发行说明

**发行日期：2020 年 5 月 13 日**

对Adobe Experience Platform中现有功能的更新：

- [Adobe Experience Platform 发行说明](#adobe-experience-platform-release-notes)
   - [用户界面更新 {#ux}](#user-interface-updates-ux)
   - [数据科学工作区 {#dsw}](#data-science-workspace-dsw)
   - [目标 {#destinations}](#destinations-destinations)
   - [Experience Platform Web SDK和Experience Platform Edge Network {#edge}](#experience-platform-web-sdk-and-experience-platform-edge-network-edge)
   - [源 {#sources}](#sources-sources)

## 用户界面更新 {#ux}

Adobe Experience Platform将发布域和标题栏的更新，以改进您的体验并与其他Experience Cloud应用程序统一。

- 更轻松地在组织之间或切换到其他应用程序
- 改进了用户帮助，包括“帮助”菜单中的特色文章和上下文相关文档
- 能够提供有关Experience Platform和文件支持票证的反馈

新体验的推出是渐进的。 您可以在https://experience.adobe.com/platform上视图 [体验](https://experience.adobe.com/platform)。

## 数据科学工作区 {#dsw}

数据科学工作区使用机器学习和人工智能从数据中释放洞察。 数据科学工作区集成到Adobe Experience Platform中，可帮助您跨Adobe解决方案使用内容和数据资产进行预测。 Data Science Workspace实现这一点的方法之一是使用JupyterLab。 JupyterLab是Project Jupyter的基于Web的 <a href="https://jupyter.org/" target="_blank">用户界面</a> ，与Adobe Experience Platform紧密集成。 它为数据科学家提供一个交互式开发环境，以便与Jupyter笔记本、代码和数据一起使用。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| JupyterLab Launcher | JupyterLab Launcher现在包括Spark 2.4笔记本的入门软件。 现在，Spark 2.3笔记本起始页已标记为已弃用，并且设置为在后续版本中删除。 |
| Spark 2.4 | 新的Scala(Spark)和PySpark菜谱现在使用Spark 2.4。 |
| 内核 | 现在，Scala(Spark)笔记本是通过Scala内核创作的。 PySpark笔记本现在通过Python Kernel进行创作。 Spark和PySpark内核已弃用，并设置为在后续版本中删除。 |
| 菜谱 | 新的PySpark和Spark菜谱现在采用类似于Python和R菜谱的Docker工作流程。 |

有关迁移笔记本电脑和方法以使用Spark 2.4的更多信息，请参阅笔记本 [电脑迁移指南](../../data-science-workspace/recipe-notebook-migration.md)。 有关数据科学工作区的更多一般信息，请参阅 [概述文档](../../data-science-workspace/home.md)。

## 目标 {#destinations}

在 [Adobe实时客户数据平台中](../../rtcdp/overview.md)，目标是预建的与目标平台集成，以无缝方式向这些合作伙伴激活数据。

**新目标**

Adobe实时CDP现在支持将激活存储流化到云目标，允许您将受众数据和事件以JSON格式导出到这些目标。 然后，您可以在目标事件上描述业务逻辑。 有关详细信息，请参阅以下内容：

>[!NOTE]
>
>Adobe [!DNL Amazon Kinesis] 实时 [!DNL Azure Event Hubs] CDP中的目标和目标目前都处于测试阶段。 文档和功能可能会发生变化。

| 文档 | 描述 |
|--- | ---|
| [（测试版）Amazon Kinesis目标](/help/rtcdp/destinations/amazon-kinesis-destination.md) | 本文介绍如何创建与存储的实时出站连接， [!DNL Amazon Kinesis] 以从Adobe Experience Platform流化数据。 |
| [（测试版）Azure事件集线器目标](/help/rtcdp/destinations/azure-event-hubs-destination.md) | 本文介绍如何创建与存储的实时出站连接， [!DNL Azure Event Hubs] 以从Adobe Experience Platform流化数据。 |
| [API教程——连接到流目标并激活数据](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md) | 本教程演示如何使用API调用连接到您的Adobe Experience Platform存储、创建到流式云事件目标（Amazon Kinesis或Azure集线器）的连接、创建到新创建目标的数据流以及将数据激活到新创建的目标。 |

有关详细信息，请参阅目 [标概述](/help/rtcdp/destinations/destinations-overview.md)。

## Experience Platform Web SDK和Experience Platform Edge Network {#edge}

Experience Platform Web SDK和Experience Platform Edge Network允许用户将数据实时发送到Adobe Experience Platform和其他Adobe解决方案，以用于最终用户设备和浏览器。 最新的使用案例列表可在我们的公 [共路线图](https://github.com/adobe/alloy/projects/5) （经常更新）中找到。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| 支持ECID | SDK支持ECID开箱即用，无需安装任何其他库或信息 |
| 配置UI | 在启动项中使用新的边缘配置UI管理配置ID设置，必须将其列入白名单才能访问 |
| Adobe Experience Platform Web SDK Mixin | 与包含所有受支持字段的Experience Platform Web SDK一起使用的混合。 |
| 课程同意控制 | 为公司提供对Experience Platform Web SDK的加入和退出的控制 |
| 新的Experience Cloud调试器扩展中的客户端调试支持 | 查看Experience Platform Web SDK的请求和边缘跟踪，以了解数据如何在系统中流动。 |
| Adobe Analytics | 通过边缘配置将数据发送到Analytics报表包。 XDM被拼合到上下文数据中，支持多套件标记 |
| Adobe Target | 支持Adobe目标。 包括VEC、基于表单的书写器、A/B、XT、自动个性化、MVT |
| Adobe受众管理器支持 | 支持受众管理器ID同步、URL目标和Cookie目标 |
| 身份同步 | 重命 `setCustomersIds` 名 `syncIdentity` 为，以便更加清楚 |
| XDM Object Builder | 在启动扩展中，您现在可以将XDM对象构建为数据元素 |

有关Platform Web SDK和Edge Network的更多信息，请参阅 [文档](../../edge/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源收集数据，同时允许您使用平台服务构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)收集数据。

Experience Platform提供REST风格的API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 对云存储系统的更多API和UI支持 | Azure文件存储的新源连接器。 |
| 对数据库的其他API和UI支持 | Azure Data Explorer、IBM DB2和Oracle DB的新源连接器。 |
| Adobe受众管理器到Experience Platform数据共享 | 受众管理器连接器的设置过程已更新。 现在，实时受众用户档案的管理器数据集默认处于禁用状态。 您可以手动选择要提升到用户档案的数据集。 新的默认设置不具有追溯性，并且仅影响新受众管理器连接器的设置。 请参阅数据集用户指 [南中的更多信息](../../catalog/datasets/user-guide.md)。 |

**已知问题**

- None

要进一步了解源，请参阅 [源概述](../../sources/home.md)。