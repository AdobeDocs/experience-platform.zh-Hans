---
keywords: Experience Platform；主页；热门主题；XDM;XDM系统；XDM个人配置文件；XDM ExperienceEvent;XDM体验事件；体验事件；字段组；字段组；字段组；体验事件；XDM体验事件；体验事件；体验事件；XDM体验事件；体验事件；XDM体验事件；体验数据模型；体验数据模型；数据模型；数据模型；数据模型；数据库模式；架构；架构；注册表；架构；记录数据；时间序列；时间序列
solution: Experience Platform
title: XDM系统概述
topic-legacy: overview
description: 标准化和互操作性是Adobe Experience Platform背后的关键概念。 由Adobe驱动的体验数据模型(XDM)旨在标准化客户体验数据并定义客户体验管理架构。
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: a95e5cf02e993d6c761abd74c98c0967a89eb678
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 2%

---

# XDM系统概述

标准化和互操作性是Adobe Experience Platform背后的关键概念。 [!DNL Experience Data Model] (XDM)在Adobe的驱动下，努力标准化客户体验数据并定义客户体验管理架构。

XDM是一项公开记录的规范，旨在提高数字体验的强大功能。 它提供了通用结构和定义，允许任何应用程序用于与Platform服务通信。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以便以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及为个性化目的表达客户属性。

XDM是基础框架，它允许Adobe Experience Cloud在Experience Platform的支持下，在适当的时间，通过适当的渠道向适当的人员提供适当的信息。 构建Experience Platform的方法（XDM系统）可操作 [!DNL Experience Data Model] 平台服务使用的模式。

本文档概述了XDM系统在Experience Platform中的角色。

## XDM模式

Experience Platform 会使用架构，以便以可重用的一致方式描述数据结构。通过在整个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。

在将数据摄取到平台中之前，必须构建一个架构来描述数据的结构，并对每个字段中可包含的数据类型提供约束。 架构由基类和零个或多个架构字段组组成。

有关架构组合模型（包括设计原则和最佳实践）的更多信息，请参阅 [架构组合基础知识](schema/composition.md).

### 标准XDM组件

XDM提供了标准字段组和数据类型的强大集合，旨在捕获不同行业中的常见概念和用例。 Experience Platform允许您按行业筛选这些组件，使您能够快速、自信地构建最能支持您特定业务需求的模式。

在Experience PlatformUI中构建架构时，会使用热门程度量度显示列出的字段组。 此量度取决于其他Platform用户在其架构中使用字段组的频率。 数字越高，字段组就越受欢迎。 默认情况下，结果会从最受欢迎到最不受欢迎，从而使您能够随时了解行业中的数据建模趋势。

