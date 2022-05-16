---
keywords: Experience Platform；配置文件；实时客户配置文件；故障诊断；API；统一配置文件；统一配置文件；统一；配置文件；rtcp;XDM图形
title: 实时客户资料概述
topic-legacy: guide
description: 实时客户资料可合并各种来源的数据，并以单个客户资料和相关时间系列事件的形式提供对该数据的访问。 通过此功能，营销人员能够跨多个渠道与其受众推动协调、一致和相关的体验。
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: d2182b48e21de059f12ad8923bb3b420ed87bcfc
workflow-type: tm+mt
source-wordcount: '2046'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile]概述

Adobe Experience Platform使您能够为客户在何处或何时与您的品牌进行交互，从而提供协调、一致的相关体验。 使用 [!DNL Real-time Customer Profile]，您可以通过合并来自多个渠道（包括在线、离线、CRM和第三方）的数据，来全面了解每个客户。 [!DNL Profile] 允许您将客户数据整合到统一视图中，为每次客户互动提供一个可操作且带有时间戳的帐户。 此概述将帮助您了解的角色和用法 [!DNL Real-time Customer Profile] in [!DNL Experience Platform].

## [!DNL Profile] Experience Platform

下图突出显示了Experience Platform内实时客户资料与其他服务之间的关系：

![实时客户资料与Adobe Experience Platform中其他服务之间的关系。 此图表显示，配置文件是Adobe Experience Platform的核心组件之一。](images/profile-overview/profile-in-platform.png)

## 了解用户档案

[!DNL Real-time Customer Profile] 合并来自各种企业系统的数据，然后通过相关时间序列事件以客户配置文件的形式提供对该数据的访问。 通过此功能，营销人员能够跨多个渠道与其受众推动协调、一致和相关的体验。 以下部分重点介绍为了在Platform中有效构建和维护用户档案，您必须了解的一些核心概念。

### 用户档案实体组合

实时客户资料由称为 **主要实体**，以及各种支持实体。 主实体由用户档案的特征、行为和区段成员关系组成。 其他实体允许分段引擎利用用户档案主实体外的数据，并包括以下内容：

- **维度实体**:用于简化跨事件或用户档案记录共享信息的数据建模过程的实体。 这也称为查找实体或分类实体。
- **B2B实体**:描述用户档案与业务对业务帐户和商机关系的实体。

