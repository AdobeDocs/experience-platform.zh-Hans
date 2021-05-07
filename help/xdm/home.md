---
keywords: Experience Platform；主题；热门主题；XDM;XDM系统；XDM个人用户档案;XDM体验事件；XDM体验事件；体验事件；字段组；字段组；字段组；体验事件;XDM体验事件;XDM体验事件；体验事件；体验事件；XDM Experienceevent；体验数据模型；体验数据模型；数据模型；模式注册；模式注册；模式库；事件库；模式库；模式；记录数据；时间序列；时间序列
solution: Experience Platform
title: XDM系统概述
topic-legacy: overview
description: 标准化和互操作性是Adobe Experience Platform的主要概念。 由Adobe驱动的体验数据模型(XDM)旨在实现客户体验数据标准化并定义客户体验管理模式。
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
translation-type: tm+mt
source-git-commit: b70e693b4ffeda561de4d4c8dd8fd1adeec489f7
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 1%

---

# XDM系统概述

>[!NOTE]
>
>术语“mixin”已更新为模式“字段组”以增进了解。 字段组是可重复使用的字段集，用于支持业务用例。 此更改现在反映在模式 Registry API、Adobe Experience Platform UI和所有平台文档中。

标准化和互操作性是Adobe Experience Platform的主要概念。 [!DNL Experience Data Model] (XDM)由Adobe驱动，旨在实现客户体验数据标准化并定义客户体验管理模式。

XDM是一个公开存档的规范，旨在提高数字体验的强大功能。 它为用于与[!DNL Platform]服务通信的任何应用程序提供了通用结构和定义。 通过遵守XDM标准，所有客户体验数据都可以整合到一种通用的表现形式中，以更快、更集成的方式提供洞察。 您可以从客户行动中获得宝贵的洞察，通过细分定义客户受众，并表达客户属性以实现个性化。

XDM是基本框架，它允许Adobe Experience Cloud在[!DNL Experience Platform]的支持下，在恰当的时间，在适当的渠道，向适当的人提供适当的信息。 构建[!DNL Experience Platform]的方法， XDM系统，可操作[!DNL Experience Data Model]模式，供[!DNL Platform]服务使用。

本文档概述了[!DNL Experience Platform]中XDM系统的作用。

## XDM模式

[!DNL Experience Platform] 会使用架构，以便以可重用的一致方式描述数据结构。通过在整个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。

在将数据引入[!DNL Platform]之前，必须构成一个模式来描述数据的结构，并对每个字段中可以包含的数据类型提供约束。 模式由基类和零个或多个模式字段组组成。

有关模式合成模型的详细信息（包括设计原则和最佳实践），请参阅[模式合成基础知识](schema/composition.md)。

### [!DNL Schema Registry] 和 [!DNL Schema Library]

**[!DNL Schema Registry]**&#x200B;提供一个用户界面和RESTful API，您可以从中视图和管理Adobe Experience Platform **[!DNL Schema Library]**&#x200B;中所有与模式相关的资源。 [!DNL Schema Library]包含由Adobe提供给您的行业标准资源，以及来自[!DNL Experience Platform]合作伙伴和您使用应用程序的供应商的资源。 模式注册表UI和API还可用于创建和管理组织特有的新模式和资源。

有关[!DNL Schema Registry]中主要操作的全面指南，请参阅[模式注册表开发人员指南](api/getting-started.md)。

## XDM系统{#data-behaviors}中的数据行为

用于[!DNL Experience Platform]的数据分为两种行为类型：

* **记录数据**:提供有关主题属性的信息。主题可以是组织或个人。
* **时间序列数据**:提供记录主体直接或间接采取操作时系统的快照。

所有XDM模式都描述了可以分类为记录或时间序列的数据。 模式的模式行为由的类定义，该类在首次创建模式时分配给。 XDM类描述模式必须包含的最小属性数，以表示特定数据行为。

尽管您能够在[!DNL Schema Registry]中定义自己的类，但建议您分别使用首选类&#x200B;**[!DNL XDM Individual Profile]**&#x200B;和&#x200B;**[!DNL XDM ExperienceEvent]**&#x200B;用于记录和时间序列数据。 下面将详细介绍这些类。

### [!DNL XDM Individual Profile] {#xdm-individual-profile}

[!DNL XDM Individual Profile] 是一个基于记录的类，它对已识别和部分已识别主题的属性形成单一表示。高度识别的用户档案可用于个人通信或有针对性的活动，并可包含详细的个人信息，例如姓名、性别、出生日期、地点和包括电话号码和电子邮件地址的联系信息。

识别较少的用户档案可能只包含浏览器cookie等匿名行为信号。 在这种情况下，使用稀疏用户档案数据来构建一个信息库，在该信息库中整理和存储匿名用户档案的兴趣和偏好。 随着主题注册通知、订阅、购买等，这些标识符可能会随着时间的推移变得更加详细。 用户档案属性的这种增加最终可能导致已识别的主题，并使目标参与度更高。

随着消费者用户档案的不断增长，它将成为一个可靠的存储库，其中包含个人的个人信息、身份信息、联系信息和通信首选项。

### [!DNL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent是一个基于时间序列的类，用于在发生事件(或一组事件)时捕获系统状态，包括所涉主题的时间点和身份。 经验事件是事实记录，因此它们是不可改变的，不经汇总或解释就能代表所发生的事情。 它们对于时域分析至关重要，因为它们可用于分析给定时间窗口中发生的更改，以及在多个时间窗口之间进行比较以跟踪趋势。

