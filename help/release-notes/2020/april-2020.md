---
title: Adobe Experience Platform发行说明2020年4月
description: Adobe Experience Platform 2020年4月版发行说明。
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: 发行说明;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 10%

---

# Adobe Experience Platform 发行说明

**发布日期：2020 年 4 月 8 日**

Adobe Experience Platform中的新增功能：
* [[!DNL Intelligent Services]](#intelligent)

现有功能的更新：
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [数据治理](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] 让营销分析师和从业人员能够在客户体验用例中利用人工智能和机器学习的强大功能。 这允许营销分析人员使用业务级别配置设置特定于公司需求的预测，而无需数据科学专业知识。 此外，营销从业者可以在Adobe Experience Cloud、Adobe Experience Platform和第三方应用程序中激活预测。

**主要功能**

| 功能 | 描述 |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] 为营销人员提供了在个人层面生成客户预测并提供解释的能力。 在影响因素的帮助下， [!DNL Customer AI] 可以告诉您客户可能会做什么以及为什么。 此外，营销人员还可以从 [!DNL Customer AI] 预测和洞察，通过提供最合适的优惠和消息传送来个性化客户体验。 |
| [!DNL Attribution AI] | [!DNL Attribution AI] 是一种多渠道的算法归因服务，用于计算客户交互对指定结果的影响和增量影响。 利用 [!DNL Attribution AI]，营销人员可以通过了解客户历程各个阶段每个客户互动的影响来衡量和优化营销和广告支出。 |

**已知问题**

* 当前没有已知问题。

有关的详细信息 [!DNL Intelligent Services] 以及它所提供的功能，请参见 [智能服务概述](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM)系统 {#xdm}

标准化和互操作性是背后的关键概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)由Adobe驱动，致力于标准化客户体验数据并定义用于客户体验管理的架构。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为任何应用程序提供通用结构和定义，以便与Adobe Experience Platform上的服务进行通信。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 自动替代显示信息 | 此 [!DNL Schema Registry] 自动应用中配置的自定义标题和描述值 `alternateDisplayInfo` 描述符。 |
| 标量字段限制 | 此 [!DNL Schema Registry] 不允许在单个架构中存在6000个以上的标量字段。 |
| 性能检修 | 此 [!DNL Schema Registry] 进行了全面整修，以履行和满足 [!DNL Experience Platform] 好多了。 |

**错误修复**

* 将XDM更新为XED，转换为支持标准XDM中嵌套URI字段的更干净的XED格式。

**已知问题**

* 已知

## 数据治理 {#governance}

Adobe Experience Platform数据管理是用于管理客户数据并确保遵守适用于数据使用的法规、限制和策略的一系列策略和技术。 它在以下方面发挥着关键作用 [!DNL Experience Platform] 在不同的级别，包括编目、数据谱系、数据使用标签、数据访问策略和对营销活动数据的访问控制。

开始使用数据治理需要全面了解适用于客户数据的管理法规、合同义务和企业政策。 从那里，可以通过应用适当的数据使用标签对数据进行分类，并且可以通过定义数据使用策略来控制其使用。

数据管理框架通过简化分类数据和创建数据使用策略的流程 [!DNL Experience Platform] 用户界面和 [!DNL Policy Service] API。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 在UI中管理数据使用策略 | 现在可以在中管理数据使用策略 **策略** 中的工作区 [!DNL Experience Platform] UI。 请参阅 [策略用户指南](../../data-governance/policies/user-guide.md) 了解更多信息。 |

**已知问题**

* None.

欲知更多信息，请参见 [数据治理概述](../../data-governance/home.md).


## 目标 {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md)，目标是预先构建的与目标平台的集成，可无缝地向这些合作伙伴激活数据。

**新目标**

Real-Time CDP现在支持将数据激活提高到50个以上 [!DNL Experience Cloud Launch] 扩展，启用analytics、个性化和其他用例。 有关详细信息，请参阅下文：

| 文档 | 描述 |
|--- | ---|
| [目标类型和类别](../../destinations/destination-types.md) | 本文说明了Real-Time CDP界面中连接和扩展之间的区别，并就何时使用其中每个目标提出建议。 |
| [Experience Platform Launch扩展](../../destinations/catalog/launch-extensions/overview.md) | 本页说明了 [!DNL Launch] 扩展是，列出了使用这些扩展的使用案例，以及指向每个扩展的文档的链接 [!DNL Launch] Real-Time CDP中的扩展。 |

欲知更多信息，请参见 [目标概述](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

新的法律和组织规定正在用户提供相应的权利，允许他们请求访问或删除您的数据存储中的用户个人数据。Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和用户界面，以帮助您管理来自客户的数据请求。 替换为 [!DNL Privacy Service]，您可以提交从Adobe Experience Cloud应用程序访问和删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| PDPA支持 | 现在可以在泰国根据《个人数据保护法》(PDPA)创建和跟踪隐私请求。 在API中提出隐私请求时， `regulation` 数组接受值“pdpa_tha”。 |
| UI中的命名空间类型 | 现在，您可以在的请求生成器中指定不同的命名空间类型 [!DNL Privacy Service] UI。 请参阅 [用户指南](../../privacy-service/ui/user-guide.md) 了解更多信息。 |
| 弃用旧端点 | 旧API端点(`data/privacy/gdpr`)已被弃用。 |

已知问题

* None

有关详情，请参阅 [!DNL Privacy Service]，请先阅读 [Privacy Service概述](../../privacy-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用来构建、标记和增强这些数据 [!DNL Platform] 服务。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

[!DNL Experience Platform] 提供了一个RESTful API和一个交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据库的API和用户界面支持 | 新的源连接器 [!DNL Apache Spark] （在HDInsights上）， [!DNL Azure Synapse Analytics]， [!DNL Azure Table Storage]， [!DNL Hive] （在HDInsights上），和 [!DNL Phoenix]. |
| 基于支付的应用程序的API和UI支持 | 新的源连接器 [!DNL PayPal]. |
| 基于协议的应用程序的API和UI支持 | 新的源连接器 [!DNL Generic OData]. |

**已知问题**

* None

要了解有关源的更多信息，请参阅 [源概述](../../sources/home.md).
