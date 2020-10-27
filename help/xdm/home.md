---
keywords: Experience Platform;home;popular topics;XDM;XDM system;XDM individual profile;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience event;Mixins;mixins;mixin;Mixin;Experience event;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM Experienceevenet;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema library;Schema Library;schema;record data;time series;time-series
solution: Experience Platform
title: 体验数据模型(XDM)系统
topic: overview
description: '标准化和互操作性是Adobe Experience Platform背后的关键概念。 体验Adobe模型(XDM)由客户驱动，旨在实现客户体验数据标准化并为客户体验管理定义模式。 '
translation-type: tm+mt
source-git-commit: 1c00456ee06c1fc09c8e4ce070c90255f51811e1
workflow-type: tm+mt
source-wordcount: '1586'
ht-degree: 2%

---


# XDM系统概述

标准化和互操作性是Adobe Experience Platform背后的关键概念。 [!DNL Experience Data Model] (XDM)由Adobe驱动，旨在实现客户体验数据标准化并定义客户体验管理模式。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为用于与服务通信的任何应用程序提供了通用结构和 [!DNL Platform] 定义。 通过遵守XDM标准，所有客户体验数据都可以整合到一种通用的表现形式中，以更快、更集成的方式提供洞察。 您可以从客户行动中获得宝贵的洞察，通过细分定义客户受众，并表达客户属性以实现个性化。

XDM是一个基本框架，它允许Adobe Experience Cloud在 [!DNL Experience Platform]其支持下，在正确的渠道、恰当的时机、向正确的人提供正确的信息。 构建XDM系 [!DNL Experience Platform] 统的方法可操作模式, [!DNL Experience Data Model] 供服务使 [!DNL Platform] 用。

本文档概述了XDM系统在中的作用 [!DNL Experience Platform]。

## XDM模式

[!DNL Experience Platform] 会使用架构，以便以可重用的一致方式描述数据结构。通过在整个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。

在将数据引入 [!DNL Platform]之前，必须构建模式以描述数据结构，并对每个字段中可以包含的数据类型提供约束。 模式由基类和零个或多个混音组成。

有关模式合成模型的更多信息（包括设计原则和最佳实践），请参 [阅模式合成基础知识](schema/composition.md)。

### [!DNL Schema Registry] 和 [!DNL Schema Library]

它提 **[!DNL Schema Registry]** 供了一个用户界面和RESTful API，您可以从中视图和管理Adobe Experience Platform的所有与模式相关的资源 **[!DNL Schema Library]**。 它包 [!DNL Schema Library] 含由Adobe提供给您的行业标准资源，以及来自您使用应用程序的合 [!DNL Experience Platform] 作伙伴和供应商的资源。 模式注册表UI和API还可用于创建和管理您的组织特有的新模式和资源。

有关中提供的主要操作的全面指南， [!DNL Schema Registry]请参阅模式注 [册表开发人员指南](api/getting-started.md)。

## XDM系统中的数据行为 {#data-behaviors}

计划用于的数据 [!DNL Experience Platform] 分为两种行为类型：

* **记录数据**:提供有关主题属性的信息。 主题可以是组织或个人。
* **时间序列数据**:提供记录主体直接或间接采取操作时系统的快照。

所有XDM模式都描述可以分类为记录或时间序列的数据。 模式的数据行为由模式的类定义，该类在模式首次创建时被分配给。 XDM类描述模式必须包含的最小属性数，以表示特定数据行为。

尽管您可以在中定义自己的类， [!DNL Schema Registry]但建议您分别使用首选类 **[!DNL XDM Individual Profile]****[!DNL XDM ExperienceEvent]** 和记录和时间序列数据。 下文将详细介绍这些类。

### [!DNL XDM Individual Profile] {#xdm-individual-profile}

[!DNL XDM Individual Profile] 是基于记录的类，它对已识别和部分已识别主题的属性形成单一表示。 高度识别的用户档案可用于个人通信或定向活动，并可包含详细的个人信息，如姓名、性别、出生日期、地点和联系信息，包括电话号码和电子邮件地址。

识别较少的用户档案可能只包含匿名行为信号，如浏览器cookie。 在这种情况下，稀疏用户档案数据被用于构建一个信息库，在该信息库中整理和存储匿名用户档案的兴趣和偏好。 随着主体注册通知、订阅、购买等，这些标识符可能会随着时间的推移变得更加详细。 用户档案属性的这种增加最终可能导致确定的主题，并使目标参与度更高。

随着消费者用户档案的不断增长，它将成为一个可靠的个人信息、身份信息、联系信息和通信首选项存储库。

### [!DNL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent是一个基于时间序列的类，用于在发生事件(或事件集)时捕获系统状态，包括时间点和所涉及主题的身份。 体验事件是事实记录，因此它们是不可改变的，代表所发生的事情，而不经过聚合或解释。 它们对于时域分析至关重要，因为它们可用于分析给定时间窗口中发生的更改，以及在多个时间窗口之间进行比较以跟踪趋势。

体验事件可以是显式的或隐式的。 显式事件是在旅程中某一点发生的直接可观察的人类行为。 内隐事件是在没有直接人类行为的情况下长大的事件，但仍与个人有关。 隐式事件的示例包括计划发送电子邮件时事通讯或达到特定阈值的电池电压。

虽然并非所有事件都可以轻松地跨所有数据源分类，但在可能的情况下将类似事件协调为类似类型以进行处理是非常有价值的。