体验事件可以是显式的，也可以是隐式的。 显式事件是直接可观察的人类行为，在旅程中某一点发生。 隐式事件是在没有直接人类行为的情况下长大的事件，但仍与个人有关。 隐式事件的示例包括计划发送电子邮件新闻稿或达到特定阈值的电池电压。

虽然并非所有事件都可以轻松地跨所有数据源分类，但在可能的情况下将类似事件协调到类似类型以进行处理是非常有价值的。

![ExperienceEvent客户历程](images/overview/experience-event-journey.png)

## XDM模式和[!DNL Experience Platform]服务

[!DNL Experience Platform] 是与模式无关的，这意味着任何符合XDM标准的模式都可供服务 [!DNL Platform] 使用。以下详细介绍了不同[!DNL Platform]服务使用模式的方式。

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] 是资产及其相关 [!DNL Experience Platform] 模式的记录系统。[!DNL Catalog] 不是包含数据的实际文件或目录，而是包含这些文件和目录的元数据和说明。

[!DNL Catalog] 数据存储在高度粒 [!DNL Data Lake]度的数据存储中，它包含所有由管理的数 [!DNL Platform]据，而不管来源或文件格式。

要开始将数据引入[!DNL Experience Platform]，将使用[!DNL Catalog Service]创建数据集。 数据集引用描述要摄取的数据结构的XDM模式。 如果创建的数据集没有模式,[!DNL Experience Platform]将通过检查所摄取数据字段的类型和内容来导出“观察到的模式”。 然后，在[!DNL Catalog]中跟踪数据集，并与模式和观察到的模式一起存储在[!DNL Data Lake]中。

有关[!DNL Catalog]的详细信息，请参阅[目录服务概述](../catalog/home.md)。 有关Adobe Experience Platform数据摄取的详细信息，请参阅[数据摄取概述](../ingestion/home.md)。

### [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service]允许您使用标准SQL查询[!DNL Experience Platform]数据以支持许多不同的用例。

在合成模式并创建引用该模式的数据集后，数据会被摄取并存储在[!DNL Data Lake]中。 使用[!DNL Query Service]，您可以加入[!DNL Data Lake]中的任何数据集，并将查询结果捕获为新数据集，以用于报告、机器学习或引入[!DNL Real-time Customer Profile]。

要了解有关[!DNL Query Service]的详细信息，请参阅[查询服务简介](../query-service/home.md)。

### [!DNL Real-time Customer Profile]

实时客户用户档案为有针对性的个性化体验管理提供了集中化的消费者用户档案。 每个用户档案都包含跨所有系统聚合的事件，以及涉及与[!DNL Experience Platform]一起使用的任何系统中发生的个人的可操作时间戳帐户。

[!DNL Real-time Customer Profile] 根据或类读取模式格式 [!DNL XDM Individual Profile] 的 [!DNL XDM ExperienceEvent] 数据，并根据该数据响应查询。[!DNL Profile] 不支持基于其他类使用模式。

[!DNL Profile] 维护每个客户用户档案的实例，将数据合并在一起，为个人构成“单一真相来源”。此统一数据使用称为“合并视图”的数据表示。 合并视图将实现相同类的所有模式的字段聚合为一个模式。  使用UI或API编写模式时，您可以启用模式以与[!DNL Real-time Customer Profile]一起使用，并为其标记以包含在合并视图中。 加标签的模式随后将参与提供给[!DNL Profile]的模式定义。

当[!DNL XDM Individual Profile]和[!DNL XDM ExperienceEvent]数据被[!DNL Catalog]摄取和管理时，它触发[!DNL Real-time Customer Profile]以开始摄取已启用以供使用的数据。 所摄取的交互和细节越多，单个用户档案就越健壮。

[!DNL XDM Individual Profile] 数据有助于在任何渠道或Adobe解决方案集成中提供信息和支持操作，如果与丰富的行为和交互数据历史相配，这些数据将用于推动机器学习。[!DNL Real-time Customer Profile] API还可用于丰富第三方解决方案、CRM和专有解决方案的功能。

有关详细信息，请参阅[实时客户用户档案概述](../profile/home.md)。

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace]使用机器学习和人工智能从[!DNL Experience Platform]中存储的数据获得洞察。 [!DNL Data Science Workspace] 允许数据科学家根据XDM个人和有关 [!DNL Profile] 客 [!DNL XDM ExperienceEvent] 户及其活动的数据来构建方法，从而促进购买倾向等预测以及个人可能喜欢和使用的推荐优惠。

借助[!DNL Data Science Workspace]，数据科学家可以轻松创建由机器学习提供支持的智能服务API。 这些服务可与其他Adobe解决方案(包括Adobe Target和Adobe Analytics Cloud)配合使用，帮助您实现个性化、有针对性的数字体验自动化。

有关使用[!DNL Experience Platform]数据来增强洞察力的更多信息，请参阅[数据科学工作区概述](../data-science-workspace/home.md)。

## 后续步骤和其他资源

现在，您已经更好地了解了[!DNL Experience Platform]中模式的角色，因此，您已准备好构成自己的开始。 要继续补充您的学习，请阅读建议的文档并观看以下视频，以开始。

要了解要与[!DNL Experience Platform]一起使用的模式合成的设计原则和最佳实践，请首先阅读模式合成的[基础知识](schema/composition.md)。 有关如何创建模式的分步说明，请参阅有关使用API](tutorials/create-schema-api.md)或使用用户界面](tutorials/create-schema-ui.md)创建模式[的教程。[

要加深您对[!DNL Experience Platform]中[!DNL XDM System]的理解，请观看以下视频：

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