![字段组热门程度](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform提供了用户界面和RESTful API，您可以从中查看和管理Experience Platform中所有与架构相关的资源 **[!DNL Schema Library]**. 的 [!DNL Schema Library] 包含按Adobe为您提供的标准XDM组件，以及来自Experience Platform合作伙伴和您使用应用程序的供应商的资源。

使用 [!DNL Schema Registry API] 或 [!UICONTROL 模式] 工作区中，您还可以创建和管理组织特有的新模式和资源。

有关如何在平台中管理架构并与其进行交互的更多信息，请参阅以下文档：

* [XDM UI指南](./ui/overview.md)
* [架构注册API指南](./api/overview.md)

## XDM系统中的数据行为 {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="数据行为"
>abstract="用于Experience Platform的数据分为三种行为类型：记录、时间系列和临时。 记录架构提供有关主体属性的信息，而时序架构在执行操作时捕获系统的快照。 临时架构捕获字段是命名空间，仅供单个数据集使用。 有关Platform中数据行为的更多信息，请参阅此文档。"

用于Experience Platform的数据分为三种行为类型：

* **记录**:提供有关主题属性的信息。 主题可以是组织或个人。
* **时间系列**:提供记录主体直接或间接执行某项操作时系统的快照。
* **临时**:捕获仅由单个数据集使用的与名称命名的字段。 临时架构用于各种Experience Platform数据摄取工作流，包括摄取CSV文件和创建特定类型的源连接。

所有XDM架构都描述了可以分类为记录或时间序列的数据。 架构的数据行为由架构的类定义，该类在首次创建架构时分配给架构。 XDM类描述架构必须包含的最小属性数，以表示特定数据行为。

尽管您能够在 [!DNL Schema Registry]，建议您使用标准类 **[!UICONTROL XDM个人配置文件]** 和 **[!UICONTROL XDM ExperienceEvent]** ，用于记录数据和时序数据。 下文将详细介绍这些类。

>[!NOTE]
>
>没有基于临时行为的标准类。 临时架构由利用这些架构的平台进程自动生成，但也可以 [使用架构注册表API手动创建](./tutorials/ad-hoc.md).

### [!UICONTROL XDM个人配置文件] {#xdm-individual-profile}

[!UICONTROL XDM个人配置文件] 是基于记录的类，它对已识别和部分已识别主题的属性形成单一表示。 高度识别的用户档案可用于个人通信或定向活动，并且可以包含详细的个人信息，例如姓名、性别、出生日期、地点和联系信息，包括电话号码和电子邮件地址。

未识别的用户档案可能只包含匿名行为信号，如浏览器Cookie。 在这种情况下，使用稀疏的用户档案数据来构建一个信息库，在该信息库中整理并存储匿名用户档案的兴趣和偏好。 随着主题注册通知、订阅、购买等内容，这些标识符可能会随着时间的推移而变得更加详细。 用户档案属性的这种增加最终可能会生成已识别的主题，并允许更高程度的定向参与。

随着用户档案的不断增长，它将成为一个可靠的存储库，其中包含个人的个人信息、身份信息、联系方式和通信偏好。

请参阅 [[!UICONTROL XDM个人配置文件] 参考指南](./classes/individual-profile.md) 有关类提供的字段的结构和用例的详细信息。

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent是一个基于时间序列的类，用于在发生事件（或事件集）时捕获系统状态，包括所涉及主题的时间点和身份。 体验事件是关于在某个时间点发生的事件的不可更改的事实记录，它表示发生的事件，而不进行聚合或解释。 它们对于时域分析至关重要，因为它们可用于分析在给定时间范围内发生的更改，并在多个时间范围之间进行比较以跟踪趋势。

体验事件可以是显式事件，也可以是隐式事件。 显式事件是在旅程中某个点期间发生的可直接观察到的人类行为。 隐含事件是指在没有直接人为行为的情况下引发的事件，但仍与个人有关。 隐式事件的示例包括计划发送电子邮件快讯或达到特定阈值的电池电压。

虽然并非所有事件都可以轻松地跨所有数据源进行分类，但在可能的情况下将类似事件协调为类似类型以便进行处理是非常有价值的。

![ExperienceEvent客户历程](images/overview/experience-event-journey.png)

请参阅 [[!UICONTROL XDM ExperienceEvent] 参考指南](./classes/experienceevent.md) 有关类提供的字段的结构和用例的详细信息。

## XDM模式和Experience Platform服务

Experience Platform与模式无关，这意味着任何符合XDM标准的模式都可供Platform服务使用。 下文将详细介绍不同Platform服务使用模式的方式。

### 目录服务、数据摄取和数据湖

目录服务是Experience Platform资产及其相关架构的记录系统。 目录不包含实际的数据文件或目录，而是包含这些文件和目录的元数据和描述。

目录数据存储在数据湖中，这是一个高度精细的数据存储，包含由平台管理的所有数据，而不考虑原始数据或文件格式。

要开始将数据摄取到Experience Platform中，您可以使用目录服务创建数据集。 数据集会引用一个XDM架构，用于描述要摄取的数据的结构。 如果创建的数据集没有架构，则Experience Platform会通过检查摄取的数据字段的类型和内容来导出“观察到的架构”。 然后，数据集会在目录中进行跟踪，并与其所基于的架构和观察的架构一起存储在数据湖中。

有关目录的更多信息，请参阅 [目录服务概述](../catalog/home.md). 有关Adobe Experience Platform数据摄取的更多信息，请参阅 [数据摄取概述](../ingestion/home.md).

### 查询服务

Adobe Experience Platform查询服务允许您使用标准SQL查询Experience Platform数据，以支持许多不同的用例。

构建架构并创建引用该架构的数据集后，将会摄取数据并将其存储在数据湖中。 使用查询服务，您可以加入数据湖中的任何数据集，并作为新数据集捕获查询结果，以用于报表、机器学习或将查询结果摄取到实时客户配置文件中。

请参阅 [查询服务概述](../query-service/home.md) 以了解有关该服务的详细信息。

### 实时客户个人资料

Real-time Customer Profile提供了集中式消费者用户档案，以进行有针对性的个性化体验管理。 每个用户档案都包含在所有系统中汇总的数据，以及涉及您与Experience Platform一起使用的任何系统中发生的个人事件的带有时间戳的可操作帐户。

实时客户配置文件会根据 [!UICONTROL XDM个人配置文件] 和 [!UICONTROL XDM ExperienceEvent] 类，并基于该数据响应查询。 配置文件不支持基于其他类使用架构。

系统维护每个客户用户档案的一个实例，将数据合并在一起，为个人形成“单一真相来源”。 此统一数据使用称为“并集模式”（有时称为“并集视图”）来表示。 并集架构将实现相同类的所有架构的字段聚合到单个架构中。  使用UI或API合成架构时，您可以启用该架构以与实时客户资料一起使用，并将其标记以包含在合并中。 然后，标记的架构将参与馈送到用户档案的架构定义。

作为 [!UICONTROL XDM个人配置文件] 和 [!UICONTROL XDM ExperienceEvent] 数据会摄取到数据湖中，实时客户资料会摄取任何已启用供其使用的数据。 摄取的交互和详细信息越多，个人用户档案就越可靠。

[!UICONTROL XDM个人配置文件] 数据有助于通过任何渠道或Adobe产品集成来提供相关信息并授权相关操作。 当与丰富的行为和交互数据历史配对时，此数据可用于促进机器学习。 实时客户资料API还可用于丰富第三方解决方案、CRM和专有解决方案的功能。

请参阅 [实时客户资料概述](../profile/home.md) 以了解更多信息。

### 数据科学工作区

Adobe Experience Platform Data Science Workspace使用机器学习和人工智能从Experience Platform中存储的数据中获得洞察。 数据科学工作区允许数据科学家根据 [!UICONTROL XDM个人配置文件] 和 [!UICONTROL XDM ExperienceEvent] 客户及其活动的相关数据，有助于进行预测，如购买倾向和推荐的个人可能喜欢和使用的选件。

借助数据科学工作区，数据科学家可以轻松创建由机器学习提供支持的智能服务API。 这些服务可与其他Adobe解决方案(包括Adobe Target和Adobe Analytics Cloud)配合使用，以帮助您自动化个性化、有针对性的数字体验。

有关使用Experience Platform数据增强分析功能的更多信息，请参阅 [数据科学工作区概述](../data-science-workspace/home.md).

## 后续步骤和其他资源

既然您在整个Experience Platform中都能更好地了解模式的角色，那么您就可以开始编写自己的模式了。

要了解与Experience Platform一起使用的构建架构的设计原则和最佳实践，请首先阅读 [架构组合基础知识](schema/composition.md). 有关如何创建模式的分步说明，请参阅有关创建模式的教程 [使用API](tutorials/create-schema-api.md) 或 [使用用户界面](tutorials/create-schema-ui.md).

以加深您对 [!DNL XDM System] 在Experience Platform中，观看以下视频：

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
