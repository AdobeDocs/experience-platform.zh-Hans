---
title: Adobe Experience Platform发行说明2020年4月
description: 2020年4月的Adobe Experience Platform发行说明。
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

Adobe Experience Platform的新增功能：
* [[!DNL Intelligent Services]](#intelligent)

现有功能的更新：
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [数据管理](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] 使营销分析师和从业人员能够在客户体验用例中利用人工智能和机器学习的强大功能。 这允许营销分析人员使用业务级别配置来设置特定于公司需求的预测，而无需具备数据科学专业知识。 此外，营销从业者可以在Adobe Experience Cloud、Adobe Experience Platform和第三方应用程序中激活预测。

**主要功能**

| 功能 | 描述 |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] 为营销人员提供了在个人级别生成客户预测的功能，并提供了相关说明。 在影响因素的帮助下， [!DNL Customer AI] 可以告诉您客户可能执行的操作以及原因。 此外，营销人员还可以从 [!DNL Customer AI] 通过提供最合适的选件和消息传送来个性化客户体验的预测和分析。 |
| [!DNL Attribution AI] | [!DNL Attribution AI] 是一种多渠道算法归因服务，用于计算客户交互对指定结果的影响和增量影响。 利用 [!DNL Attribution AI]，营销人员可以通过了解客户旅程各个阶段每个客户互动的影响来衡量和优化营销和广告支出。 |

**已知问题**

* 当前没有已知问题。

有关 [!DNL Intelligent Services] 以及它要提供什么，看看 [智能服务概述](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM)系统 {#xdm}

标准化和互操作性是其背后的关键概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)在Adobe的驱动下，努力标准化客户体验数据并定义客户体验管理架构。

XDM是一项公开记录的规范，旨在提高数字体验的强大功能。 它为任何与Adobe Experience Platform上的服务通信的应用程序提供了通用结构和定义。 通过遵循XDM标准，所有客户体验数据都可以整合到通用呈现形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 自动备用显示信息 | 的 [!DNL Schema Registry] 自动应用在 `alternateDisplayInfo` 描述符。 |
| 标量字段限制 | 的 [!DNL Schema Registry] 在单个架构中不允许超过6000个标量字段。 |
| 性能检修 | 的 [!DNL Schema Registry] 已经过全面改版，以执行和满足 [!DNL Experience Platform] 更好。 |

**错误修复**

* 已将XDM更新为XDM，以支持标准XDM中嵌套URI字段的更简洁的XED格式。

**已知问题**

* 已知

## 数据管理 {#governance}

Adobe Experience Platform数据管理是用于管理客户数据并确保符合适用于数据使用的法规、限制和策略的一系列策略和技术。 它在 [!DNL Experience Platform] 在不同级别，包括编目、数据谱系、数据使用标签、数据访问策略以及对营销操作数据的访问控制。

要开始进行数据管理，必须全面了解适用于您的客户数据的法规、合同义务和公司政策。 在此，数据可以通过应用适当的数据使用标签来分类，并且其使用可以通过定义数据使用策略来控制。

数据管理框架通过 [!DNL Experience Platform] 用户界面和 [!DNL Policy Service] API。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 在UI中管理数据使用策略 | 数据使用策略现在可以在 **策略** 工作区 [!DNL Experience Platform] UI。 请参阅 [策略用户指南](../../data-governance/policies/user-guide.md) 以了解更多信息。 |

**已知问题**

* None.

有关详细信息，请参阅 [数据管理概述](../../data-governance/home.md).


## 目标 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目标是与目标平台的预建集成，可无缝地向这些合作伙伴激活数据。

**新目标**

Real-Time CDP现在支持将数据激活到超过五十个 [!DNL Experience Cloud Launch] 扩展，启用analytics、个性化和其他用例。 有关详细信息，请参阅下文：

| 文档 | 描述 |
|--- | ---|
| [目标类型和类别](../../destinations/destination-types.md) | 本文介绍了Real-Time CDP界面中连接和扩展之间的区别，并建议何时使用这些目标。 |
| [Experience Platform Launch扩展](../../destinations/catalog/launch-extensions/overview.md) | 本页介绍 [!DNL Launch] 扩展包括，列出了使用这些扩展的用例，以及每个扩展的文档链接 [!DNL Launch] 扩展。Real-Time CDP |

有关详细信息，请参阅 [目标概述](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

新的法律和组织规定正在用户提供相应的权利，允许他们请求访问或删除您的数据存储中的用户个人数据。Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和用户界面，帮助您管理来自客户的这些数据请求。 使用 [!DNL Privacy Service]，您可以提交从Adobe Experience Cloud应用程序访问和删除私有或个人客户数据的请求，以便自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| PDPA支持 | 现在，可以根据泰国的个人数据保护法(PDPA)创建和跟踪隐私请求。 在API中发出隐私请求时， `regulation` 数组接受值“pdpa_tha”。 |
| UI中的命名空间类型 | 现在，您可以在 [!DNL Privacy Service] UI。 请参阅 [用户指南](../../privacy-service/ui/user-guide.md) 以了解更多信息。 |
| 弃用旧端点 | 旧API端点(`data/privacy/gdpr`)已被弃用。 |

已知问题

* None

有关 [!DNL Privacy Service]，请首先阅读 [Privacy Service概述](../../privacy-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用 [!DNL Platform] 服务。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform] 提供了RESTful API和交互式UI，让您能够轻松为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据库的API和UI支持 | 新的源连接器 [!DNL Apache Spark] （在HDInsights上）， [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] （在HDInsights上）和 [!DNL Phoenix]. |
| 对基于支付的应用程序的API和UI支持 | 新的源连接器 [!DNL PayPal]. |
| 对基于协议的应用程序的API和UI支持 | 新的源连接器 [!DNL Generic OData]. |

**已知问题**

* 无

要进一步了解源，请参阅 [源概述](../../sources/home.md).
