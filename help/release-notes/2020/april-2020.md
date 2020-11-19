---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年4月8日
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 8%

---


# Adobe Experience Platform 发行说明

**发行日期：2020 年 4 月 8 日**

Adobe Experience Platform的新增功能：
* [[!DNL Intelligent Services]](#intelligent)

对现有功能的更新：
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [[!DNL Data Governance]](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] 使营销分析师和从业人员能够在客户体验使用案例中利用人工智能和机器学习的强大功能。 这使营销分析师能够使用业务级配置设置特定于公司需求的预测，而无需数据科学专业知识。 此外，营销从业者可以在Adobe Experience Cloud、Adobe Experience Platform和第三方应用程序中激活预测。

**主要功能**

| 功能 | 描述 |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] 为营销人员提供在个人层面生成客户预测的能力，并提供解释。 在影响因素的帮助下， [!DNL Customer AI] 您可以了解客户可能做什么以及为什么。 此外，营销人员还可以从预 [!DNL Customer AI] 测和洞察中受益，通过提供最合适的优惠和消息来个性化客户体验。 |
| [!DNL Attribution AI] | [!DNL Attribution AI] 是一种多渠道、算法归因服务，用于计算客户交互对特定结果的影响和增量影响。 利用 [!DNL Attribution AI]，营销人员可以通过了解客户旅程各个阶段每个客户互动的影响来衡量和优化营销和广告支出。 |

**已知问题**

* 当前没有已知问题。

有关此服务的 [!DNL Intelligent Services] 详细信息以及它需要优惠的内容，请参 [阅智能服务概述](../../intelligent-services/home.md)。

## [!DNL Experience Data Model] (XDM)系统 {#xdm}

标准化和互操作性是背后的关键概念 [!DNL Experience Platform]。 [!DNL Experience Data Model] (XDM)由Adobe驱动，旨在实现客户体验数据标准化并定义客户体验管理模式。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为任何与Adobe Experience Platform上的服务通信的应用程序提供了通用结构和定义。 通过遵守XDM标准，所有客户体验数据都可以整合到一个通用表现形式中，以更快、更集成的方式提供洞察。 您可以从客户行动中获得宝贵的洞察，通过细分定义客户受众，并将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 自动替代显示信息 | 自 [!DNL Schema Registry] 动应用描述符中配置的自定义标题和描述 `alternateDisplayInfo` 值。 |
| 标量字段限制 | 在 [!DNL Schema Registry] 单个模式中不允许超过6000个标量字段。 |
| 性能检查 | 已 [!DNL Schema Registry] 经过全面改造，以更好地执行和满足 [!DNL Experience Platform] 要求。 |

**错误修复**

* 将XDM更新为XDM，转换为XDM，支持标准XDM中嵌套URI字段的更简洁的XED格式。

**已知问题**

* 已知

## [!DNL Data Governance] {#governance}

Adobe Experience Platform [!DNL Data Governance] 是用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策的一系列战略和技术。 它在各个层次中都起 [!DNL Experience Platform] 着关键作用，包括编目、数据谱系、数据使用标签、数据访问策略和访问控制营销行动的数据。

要开始进行数据治理，必须全面了解适用于客户数据的法规、合同义务和公司政策。 从那里，可以通过应用适当的数据使用标签来对数据进行分类，并且可以通过定义数据使用策略来控制其使用。

该框 [!DNL Data Governance] 架通过用户界面和API简化数据分类和创建数据使用策略 [!DNL Experience Platform] 的过程并简 [!DNL Policy Service] 化。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 在UI中管理数据使用策略 | 数据使用策略现在可以在UI的“策 **略** ”工作区中 [!DNL Experience Platform] 管理。 有关详细 [信息，请参阅](../../data-governance/policies/user-guide.md) “策略用户指南”。 |

**已知问题**

* None.

有关详细信息，请参阅数 [据管理概述](../../data-governance/home.md)。


## 目标 {#destinations}

在实 [时客户数据平台中](../../rtcdp/overview.md)，目标是预建的与目标平台集成，以无缝方式向这些合作伙伴激活数据。

**新目标**

Adobe实时CDP现在支持向50多个扩展进行数据激活 [!DNL Experience Cloud Launch] ，从而支持分析、个性化和其他使用案例。 有关详细信息，请参阅以下内容：

| 文档 | 描述 |
|--- | ---|
| [目标类型和类别](/help/rtcdp/destinations/destination-types.md) | 本文介绍了Adobe实时CDP接口中连接和扩展之间的区别，并建议何时使用这些目标。 |
| [Experience Platform Launch扩展](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | 本页介绍什 [!DNL Launch] 么是扩展，列表使用这些扩展的用例，以及Adobe实时CDP中每个扩 [!DNL Launch] 展的文档链接。 |

有关详细信息，请参阅目 [标概述](/help/rtcdp/destinations/destinations-overview.md)。

## [!DNL Privacy Service] {#privacy}

新的法律和组织法规授予用户根据请求从数据存储中访问或删除其个人数据的权利。 Adobe Experience Platform [!DNL Privacy Service] 提供了RESTful API和用户界面，帮助您管理来自客户的这些数据请求。 您可 [!DNL Privacy Service]以提交从Adobe Experience Cloud应用程序访问和删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| PDPA支持 | 现在，可以根据泰国的个人数据保护法(PDPA)创建和跟踪隐私请求。 在API中发出隐私请求时， `regulation` 阵列接受值“pdpa_tha”。 |
| UI中的命名空间类型 | 您现在可以在UI的Request Builder中指定不同的命名空间 [!DNL Privacy Service] 类型。 有关详细 [信息](../../privacy-service/ui/user-guide.md) ，请参阅用户指南。 |
| 旧端点弃用 | 旧API端点(`data/privacy/gdpr`)已弃用。 |

已知问题

* None

有关更多信 [!DNL Privacy Service]息，请阅读开始 [概述](../../privacy-service/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部来源收集数据，同时允许您使用服务来构建、标记和增强该 [!DNL Platform] 数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)收集数据。

[!DNL Experience Platform] 提供REST风格的API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据库的API和UI支持 | （在HDInsights上）、 [!DNL Apache Spark] 、 [!DNL Azure Synapse Analytics](在 [!DNL Azure Table Storage]HDInsights上)和的新源连接器 [!DNL Hive][!DNL Phoenix]。 |
| 对基于付款的应用程序的API和UI支持 | 新的源连接器 [!DNL PayPal]。 |
| 对基于协议的应用程序的API和UI支持 | 新的源连接器 [!DNL Generic OData]。 |

**已知问题**

* None

要进一步了解源，请参阅 [源概述](../../sources/home.md)。
