---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年4月8日
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 8cc3b63fc91877ca1337f65e8f5c0e949b7ef01f

---


# Adobe Experience Platform 发行说明

## 发行日期：2020 年 4 月 8 日

Adobe Experience Platform的新增功能：
* [智能服务](#intelligent)

对现有功能的更新：
* [体验数据模型(XDM)](#xdm)
* [数据管理](#governance)
* [目标](#destinations)
* [隐私服务](#privacy)
* [来源](#sources)

## 智能服务 {#intelligent}

智能服务使营销分析师和从业人员能够在客户体验使用案例中利用人工智能和机器学习的强大功能。 这使营销分析人员能够使用业务级配置设置特定于公司需求的预测，而无需数据科学专业知识。 此外，营销从业者可以在Adobe Experience Cloud、Adobe Experience Platform和第三方应用程序中激活预测。

**主要功能**

| 功能 | 描述 |
|---|---|
| 客户人工智能 | 客户人工智能为营销人员提供了在个人级别生成客户预测的能力，并提供了解释。 在影响因素的帮助下，客户人工智能可以告诉您客户可能做什么以及原因。 此外，营销人员还可以从客户人工智能预测和洞察中受益，通过提供最合适的优惠和消息来个性化客户体验。 |
| 归因人工智能 | 归因人工智能是一种多渠道的算法归因服务，它计算客户交互对特定结果的影响和增量影响。 利用Attribution AI，营销人员可以通过了解客户旅程各个阶段每个客户互动的影响来衡量和优化营销和广告支出。 |

**已知问题**

* 当前没有已知问题。

有关智能服务及其要优惠的内容的详细信息，请参阅智能 [服务概述](../../intelligent-services/home.md)。

## 体验数据模型(XDM)系统 {#xdm}

标准化和互操作性是Experience Platform的主要概念。 Adobe推动的体验数据模型(XDM)旨在标准化客户体验数据并定义客户体验管理模式。

XDM是一个公开的规范，旨在提高数字体验的强大功能。 它为与Adobe Experience Platform上的服务通信的任何应用程序提供了通用结构和定义。 通过遵守XDM标准，所有客户体验数据都可以整合到以更快、更集成的方式提供洞察的共同表现形式中。 您可以从客户行动中获得宝贵的洞察，通过细分定义客户受众，并将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 自动替代显示信息 | 模式注册表自动应用在描述符中配置的自定义标题和描述 `alternateDisplayInfo` 值。 |
| 标量字段限制 | 模式注册表不允许在单个模式中超过6000个标量字段。 |
| 性能检查 | 模式登记处经过全面改革，以更好地执行和满足体验平台的需求。 |

**错误修复**

* 将XDM更新为XED，转换为XDM，支持标准XDM中嵌套URI字段的更简洁的XED格式。

**已知问题**

* 已知

## 数据管理 {#governance}

Adobe Experience Platform数据管理是用于管理客户数据并确保符合适用于数据使用的法规、限制和政策的一系列战略和技术。 它在Experience Platform的不同级别中起着关键作用，包括编目、数据谱系、数据使用标签、数据访问策略和营销操作的数据访问控制。

要开始进行数据管理，您必须全面了解适用于客户数据的法规、合同义务和公司政策。 从那里，可以通过应用适当的数据使用标签来对数据进行分类，并且可以通过定义数据使用策略来控制其使用。

DULE框架通过Experience Platform用户界面和DULE Policy Service API简化了数据分类和创建数据使用策略的过程。

**新增功能**

| 功能 | 描述 |
| -----------| ---------- |
| 在UI中管理数据使用策略 | 数据使用策略现在可以在Experience Platform UI的 _Policies_ （策略）工作区中管理。 有关详细 [信息，请参阅策略用户指南](../../data-governance/policies/user-guide.md) 。 |

**已知问题**

* 无.

有关详细信息，请参阅数 [据管理概述](../../data-governance/home.md)。


## 目标 {#destinations}

在 [Adobe实时客户数据平台中](../../rtcdp/overview.md)，目标是预建的与目标平台的集成，这些平台可以无缝地向这些合作伙伴激活数据。

**新目标**

Adobe实时CDP现在支持对超过50个Experience Cloud Launch扩展的数据激活，支持分析、个性化和其他使用案例。 有关详细信息，请参阅以下内容：

| 文档 | 描述 |
|--- | ---|
| [目标类型和类别](/help/rtcdp/destinations/destination-types.md) | 本文解释了Adobe实时CDP界面中的连接和扩展之间的区别，并建议何时使用这些目标。 |
| [Experience Platform Launch扩展](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | 本页介绍Launch扩展是什么，列表使用这些扩展的用例，以及Adobe实时CDP中每个Launch扩展的文档链接。 |

有关详细信息，请参阅目 [标概述](/help/rtcdp/destinations/destinations-overview.md)。

## 隐私服务 {#privacy}

新的法律和组织法规授予用户根据请求从数据存储中访问或删除其个人数据的权利。 Adobe Experience Platform Privacy Service提供RESTful API和用户界面，帮助您管理来自客户的这些数据请求。 通过隐私服务，您可以提交从Adobe Experience Cloud应用程序访问和删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| PDPA支持 | 现在，可以根据泰国的个人数据保护法(PDPA)创建和跟踪隐私请求。 在API中发出隐私请求时，数 `regulation` 组接受值“pdpa_tha”。 |
| 命名空间UI中的类型 | 您现在可以在隐私服务UI的Request Builder中指定不同的命名空间类型。 有关详细 [信息，请参阅](../../privacy-service/ui/user-guide.md) 《用户指南》。 |
| 旧端点弃用 | 旧API端点(`data/privacy/gdpr`)已弃用。 |

已知问题

* None

有关隐私服务的更多信息，请阅读隐私服务 [概述开始](../../privacy-service/home.md)。

## 来源 {#sources}

Adobe Experience Platform可以从外部源中摄取数据，同时允许您使用平台服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)获取数据。

Experience Platform提供RESTful API和交互式UI，使您能轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，为摄取运行设置时间，以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据库的API和UI支持 | Apache Spark（在HDInsights上）、Azure Synapse Analytics、Azure Table存储、Hive（在HDInsights上）和Phoenix的新源连接器。 |
| 对基于付款的应用程序的API和UI支持 | PayPal的新源连接器。 |
| 对基于协议的应用程序的API和UI支持 | 通用OData的新源连接器。 |

**已知问题**

* None

要进一步了解源，请参阅源 [概述](../../sources/home.md)。