![说明用户档案实体组成的图表。](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>由于维度和B2B实体仅存在于主实体外部，因此它们仅用于批量分段。

### 配置文件数据存储

尽管 [!DNL Real-time Customer Profile] 处理摄取的数据并使用Adobe Experience Platform [!DNL Identity Service] 要通过身份映射合并相关数据，它会在 [!DNL Profile] 数据存储。 的 [!DNL Profile] 存储与数据湖中的目录数据分开，并且 [!DNL Identity Service] 标识图中的数据。

配置文件存储使用Microsoft Azure Cosmos DB基础架构，而平台数据湖使用Microsoft Azure Data Lake存储。

### 配置文件护栏

Experience Platform提供了一系列护栏，以帮助您避免创建 [体验数据模型(XDM)架构](../xdm/home.md) 实时客户资料不支持的区段。 这包括软限制，这些软限制将导致性能降低，而硬限制将导致错误和系统中断。 有关更多信息（包括准则和示例用例列表），请阅读 [配置文件护栏](guardrails.md) 文档。

### 用户档案仪表板 {#profile-dashboard}

Experience PlatformUI提供了一个功能板，您可以通过该功能板查看有关实时客户配置文件数据的重要信息，这些信息是在每日快照期间捕获的。 了解如何访问和使用 [!DNL Profile] 界面中的功能板，以及与功能板中显示的量度有关的详细信息，请参阅 [配置文件功能板UI指南](ui/profile-dashboard.md).

### 配置文件片段与合并的配置文件 {#profile-fragments-vs-merged-profiles}

每个客户配置文件都由多个配置文件片段组成，这些片段已合并，以形成该客户的单一视图。 例如，如果客户跨多个渠道与您的品牌进行交互，则您的组织将在多个数据集中显示与该单个客户相关的多个配置文件片段。 将这些片段摄取到Platform后，它们会合并在一起，以便为该客户创建单个配置文件。

换句话说，配置文件片段表示唯一的主标识和相应的 [记录](#record-data) 或 [事件](#time-series-events) 给定数据集中该ID的数据。

当来自多个数据集的数据发生冲突（例如，一个片段将客户列为“单个”，而另一个片段将客户列为“已婚”）时， [合并策略](#merge-policies) 确定要排定优先级的信息，并将其包含在个人的用户档案中。 因此，Platform中的配置文件片段总数可能始终高于合并的配置文件总数，因为每个配置文件通常由多个数据集中的多个片段组成。

### 记录数据 {#record-data}

用户档案是主体、组织或个人的表示形式，由许多属性（也称为记录数据）组成。 例如，产品的配置文件可能包含SKU和描述，而人员的配置文件包含名字、姓氏和电子邮件地址等信息。 使用 [!DNL Experience Platform]，则可以自定义用户档案以使用与您的业务相关的特定数据。 标准 [!DNL Experience Data Model] (XDM)类、 [!DNL XDM Individual Profile]，是在描述客户记录数据时构建模式的首选类，并为Platform服务之间的许多交互提供数据集成。 有关在 [!DNL Experience Platform]，请首先阅读 [XDM系统概述](../xdm/home.md).

### 时间系列事件 {#time-series-events}

时间序列数据提供了在主体直接或间接采取某项操作时系统的快照，以及详细描述事件本身的数据。 时间系列数据由标准架构类XDM ExperienceEvent表示，它可描述各种事件，如添加到购物车的项目、被点击的链接以及查看的视频。 时间系列数据可用于根据分段规则，并且可以在用户档案的上下文中单独访问事件。

### 标识

每家企业都想以一种感觉上属于个人的方式与客户沟通。 但是，向客户提供相关数字体验的其中一个挑战是了解如何将其断开连接的数据绑定在一起，这些数据通常分布在不同的数字渠道中，如平板电脑、手机和笔记本电脑。 [!DNL Identity Service] 允许您通过关联多个渠道的身份并为每个客户创建身份图，从而将客户的完整图片拼合在一起。 访问 [Identity Service概述](../identity-service/home.md) 以了解更多信息。

### 合并策略

将多个来源的数据片段合并在一起，以便查看每个客户的完整视图时，合并策略是 [!DNL Platform] 用于确定数据的优先级以及将使用哪些数据来创建客户用户档案。

当来自多个数据集的数据存在冲突时，合并策略会确定应如何处理该数据以及应使用哪个值。 通过RESTful API或用户界面，您可以创建新的合并策略、管理现有策略，并为您的组织设置默认的合并策略。

要了解有关合并策略及其在Experience Platform中的角色的更多信息，请首先阅读 [合并策略概述](merge-policies/overview.md).

### 并集模式 {#profile-fragments-and-union-schemas}

的主要功能之一 [!DNL Real-time Customer Profile] 是统一多渠道数据的功能。 When [!DNL Real-time Customer Profile] 用于访问实体，它可以为您提供跨数据集的该实体所有配置文件片段的合并视图（称为“合并视图”），并通过称为合并架构的架构实现该视图。

要进一步了解并集模式，包括如何在UI中访问并集模式，请访问 [并集架构UI指南](ui/union-schema.md).

### (Alpha)计算属性

>[!IMPORTANT]
>
>计算属性功能位于Alpha中。 文档和功能可能会发生更改。

计算属性是用于将事件级别数据聚合到配置文件级别属性中的函数。 这些函数会自动计算，以便在分段、激活和个性化期间使用。 这些计算有助于您轻松回答与生命周期购买值、购买间隔时间或应用程序打开次数等相关的问题，而无需您每次需要信息时都手动执行复杂的计算。 有关计算属性的更多信息(包括了解计算属性在Adobe Experience Platform中发挥的角色)，请首先阅读 [计算属性概述](computed-attributes/overview.md).

## 用户档案和区段

Adobe Experience Platform [!DNL Segmentation Service] 会生成为各个客户提供体验所需的受众。 创建受众区段后，该区段的ID会添加到所有符合条件的用户档案的区段成员资格列表。 区段规则的生成和应用于 [!DNL Real-time Customer Profile] 使用RESTful API和区段生成器用户界面的数据。 要了解有关分段的更多信息，请首先阅读 [Segmentation Service概述](../segmentation/home.md).

### 流式摄取和流式分段

通过称为流摄取的过程实现实时输入。 在摄取用户档案和时间系列数据时， [!DNL Real-time Customer Profile] 在将数据与现有数据合并并更新并集视图之前，自动决定通过称为流分段的持续流程，将该数据包含或排除在区段中。 因此，您可以即时执行计算并做出决策，在客户与您的品牌进行交互时为客户提供增强的个性化体验。 在摄取数据时，还会进行验证以确保正确摄取数据，并符合数据集所基于的架构。 有关在摄取期间执行的验证操作的更多信息，请首先阅读 [数据摄取质量概述](../ingestion/quality/overview.md).

## 边缘投影

为了跨多个渠道为客户实时提供协调、一致和个性化的体验，需要随时提供适当的数据，并在发生更改时不断更新。 Adobe Experience Platform允许通过使用称为边缘的内容来实时访问数据。 边缘是位于地理位置的服务器，用于存储数据并使应用程序能够轻松访问它。 例如，Adobe应用程序(如Adobe Target和Adobe Campaign)使用边缘，以便实时提供个性化的客户体验。 数据通过投影被路由到边缘，其中，投影目标定义要向其发送数据的边缘，以及投影配置定义将在边缘上提供的特定信息。 要了解更多信息并开始使用 [!DNL Real-time Customer Profile] API，请参阅 [边缘投影端点指南](api/edge-projections.md).

## 将数据摄取到 [!DNL Profile]

[!DNL Platform] 可以配置为将记录和时序数据发送到 [!DNL Profile]，支持实时流式摄取和批量摄取。 有关更多信息，请参阅概述如何 [将数据添加到实时客户资料](tutorials/add-profile-data.md).

>[!NOTE]
>
>通过Adobe解决方案收集的数据，包括 [!DNL Analytics Cloud], [!DNL Marketing Cloud]和 [!DNL Advertising Cloud]，流入 [!DNL Experience Platform] 并被摄取到 [!DNL Profile].

### 配置文件摄取量度

可观察性分析允许您在Adobe Experience Platform中显示关键量度。 除 [!DNL Experience Platform] 各种使用情况统计和业绩指标 [!DNL Platform] 功能中，提供了一些与用户档案相关的特定量度，可让您深入了解传入请求率、成功摄取率、摄取的记录大小等。 要了解更多信息，请首先阅读 [可观察性分析API概述](../observability/api/overview.md)，以及实时客户配置文件量度的完整列表，请参阅 [可用量度](../observability/api/metrics.md#available-metrics).

## 更新配置文件存储数据

有时可能需要更新贵组织的用户档案存储区中的数据。 例如，您可能需要更正记录或更改属性值。 这可以通过批量摄取完成，并且需要一个启用了配置文件的数据集，该数据集配置了一个更新标记。 有关如何配置数据集以进行属性更新的更多信息，请参阅 [为配置文件启用数据集并重新插入](../catalog/datasets/enable-upsert.md).

## 数据管理和 [!DNL Privacy]

“数据管理”是用于管理客户数据并确保遵守适用于数据使用的法规、限制和策略的一系列策略和技术。

由于数据管理与访问数据有关，因此在 [!DNL Experience Platform] 在不同级别：

- 数据使用标签设置
- 数据访问策略
- 对营销操作数据的访问控制

“数据管理”在几个点进行管理。 这包括确定要引入哪些数据 [!DNL Platform] 以及在为给定营销操作摄取后可访问哪些数据。 有关更多信息，请首先阅读 [数据管理概述](../data-governance/home.md).

### 处理选择禁用和数据隐私请求

[!DNL Experience Platform] 允许您的客户发送与其数据在 [!DNL Real-time Customer Profile]. 有关如何处理选择退出请求的更多信息，请参阅 [响应选择退出请求](../segmentation/consents.md).

## 后续步骤和其他资源

要了解有关使用Experience PlatformUI或用户档案API处理实时客户用户档案数据的更多信息，请首先阅读 [配置文件UI指南](ui/user-guide.md) 或 [API开发人员指南](api/overview.md)，分别为。
