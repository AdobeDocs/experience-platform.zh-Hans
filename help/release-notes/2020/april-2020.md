---
title: Adobe Experience Platform 发行说明（2020 年 4 月）
description: Adobe Experience Platform 的 2020 年 4 月发行说明。
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: 发行说明；
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 28%

---

# Adobe Experience Platform 发行说明

**发行日期： 2020年4月8日**

Adobe Experience Platform 的新功能：
* [[!DNL Intelligent Services]](#intelligent)

现有功能更新：
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [数据治理](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services]使营销分析师和从业人员能够在客户体验用例中利用人工智能和机器学习的强大功能。 借助此功能，营销分析人员可以使用业务级配置来设置特定于公司需求的预测，而无需具备数据科学专业知识。 此外，营销从业者可以在Adobe Experience Cloud、Adobe Experience Platform和第三方应用程序中激活预测。

**主要功能**

| 功能 | 描述 |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI]为营销人员提供了在个人层面生成客户预测并提供解释的能力。 在影响因素的帮助下，[!DNL Customer AI]可以告诉您客户可能会做什么以及为什么。 此外，营销人员可以从[!DNL Customer AI]预测和洞察中受益，通过提供最合适的优惠和消息传递来个性化客户体验。 |
| [!DNL Attribution AI] | [!DNL Attribution AI]是一种多渠道的算法归因服务，用于计算客户交互对指定结果的影响和增量影响。 通过使用[!DNL Attribution AI]，营销人员可以通过了解每个客户互动对客户历程各个阶段的影响来衡量和优化营销和广告支出。 |

**已知问题**

* 当前没有已知问题。

有关[!DNL Intelligent Services]及其所提供内容的详细信息，请参阅[智能服务概述](../../intelligent-services/home.md)。

## [!DNL Experience Data Model] (XDM)系统 {#xdm}

标准化和互操作性是[!DNL Experience Platform]背后的关键概念。 由Adobe驱动的[!DNL Experience Data Model] (XDM)致力于标准化客户体验数据并定义用于客户体验管理的架构。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为任何应用程序提供通用结构和定义，以便与Adobe Experience Platform上的服务进行通信。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 自动替代显示信息 | [!DNL Schema Registry]自动应用在`alternateDisplayInfo`描述符中配置的自定义标题和描述值。 |
| 标量字段限制 | [!DNL Schema Registry]不允许单个架构中标量字段超过6000个。 |
| 性能检修 | 已对[!DNL Schema Registry]进行了全面检查，以便更好地执行和满足[!DNL Experience Platform]的要求。 |

**错误修复**

* 已将XDM更新为XED，并将其转换为支持标准XDM中的嵌套URI字段使用更干净的XED格式。

**已知问题**

* 已知

## 数据治理 {#governance}

Adobe Experience Platform 数据治理是一系列策略和技术，用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策。它在 Experience Platform 的 [!DNL Experience Platform] 各个层面中发挥着关键作用，包括编目、数据谱系、数据使用标记、数据访问策略和营销操作数据访问控制。

开始使用数据治理需要彻底了解适用于您的客户数据的管理法规、合同义务和企业政策。 从那里，可以通过应用适当的数据使用标签对数据进行分类，并且可以通过定义数据使用策略来控制其使用。

数据管理框架简化并简化了通过[!DNL Experience Platform]用户界面和[!DNL Policy Service] API对数据进行分类和创建数据使用策略的过程。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 在 UI 中管理数据使用策略 | 现在可以在[!DNL Experience Platform] UI的&#x200B;**策略**&#x200B;工作区中管理数据使用策略。 有关详细信息，请参阅[策略用户指南](../../data-governance/policies/user-guide.md)。 |

**已知问题**

* 无。

有关详细信息，请参阅[数据管理概述](../../data-governance/home.md)。


## 目标 {#destinations}

在[Real-Time Customer Data Platform](../../rtcdp/overview.md)中，目标是与目标平台预先构建的集成，这些平台以无缝方式向这些合作伙伴激活数据。

**新目标**

Real-Time CDP现在支持数据激活超过50个[!DNL Experience Cloud Launch]扩展，可启用Analytics、个性化和其他用例。 有关详细信息，请参阅下文：

| 文档 | 描述 |
|--- | ---|
| [目标类型和类别](../../destinations/destination-types.md) | 本文说明了Real-Time CDP界面中连接和扩展之间的区别，并建议何时使用其中的每个目标。 |
| [Experience Platform Launch扩展](../../destinations/catalog/launch-extensions/overview.md) | 本页介绍什么是[!DNL Launch]扩展，列出使用它们的用例，以及指向Real-Time CDP中每个[!DNL Launch]扩展的文档的链接。 |

有关详细信息，请参阅[目标概述](../../destinations/home.md)。

## [!DNL Privacy Service] {#privacy}

新的法律和组织法规授予用户权利，允许他们根据请求从您的数据存储中访问或删除其个人数据。 Adobe Experience Platform [!DNL Privacy Service] 提供 RESTful API 和用户界面，帮助您管理客户数据请求。借助 [!DNL Privacy Service]，您可以提交从 Adobe Experience Cloud 应用程序访问和删除个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| PDPA 支持 | 现在，泰国可以根据个人数据保护法(PDPA)创建和跟踪隐私请求。 在 API 中发出隐私请求时，`regulation` 数组接受值“pdpa_tha”。 |
| UI 中的命名空间类型 | 您现在可以在 [!DNL Privacy Service] UI 中的请求构建器中指定不同的命名空间类型。请参阅[用户指南](../../privacy-service/ui/user-guide.md)，获取更多信息。 |
| 旧端点弃用 | 已弃用旧的 API 端点 (`data/privacy/gdpr`)。 |

已知问题

* None

有关[!DNL Privacy Service]的详细信息，请先阅读[Privacy Service概述](../../privacy-service/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强该数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform]提供了一个RESTful API和一个交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据库的API和用户界面支持 | [!DNL Apache Spark] （在HDInsights上）、[!DNL Azure Synapse Analytics]、[!DNL Azure Table Storage]、[!DNL Hive] （在HDInsights上）和[!DNL Phoenix]的新源连接器。 |
| 基于支付的应用程序的API和UI支持 | [!DNL PayPal]的新源连接器。 |
| 基于协议的应用程序的API和UI支持 | [!DNL Generic OData]的新源连接器。 |

**已知问题**

* None

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
