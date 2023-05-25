---
keywords: Experience Platform；个人资料；实时客户个人资料；故障排除；API；统一个人资料；统一个人资料；统一；个人资料；rtcp；XDM图形
title: Real-Time Customer Profile概述
description: Real-time Customer Profile可合并来自各种来源的数据，并以单个客户配置文件和相关时间序列事件的形式提供对这些数据的访问。 此功能使营销人员能够跨多个渠道推动与其受众协调、一致且相关的体验。
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] 概述

通过Adobe Experience Platform，无论客户在何处或何时与您的品牌互动，您都可以为其推动协调、一致且相关的体验。 替换为 [!DNL Real-Time Customer Profile]，您可以通过组合来自多个渠道（包括在线、离线、CRM和第三方）的数据来查看每个客户的整体视图。 [!DNL Profile] 允许您将客户数据整合到一个统一视图中，并提供每个客户交互的带时间戳的可操作帐户。 此概述将帮助您了解的角色和用法 [!DNL Real-Time Customer Profile] 在 [!DNL Experience Platform].

## [!DNL Profile] 在Experience Platform中

下图突出显示了Real-time Customer Profile与Experience Platform内其他服务之间的关系：

![Real-Time Customer Profile与Adobe Experience Platform中的其他服务之间的关系。 此图显示配置文件是Adobe Experience Platform的核心组件之一。](images/profile-overview/profile-in-platform.png)

## 了解用户档案

[!DNL Real-Time Customer Profile] 合并来自各种企业系统的数据，然后以客户档案的形式提供对相关时间序列事件的数据访问。 此功能使营销人员能够跨多个渠道推动与其受众协调、一致且相关的体验。 以下部分重点介绍您必须了解的一些核心概念，以便在Platform中有效构建和维护用户档案。

### 个人资料实体组合

Real-time Customer Profile由一个称为 **主要实体**&#x200B;和各种支持实体。 在Experience Platform的上下文中，主要实体通常是 **配置文件实体**，由个人特征、行为和区段成员资格组成。 其他实体允许分段引擎利用用户档案的主要实体以外的数据，并且包括以下内容：

- **维度实体**：用于简化跨事件或配置文件记录共享的信息的数据建模过程的实体。 这也称为查找实体或分类实体。
- **B2B实体**：描述用户档案与企业对企业的客户和机会关系的实体。

