---
keywords: Experience Platform；主题；热门主题；XDM;XDM系统；XDM个人用户档案;XDM体验事件；XDM体验事件；体验事件；体验模式；混合；混合；体验事件;XDM体验事件;XDM体验事件；体验事件；体验事件；XDM体验数据模型；体验数据模型；体验数据模型；数据模型；模式注册；模式注册；模式库；模式库；库；库；；记录数据；时间序列；时间序列
solution: Experience Platform
title: XDM系统概述
topic: overview
description: '标准化和互操作性是Adobe Experience Platform背后的关键概念。 体验Adobe模型(XDM)由客户驱动，旨在实现客户体验数据标准化并为客户体验管理定义模式。 '
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 2%

---


# XDM系统概述

标准化和互操作性是Adobe Experience Platform背后的关键概念。 [!DNL Experience Data Model] (XDM)由Adobe驱动，旨在实现客户体验数据标准化并定义客户体验管理模式。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为用于与[!DNL Platform]服务通信的任何应用程序提供了通用结构和定义。 通过遵守XDM标准，所有客户体验数据都可以整合到一种通用的表现形式中，以更快、更集成的方式提供洞察。 您可以从客户行动中获得宝贵的洞察，通过细分定义客户受众，并表达客户属性以实现个性化。

XDM是一个基本框架，它允许Adobe Experience Cloud在[!DNL Experience Platform]的支持下，在正确的渠道，在正确的时刻，向正确的人提供正确的信息。 构建[!DNL Experience Platform]的方法， XDM系统，操作[!DNL Experience Data Model]模式，供[!DNL Platform]服务使用。

此文档概述了[!DNL Experience Platform]中XDM系统的角色。

## XDM模式

[!DNL Experience Platform] 会使用架构，以便以可重用的一致方式描述数据结构。通过在整个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。

在将数据引入[!DNL Platform]之前，必须构成一个模式来描述数据的结构，并对每个字段中可以包含的数据类型提供约束。 模式由基类和零个或多个混音组成。

有关模式合成模型的详细信息（包括设计原则和最佳实践），请参阅[模式合成基础知识](schema/composition.md)。

### [!DNL Schema Registry] 和 [!DNL Schema Library]

**[!DNL Schema Registry]**&#x200B;提供一个用户界面和RESTful API，您可以从中视图和管理Adobe Experience Platform **[!DNL Schema Library]**&#x200B;中所有与模式相关的资源。 [!DNL Schema Library]包含由Adobe提供给您的行业标准资源，以及来自[!DNL Experience Platform]合作伙伴和您使用其应用程序的供应商的资源。 模式注册表UI和API还可用于创建和管理您的组织特有的新模式和资源。

有关[!DNL Schema Registry]中主要操作的全面指南，请参阅[模式注册表开发人员指南](api/getting-started.md)。

## XDM系统{#data-behaviors}中的数据行为

用于[!DNL Experience Platform]的数据分为两种行为类型：

* **记录数据**:提供有关主题属性的信息。主题可以是组织或个人。
* **时间序列数据**:提供记录主体直接或间接采取操作时系统的快照。

所有XDM模式都描述可以分类为记录或时间序列的数据。 模式的数据行为由模式的类定义，该类在模式首次创建时被分配给。 XDM类描述模式必须包含的最小属性数，以表示特定数据行为。

尽管您能够在[!DNL Schema Registry]中定义自己的类，但建议您分别使用首选类&#x200B;**[!DNL XDM Individual Profile]**&#x200B;和&#x200B;**[!DNL XDM ExperienceEvent]**&#x200B;来记录和时间序列数据。 下文将详细介绍这些类。

### [!DNL XDM Individual Profile] {#xdm-individual-profile}

[!DNL XDM Individual Profile] 是基于记录的类，它对已识别和部分已识别主题的属性形成单一表示。高度识别的用户档案可用于个人通信或定向活动，并可包含详细的个人信息，如姓名、性别、出生日期、地点和联系信息，包括电话号码和电子邮件地址。

识别较少的用户档案可能只包含匿名行为信号，如浏览器cookie。 在这种情况下，稀疏用户档案数据被用于构建一个信息库，在该信息库中整理和存储匿名用户档案的兴趣和偏好。 随着主体注册通知、订阅、购买等，这些标识符可能会随着时间的推移变得更加详细。 用户档案属性的这种增加最终可能导致确定的主题，并使目标参与度更高。

随着消费者用户档案的不断增长，它将成为一个可靠的个人信息、身份信息、联系信息和通信首选项存储库。

### [!DNL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent是一个基于时间序列的类，用于在发生事件(或事件集)时捕获系统状态，包括时间点和所涉及主题的身份。 体验事件是事实记录，因此它们是不可改变的，代表所发生的事情，而不经过聚合或解释。 它们对于时域分析至关重要，因为它们可用于分析给定时间窗口中发生的更改，以及在多个时间窗口之间进行比较以跟踪趋势。

体验事件可以是显式的或隐式的。 显式事件是在旅程中某一点发生的直接可观察的人类行为。 内隐事件是在没有直接人类行为的情况下长大的事件，但仍与个人有关。 隐式事件的示例包括计划发送电子邮件时事通讯或达到特定阈值的电池电压。

虽然并非所有事件都可以轻松地跨所有数据源分类，但在可能的情况下将类似事件协调为类似类型以进行处理是非常有价值的。

