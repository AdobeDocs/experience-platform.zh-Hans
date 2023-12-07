---
keywords: Experience Platform；主页；热门主题；XDM；XDM系统；XDM个人资料；XDM ExperienceEvent；XDM ExperienceEvent；XDM体验事件；体验事件；字段组；字段组；字段组；体验事件；XDM ExperienceEvent；XDM Experienceevent；XDM Experienceevent；体验数据模型；体验数据模型；数据模型；架构注册表；架构库；架构库；记录时间序列
solution: Experience Platform
title: XDM系统概述
description: 标准化和互操作性是Adobe Experience Platform背后的关键概念。 体验数据模型(XDM)由Adobe驱动，它致力于标准化客户体验数据并定义用于客户体验管理的架构。
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 4%

---

# XDM系统概述

标准化和互操作性是Adobe Experience Platform背后的关键概念。 [!DNL Experience Data Model] (XDM)由Adobe驱动，致力于标准化客户体验数据并定义用于客户体验管理的架构。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它提供了通用结构和定义，允许任何应用程序使用与Platform服务进行通信。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并表达客户属性以进行个性化。

XDM是一个基础框架，它允许Adobe Experience Cloud由Experience Platform提供支持，在正确的时间通过正确的渠道向正确的人员传递正确的信息。 XDMExperience Platform的构建方法可操作 [!DNL Experience Data Model] 供Platform服务使用的架构。

本文档概述了XDM System在Experience Platform中的作用。

## XDM架构

Experience Platform 会使用架构，以便以可重用的一致方式描述数据结构。通过在系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。

在将数据引入Platform之前，必须组合模式以描述数据的结构并对每个字段中可以包含的数据类型提供约束。 架构由一个基类以及零个或多个架构字段组组成。

有关架构组合模型的更多信息，包括设计原则和最佳实践，请参阅 [模式组合基础](schema/composition.md).

### 标准XDM组件

XDM提供了标准字段组和数据类型的强大集合，旨在捕获不同行业的通用概念和使用案例。 Experience Platform允许您按行业筛选这些组件，使您能够快速自信地构建最符合您特定业务需求的架构。

在Experience PlatformUI中构建架构时，列出的字段组将显示热门程度量度。 此量度由其他Platform用户在其架构中使用字段组的频率决定。 数字越大，字段组就越受欢迎。 默认情况下，显示的结果会从最受欢迎到最不受欢迎，从而让您随时了解行业中的数据建模趋势。