![说明用户档案实体组成的图。](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>由于维度和B2B实体仅存在于主要实体之外，因此它们仅用于批量分段。

维度和B2B实体通过以下方式链接到主要实体 **架构关系**. 有关更多信息，请参阅以下文档：

- [为查找实体创建一对一架构关系](../xdm/tutorials/relationship-ui.md)
- [为B2B实体创建多对一架构关系](../xdm/tutorials/relationship-b2b.md)

### 配置文件数据存储

虽然 [!DNL Real-Time Customer Profile] 处理摄取的数据并使用Adobe Experience Platform [!DNL Identity Service] 要通过身份映射合并相关数据，它会将自己的数据保留在 [!DNL Profile] 数据存储。 此 [!DNL Profile] 存储区与数据湖中目录数据分离，并且 [!DNL Identity Service] 身份图中的数据。

配置文件存储使用Microsoft Azure Cosmos DB基础结构，平台数据湖使用Microsoft Azure Data Lake存储。

### 轮廓护栏

Experience Platform提供了一系列护栏，帮助您避免创建 [Experience Data Model (XDM)架构](../xdm/home.md) Real-Time Customer Profile无法支持的功能。 这包括会导致性能下降的软限制，以及会导致错误和系统中断的硬限制。 欲知更多信息（包括一系列准则和示例用例），请阅读 [轮廓护栏](guardrails.md) 文档。

### 配置文件仪表板 {#profile-dashboard}

Experience PlatformUI提供了一个仪表板，通过该仪表板可以查看有关实时客户配置文件数据的重要信息，如在每日快照期间捕获的数据。 了解如何访问和使用 [!DNL Profile] UI中的仪表板，以及有关该仪表板中显示的量度的详细信息，请参阅 [配置文件功能板UI指南](ui/profile-dashboard.md).

### 配置文件片段与合并的配置文件 {#profile-fragments-vs-merged-profiles}

每个客户配置文件都由多个配置文件片段组成，这些片段已合并以形成该客户的单一视图。 例如，如果客户跨多个渠道与您的品牌互动，则您的组织将有多个与该单个客户相关的配置文件片段出现在多个数据集中。 将这些片段摄取到Platform后，会将其合并在一起，以便为该客户创建一个配置文件。

换句话说，配置文件片段表示唯一的主要身份和相应的 [记录](#record-data) 或 [事件](#time-series-events) 给定数据集中该ID的数据。

当来自多个数据集的数据发生冲突时（例如，一个片段将客户列为“单身”，而另一个片段将客户列为“已婚”）， [合并策略](#merge-policies) 确定个人资料中要优先包含哪些信息。 因此，Platform中的配置文件片段总数可能始终高于合并的配置文件总数，因为每个配置文件通常由来自多个数据集的多个片段组成。

### 记录数据 {#record-data}

用户档案是主体、组织或个人的表示形式，由许多属性（也称为记录数据）组成。 例如，产品的配置文件可能包括SKU和描述，而人员的配置文件包含名字、姓氏和电子邮件地址等信息。 使用 [!DNL Experience Platform]，您可以自定义用户档案以使用与业务相关的特定数据。 标准 [!DNL Experience Data Model] (XDM)类， [!DNL XDM Individual Profile]，是描述客户记录数据时用来构建架构的首选类，它提供的数据是Platform服务之间许多交互不可或缺的一部分。 有关在中使用架构的更多信息 [!DNL Experience Platform]，请先阅读 [XDM系统概述](../xdm/home.md).

### 时间序列事件 {#time-series-events}

时序数据提供主体直接或间接执行操作时的系统快照，以及详细说明事件本身的数据。 时间序列数据由标准架构类XDM ExperienceEvent表示，可以描述事件，例如添加到购物车的项目、点击的链接和查看的视频。 时间序列数据可用于作为分段规则的基础，事件可在用户档案的上下文中单独访问。

### 标识

每家企业都希望以一种个人化的方式与客户沟通。 但是，向客户交付相关数字体验的挑战之一是了解如何将他们的互联数据绑定在一起，这通常散布在平板电脑、手机和笔记本电脑等不同的数字渠道中。 [!DNL Identity Service] 允许您通过关联来自多个渠道的身份并为每个客户创建身份图，将客户的整体情况拼合在一起。 访问 [Identity服务概述](../identity-service/home.md) 了解更多信息。

### 合并策略

将来自多个源的数据片段聚集在一起并进行组合以便查看每个客户的完整视图时，合并策略是指 [!DNL Platform] 使用确定数据的优先顺序以及用于创建客户用户档案的数据。

当多个数据集中存在冲突数据时，合并策略会确定应如何处理该数据以及应使用哪个值。 通过RESTful API或用户界面，您可以创建新的合并策略、管理现有策略以及为组织设置默认合并策略。

要了解有关合并策略及其在Experience Platform中的角色的更多信息，请首先阅读 [合并策略概述](merge-policies/overview.md).

### 合并模式 {#profile-fragments-and-union-schemas}

的主要功能之一 [!DNL Real-Time Customer Profile] 是统一多渠道数据的能力。 时间 [!DNL Real-Time Customer Profile] 用于访问实体，可为您提供该实体在数据集间的所有配置文件片段的合并视图，称为“合并视图”，可通过称为合并架构的方式实现。

要了解有关合并架构的更多信息，包括如何在UI中访问合并架构，请访问 [合并架构UI指南](ui/union-schema.md).

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## 用户档案和区段

Adobe Experience Platform [!DNL Segmentation Service] 生成支持个人客户体验所需的受众。 创建受众区段后，该区段的ID会添加到所有符合条件的用户档案的区段成员资格列表中。 生成区段规则并将其应用于 [!DNL Real-Time Customer Profile] 数据使用RESTful API和区段生成器用户界面。 要了解有关分段的更多信息，请先阅读 [分段服务概述](../segmentation/home.md).

### 流摄取和流分段

实时输入可通过称为流式摄取的过程实现。 当配置文件和时序数据被摄取时， [!DNL Real-Time Customer Profile] 在将区段与现有数据合并并更新合并视图之前，通过称为流式客户细分的持续过程，自动决定从区段包含或排除该数据。 因此，您可以即时执行计算并做出决策，以便在客户与您的品牌互动时为他们提供经过增强、个性化的体验。 在摄取数据时，还会对其进行验证，以确保数据被正确摄取，并符合数据集所基于的架构。 有关在摄取期间执行的验证的更多信息，请从阅读 [数据摄取质量概述](../ingestion/quality/overview.md).

## 边缘投影

为了实时推动跨多个渠道为客户提供协调、一致和个性化的体验，需要随时提供正确的数据，并在发生更改时不断更新。 Adobe Experience Platform通过使用称为边缘的功能，实现了数据的实时访问。 Edge是位于不同地理位置的服务器，用于存储数据并使应用程序能够轻松访问数据。 例如，Adobe应用程序(如Adobe Target和Adobe Campaign)使用边缘来实时提供个性化的客户体验。 数据通过投影被路由到边缘，投影目的地定义数据将发送到的边缘，投影配置定义将在边缘上可用的特定信息。 要了解更多信息并开始使用预测，请使用 [!DNL Real-Time Customer Profile] API，请参阅 [边缘投影端点指南](api/edge-projections.md).

## 将数据摄取到 [!DNL Profile]

[!DNL Platform] 可以配置为将记录和时间序列数据发送到 [!DNL Profile]，支持实时流摄取和批量摄取。 有关更多信息，请参阅概述以下操作的教程： [将数据添加到Real-time Customer Profile](tutorials/add-profile-data.md).

>[!NOTE]
>
>通过Adobe解决方案收集的数据，包括 [!DNL Analytics Cloud]， [!DNL Marketing Cloud]、和 [!DNL Advertising Cloud]，流入 [!DNL Experience Platform] 并引入 [!DNL Profile].

### 配置文件摄取量度

可观察性分析允许您在Adobe Experience Platform中公开关键量度。 除此之外 [!DNL Experience Platform] 各种使用情况统计和绩效指标 [!DNL Platform] 通过各种功能，您可以了解与配置文件相关的特定指标，从而深入了解传入请求率、成功摄取率、摄取记录大小等。 要了解更多信息，请从阅读 [Observability Insights API概述](../observability/api/overview.md)和有关Real-time Customer Profile量度的完整列表，请参阅以下文档： [可用量度](../observability/api/metrics.md#available-metrics).

## 更新配置文件存储数据

有时候，可能需要更新您组织的配置文件存储区中的数据。 例如，您可能需要更正记录或更改属性值。 这可以通过批量摄取完成，并且需要为启用了配置文件的数据集配置更新插入标记。 有关如何为属性更新配置数据集的更多信息，请参阅的教程 [为配置文件和更新插入启用数据集](../catalog/datasets/enable-upsert.md).

## 数据治理和 [!DNL Privacy]

数据治理是用于管理客户数据并确保遵守适用于数据使用的法规、限制和策略的一系列策略和技术。

由于数据治理与访问数据相关，因此它在以下方面起着关键作用： [!DNL Experience Platform] 在各个级别：

- 数据使用情况标签
- 数据访问策略
- 营销活动数据的访问控制

数据治理在多个时间点进行管理。 这包括决定要将哪些数据摄取到 [!DNL Platform] 以及引入后给定营销操作可以访问哪些数据。 欲知更多信息，请阅读 [数据治理概述](../data-governance/home.md).

### 处理选择退出和数据隐私请求

[!DNL Experience Platform] 使您的客户能够发送与其数据的使用和存储相关的选择退出请求 [!DNL Real-Time Customer Profile]. 有关如何处理选择退出请求的更多信息，请参阅上的文档 [接受选择退出请求](../segmentation/consents.md).

## 后续步骤和其他资源

要了解有关使用Experience PlatformUI或配置文件API处理实时客户配置文件数据的更多信息，请从阅读 [配置文件UI指南](ui/user-guide.md) 或 [API开发人员指南](api/overview.md)，则不会显示任何内容。