![体验活动客户旅程](images/overview/experience-event-journey.png)

## XDM模式和服 [!DNL Experience Platform] 务

[!DNL Experience Platform] 与模式无关，这意味着任何符合XDM标准的模式都可供服务 [!DNL Platform] 使用。 以下更详细介绍了不 [!DNL Platform] 同服务使用模式的方式。

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] 是资产及其相关模式 [!DNL Experience Platform] 的记录系统。 [!DNL Catalog] 不是包含数据的实际文件或目录，而是包含这些文件和目录的元数据和说明。

[!DNL Catalog] 数据存储在一个高度细 [!DNL Data Lake]粒度的数据存储中，它包含所有由管理的数 [!DNL Platform]据，而不管来源或文件格式。

要开始将数据引入 [!DNL Experience Platform]数据中，将使用创建数据集 [!DNL Catalog Service]。 数据集引用描述要摄取的数据结构的XDM模式。 如果创建的数据集没有模式, [!DNL Experience Platform] 将通过检查所摄取数据字段的类型和内容来导出“观察到的模式”。 然后，在模式和观 [!DNL Catalog] 察模式中跟踪数据集，并 [!DNL Data Lake] 将其存储在数据集所基于的中。

有关的详细信 [!DNL Catalog]息，请参阅 [目录服务概述](../catalog/home.md)。 有关Adobe Experience Platform数据摄取的详细信息，请参 [阅数据摄取概述](../ingestion/home.md)。

### [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] 允许您使用标准SQL查询数据以支持 [!DNL Experience Platform] 许多不同的用例。

在构建模式并创建引用该模式的数据集后，数据被摄取并存储在中 [!DNL Data Lake]。 使 [!DNL Query Service]用，您可以加入查询中的任何数据集 [!DNL Data Lake] 并将报告结果捕获为新数据集，以用于、机器学习或引入 [!DNL Real-time Customer Profile]。

要了解有关的更 [!DNL Query Service]多信息，请参阅 [查询服务简介](../query-service/home.md)。

### [!DNL Real-time Customer Profile]

实时客户用户档案为有针对性的个性化体验管理提供了集中化的消费者用户档案。 每个用户档案都包含跨所有系统聚集的数据，以及涉及您所使用的任何系统中发生的个人的事件的可操作时间戳帐户 [!DNL Experience Platform]。

[!DNL Real-time Customer Profile] 根据模式或类消耗格 [!DNL XDM Individual Profile] 式的 [!DNL XDM ExperienceEvent] 数据，并根据该数据响应查询。 [!DNL Profile] 不支持使用基于其他类的模式。

[!DNL Profile] 维护每个客户用户档案的一个实例，将数据合并在一起，为个人形成“单一的真相来源”。 此统一数据使用称为“合并视图”的数据表示。 合并视图将实现同一类的所有模式的字段聚合为单个模式。  使用UI或API编写模式时，您可以启用模式以与其一起使用，并 [!DNL Real-time Customer Profile] 将其标记以包含在合并视图中。 加标签的模式随后将参与要输入的模式定义 [!DNL Profile]。

由 [!DNL XDM Individual Profile] 于 [!DNL XDM ExperienceEvent] 数据是摄取和管理的，它触发 [!DNL Catalog]器开始 [!DNL Real-time Customer Profile] 摄取已启用其使用的数据。 所摄取的交互和细节越多，个体用户档案就越健壮。

[!DNL XDM Individual Profile] 数据有助于在任何渠道或Adobe解决方案集成中提供信息并赋予其行动能力，如果与行为和交互数据的丰富历史相配，这些数据将用于推动机器学习。 该 [!DNL Real-time Customer Profile] API还可用于丰富第三方解决方案、CRM和专有解决方案的功能。

有关更 [多信息，请参阅实时客户用户档案](../profile/home.md) 概述。

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] 使用机器学习和人工智能从存储在其中的数据获得洞 [!DNL Experience Platform]察。 [!DNL Data Science Workspace] 使数据科学家能够根据XDM个人 [!DNL Profile] 和客 [!DNL XDM ExperienceEvent] 户及其活动的数据来构建食谱，从而促进购买倾向和个人可能喜欢和使用的推荐优惠等预测。

借助 [!DNL Data Science Workspace]数据科学家可以轻松创建由机器学习提供支持的智能服务API。 这些服务与包括Adobe Target和Adobe Analytics Cloud在内的其他Adobe解决方案配合使用，帮助您实现个性化、有针对性的数字体验自动化。

有关使用数据来提 [!DNL Experience Platform] 高洞察力的更多信息，请参 [阅数据科学工作区概述](../data-science-workspace/home.md)。

## 后续步骤和其他资源

现在，您更好地了解模式在整个过程中的 [!DNL Experience Platform]角色，因此，您已准备好编写自己的开始。 要继续补充您的学习，请阅读建议的文档并观看以下视频，以开始。

要了解用于编写模式的设计原则和最佳实践， [!DNL Experience Platform]请首先阅读模式排 [版的基础知识](schema/composition.md)。 有关如何创建模式的分步说明，请参阅有关使用API或使用用 [户界面创](tutorials/create-schema-api.md)[建模式的教程](tutorials/create-schema-ui.md)。

要加深您对中的 [!DNL XDM System] 了 [!DNL Experience Platform]解，请观看以下视频：

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