![字段组热门程度](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform提供了一个用户界面和RESTful API，从中可以查看和管理Experience Platform中所有与架构相关的资源 **[!DNL Schema Library]**. 此 [!DNL Schema Library] 包含按Adobe为您提供的标准XDM组件，以及来自您使用应用程序的Experience Platform合作伙伴和供应商的资源。

使用 [!DNL Schema Registry API] 或 [!UICONTROL 架构] 工作区，您还可以创建和管理组织专属的新架构和资源。

有关如何在Platform中管理架构并与之交互的更多信息，请参阅以下文档：

* [XDM UI指南](./ui/overview.md)
* [架构注册表API指南](./api/overview.md)

## XDM系统中的数据行为 {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="数据行为"
>abstract="Experience Platform 中使用的数据分为三种行为类型：记录、时间序列和临时。记录架构提供有关主体属性的信息，时间序列架构在执行操作时捕获系统的快照。临时架构捕获作为仅由单个数据集使用的命名空间的字段。有关 Platform 中的数据行为的更多信息，请参阅文档。"

用于Experience Platform的数据分为三种行为类型：

* **记录**：提供有关主题属性的信息。 主体可以是组织，也可以是个人。
* **时间序列**：提供记录主体直接或间接执行操作时的系统快照。
* **临时**：捕获仅供单个数据集使用的命名空间字段。 临时架构用在各种数据摄取工作流中用于Experience Platform，包括摄取CSV文件和创建特定类型的源连接。

所有XDM架构都描述了可归类为记录或时间序列的数据。 架构的数据行为由架构的类定义，该类在首次创建架构时分配给架构。 XDM类描述架构必须包含的最小属性数，以便表示特定数据行为。

虽然您可以在 [!DNL Schema Registry]，建议您使用标准类 **[!UICONTROL XDM个人资料]** 和 **[!UICONTROL XDM ExperienceEvent]** 记录数据和时间序列数据。 下面将更详细地概述这些类。

>[!NOTE]
>
>没有基于临时行为的标准类。 临时架构由使用这些临时架构的Platform进程自动生成，但这些临时架构也可以 [使用架构注册表API手动创建](./tutorials/ad-hoc.md).

### [!UICONTROL XDM 个人资料] {#xdm-individual-profile}

[!UICONTROL XDM个人资料] 是基于记录的类，它构成已识别和部分识别主体的属性的单一表示。 高度识别的用户档案可用于个人通信或定向参与，并且可以包含详细的个人信息，例如姓名、性别、出生日期、位置以及联系信息（包括电话号码和电子邮件地址）。

识别较少的用户档案可能仅由匿名行为信号（如浏览器Cookie）组成。 在这种情况下，使用稀疏的配置文件数据来构建信息库，匿名配置文件的兴趣和偏好被整理并存储在该信息库中。 随着主体注册通知、订阅、购买等，这些标识符可能会随着时间的推移而变得更加详细。 用户档案属性的这种增加最终可导致识别的主题，并允许更高程度的目标参与。

随着用户档案的不断增长，它将成为包含个人信息、身份信息、联系详情和通信首选项的强大存储库。

请参阅 [[!UICONTROL XDM个人资料] 参考指南](./classes/individual-profile.md) 有关类提供的字段的结构和用例的更多信息。

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent是一个基于时间序列的类，用于在事件（或事件集）发生时捕获系统的状态，包括相关主体的时间点和身份。 体验事件是指在该时间点发生的情况的不可变、真实的记录，表示在没有聚合或解释的情况下发生的情况。 它们对于时域分析至关重要，因为它们可用于分析给定时间段内发生的更改，并用于在多个时间段之间进行比较以跟踪趋势。

体验事件可以是显式的，也可以是隐式的。 显式事件是旅程中某个时间点发生的直接可观察的人类行为。 隐含事件是在没有直接人类行动的情况下引发的，但仍与个人有关的事件。 隐式事件的示例可能包括按计划发送电子邮件新闻稿或电池电压达到特定阈值。

虽然并非所有事件都可以轻松地跨所有数据源进行分类，但尽可能将相似事件统一为相似类型以进行处理极具价值。

![ExperienceEvent客户历程](images/overview/experience-event-journey.png)

请参阅 [[!UICONTROL XDM ExperienceEvent] 参考指南](./classes/experienceevent.md) 有关类提供的字段的结构和用例的更多信息。

## XDM架构和Experience Platform服务

Experience Platform与架构无关，这意味着任何符合XDM标准的架构均可用于Platform服务。 下文将更详细地概述不同Platform服务使用架构的方式。

### 目录服务、数据摄取和数据湖

目录服务是Experience Platform资源及其相关架构的记录系统。 目录不包含实际的数据文件或目录，而是包含这些文件和目录的元数据和描述。

目录数据存储在“数据湖”中，这是一个高度精细化的数据存储区，包含由Platform管理的所有数据，而不管是源数据还是文件格式。

要开始将数据摄取到Experience Platform中，您可以使用目录服务创建数据集。 数据集引用了描述要摄取的数据结构的XDM架构。 如果创建的数据集没有架构，则Experience Platform通过检查摄取的数据字段的类型和内容来派生一个“观察到的架构”。 然后，在目录中跟踪数据集，并将其与架构以及它们所基于的观察架构一起存储在数据湖中。

欲知有关“目录”的更多信息，请参见 [目录服务概述](../catalog/home.md). 有关Adobe Experience Platform数据摄取的更多信息，请参阅 [数据引入概述](../ingestion/home.md).

### 查询服务

Adobe Experience Platform查询服务允许您使用标准SQL查询Experience Platform数据，以支持多种不同的用例。

在组合了架构并创建了引用该架构的数据集后，将会摄取数据并将其存储在数据湖中。 使用查询服务，您可以加入数据湖中的任何数据集，并将查询结果捕获为新数据集，以用于报表、机器学习或将其摄取到实时客户档案中。

请参阅 [查询服务概述](../query-service/home.md) 以了解有关该服务的更多信息。

### 实时客户配置文件

Real-Time Customer Profile为有针对性的个性化体验管理提供了一个集中式客户配置文件。 每个用户档案都包含跨所有系统汇总的数据，以及在您用于Experience Platform的任何系统中发生的涉及个人事件的可操作时间戳帐户。

Real-time Customer Profile使用基于以下项的架构格式数据 [!UICONTROL XDM个人资料] 和 [!UICONTROL XDM ExperienceEvent] 类，并根据这些数据响应查询。 配置文件不支持使用基于其他类的架构。

该系统维护每个客户个人资料的实例，将数据合并在一起，形成个人的“单一真实来源”。 这种统一的数据使用所谓的“联合架构”（有时称为“联合视图”）表示。 合并架构将实施相同类的所有架构的字段聚合到单个架构中。  使用UI或API构成架构时，您可以启用架构以用于Real-time Customer Profile，并将其标记以包含在合并中。 然后，标记的架构将参与馈送到用户档案的架构定义。

作为 [!UICONTROL XDM个人资料] 和 [!UICONTROL XDM ExperienceEvent] 数据被摄取到数据湖中，实时客户配置文件会摄取已启用以供使用的任何数据。 引入的交互和详细信息越多，个人资料就越可靠。

[!UICONTROL XDM个人资料] 数据有助于通知和增强任何渠道或Adobe产品集成中的操作。 当与丰富的行为和交互数据历史结合起来时，这些数据可用于推动机器学习。 Real-time Customer Profile API还可用于丰富第三方解决方案、CRM和专有解决方案的功能。

请参阅 [Real-time Customer Profile概述](../profile/home.md) 以了解更多信息。

### 数据科学工作区

Adobe Experience Platform数据科学工作区使用机器学习和人工智能从Experience Platform中存储的数据获取见解。 数据科学工作区允许数据科学家根据 [!UICONTROL XDM个人资料] 和 [!UICONTROL XDM ExperienceEvent] 有关客户及其活动的数据，有助于进行预测，例如购买倾向和个人可能欣赏和使用的推荐选件。

借助数据科学工作区，数据科学家可以轻松创建由机器学习提供支持的智能服务API。 这些服务可与其他Adobe解决方案(包括Adobe Target和Adobe Analytics Cloud)配合使用，帮助您自动提供个性化、有针对性的数字体验。

有关使用Experience Platform数据增强洞察功能的更多信息，请参阅 [数据科学工作区概述](../data-science-workspace/home.md).

## 后续步骤和其他资源

现在您已经更好地了解架构在整个Experience Platform中的角色，可以开始编写自己的架构了。

要了解用于构成要与Experience Platform一起使用的架构的设计原则和最佳实践，请从阅读 [模式组合基础](schema/composition.md). 有关如何创建架构的分步说明，请参阅有关创建架构的教程 [使用API](tutorials/create-schema-api.md) 或 [使用用户界面](tutorials/create-schema-ui.md).

加强您对 [!DNL XDM System] 在Experience Platform中，观看以下视频：

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