![体验活动客户历程](images/overview/experience-event-journey.png)

## XDM模式和[!DNL Experience Platform]服务

[!DNL Experience Platform] 与模式无关，这意味着任何符合XDM标准的模式都可供服务 [!DNL Platform] 使用。以下详细介绍了不同[!DNL Platform]服务使用模式的方式。

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] 是资产及其相关 [!DNL Experience Platform] 模式的记录系统。[!DNL Catalog] 不是包含数据的实际文件或目录，而是包含这些文件和目录的元数据和说明。

[!DNL Catalog] 数据存储在一个高度细 [!DNL Data Lake]粒度的数据存储中，它包含所有由管理的数 [!DNL Platform]据，而不管来源或文件格式。

要开始将数据引入[!DNL Experience Platform]，将使用[!DNL Catalog Service]创建数据集。 数据集引用描述要摄取的数据结构的XDM模式。 如果创建的数据集没有模式,[!DNL Experience Platform]将通过检查所摄取数据字段的类型和内容来导出“观察到的模式”。 然后，在[!DNL Catalog]中跟踪数据集，并将数据集与模式和观察模式一起存储在[!DNL Data Lake]中。

有关[!DNL Catalog]的详细信息，请参阅[目录服务概述](../catalog/home.md)。 有关Adobe Experience Platform数据摄取的详细信息，请参阅[数据摄取概述](../ingestion/home.md)。

### [!DNL Query Service]

Adobe Experience Platform[!DNL Query Service]允许您使用标准SQL查询[!DNL Experience Platform]数据以支持许多不同的用例。

在构建模式并创建引用该模式的数据集后，数据会被摄取并存储在[!DNL Data Lake]中。 使用[!DNL Query Service]，您可以加入[!DNL Data Lake]中的任何数据集并将查询结果捕获为新数据集，用于报告、机器学习或引入[!DNL Real-time Customer Profile]。

要进一步了解[!DNL Query Service]，请参阅[查询服务简介](../query-service/home.md)。

### [!DNL Real-time Customer Profile]

实时客户用户档案为有针对性的个性化体验管理提供了集中化的消费者用户档案。 每个用户档案都包含跨所有系统聚集的数据，以及涉及您与[!DNL Experience Platform]一起使用的任何系统中发生的个人的事件的可操作时间戳帐户。

[!DNL Real-time Customer Profile] 根据或类消耗模式格式 [!DNL XDM Individual Profile] 化 [!DNL XDM ExperienceEvent] 的数据，并基于该数据响应查询。[!DNL Profile] 不支持使用基于其他类的模式。

[!DNL Profile] 维护每个客户用户档案的一个实例，将数据合并在一起，为个人形成“单一的真相来源”。此统一数据使用称为“合并视图”的数据表示。 合并视图将实现同一类的所有模式的字段聚合为单个模式。  使用UI或API编写模式时，可以启用模式以与[!DNL Real-time Customer Profile]一起使用，并将其标记以包含在合并视图中。 标记模式随后将参与输入到[!DNL Profile]的模式定义。

由于[!DNL XDM Individual Profile]和[!DNL XDM ExperienceEvent]数据由[!DNL Catalog]摄取和管理，它触发[!DNL Real-time Customer Profile]以开始摄取已启用其使用的数据。 所摄取的交互和细节越多，个体用户档案就越健壮。

[!DNL XDM Individual Profile] 数据有助于在任何渠道或Adobe解决方案集成中提供信息并赋予其行动能力，如果与行为和交互数据的丰富历史相配，这些数据将用于推动机器学习。[!DNL Real-time Customer Profile] API还可用于丰富第三方解决方案、CRM和专有解决方案的功能。

有关详细信息，请参阅[实时客户用户档案概述](../profile/home.md)。

### [!DNL Data Science Workspace]

Adobe Experience Platform[!DNL Data Science Workspace]使用机器学习和人工智能从存储在[!DNL Experience Platform]中的数据获得洞察。 [!DNL Data Science Workspace] 使数据科学家能够根据XDM个人和 [!DNL Profile] 客 [!DNL XDM ExperienceEvent] 户及其活动的相关数据来构建食谱，从而促进购买倾向和推荐优惠等预测，这些预测是个人可能欣赏和使用的。

借助[!DNL Data Science Workspace]，数据科学家可以轻松创建由机器学习提供支持的智能服务API。 这些服务与包括Adobe Target和Adobe Analytics Cloud在内的其他Adobe解决方案配合使用，帮助您实现个性化、有针对性的数字体验自动化。

有关使用[!DNL Experience Platform]数据来提供洞察的更多信息，请参阅[数据科学工作区概述](../data-science-workspace/home.md)。

## 后续步骤和其他资源

现在，您可以更好地了解[!DNL Experience Platform]中模式的角色，随时可以编写自己的开始。 要继续补充您的学习，请阅读建议的文档并观看以下视频，以开始。

要了解构建要与[!DNL Experience Platform]一起使用的模式的设计原则和最佳实践，请首先阅读[模式构建基础知识](schema/composition.md)。 有关如何创建模式的分步说明，请参阅有关使用API](tutorials/create-schema-api.md)或使用用户界面](tutorials/create-schema-ui.md)创建模式[的教程。[

要加深您对[!DNL Experience Platform]中[!DNL XDM System]的理解，请观看以下视频：

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

