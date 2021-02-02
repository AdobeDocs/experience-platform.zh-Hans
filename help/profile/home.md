---
keywords: Experience Platform;用户档案；实时客户用户档案；故障排除；API；统一用户档案；统一用户档案；统一；用户档案;rtcp;XDM图
title: 实时客户用户档案概述
topic: guide
description: 实时用户档案是一个通用查找实体存储，它合并来自各种企业数据资产的数据，然后以单个客户用户档案和相关时间序列事件的形式提供对该数据的访问。 此功能使营销人员能够跨多个渠道通过受众推动协调一致的相关体验。
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 1%

---


# [!DNL Real-time Customer Profile]概述

Adobe Experience Platform使您能够为客户提供协调、一致和相关的体验，无论客户在何处或何时与您的品牌互动。 通过[!DNL Real-time Customer Profile]，您可以通过组合来自多个视图（包括联机、脱机、CRM和第三方）的数据，了解每位客户的整体渠道。 [!DNL Profile] 允许您将客户数据整合到统一的视图中，为每次客户互动提供一个具有可操作性且时间戳的帐户。本概述将帮助您了解[!DNL Experience Platform]中[!DNL Real-time Customer Profile]的角色和用法。

## [!DNL Profile] experience platform

实时客户用户档案与Experience Platform内其他服务之间的关系在下图中突出显示：

![](images/profile-overview/profile-in-platform.png)

## 了解用户档案

[!DNL Real-time Customer Profile] 合并来自各种企业系统的数据，然后以客户用户档案的形式提供对这些数据的访问，同时提供相关的时间序列事件。此功能使营销人员能够跨多个渠道通过受众推动协调一致的相关体验。 以下各节重点介绍了在平台内有效构建和维护用户档案所必须了解的一些核心概念。

### 用户档案数据存储

尽管[!DNL Real-time Customer Profile]处理摄取的数据并使用Adobe Experience Platform[!DNL Identity Service]通过身份映射合并相关数据，但它在[!DNL Profile]数据存储中保留自己的数据。 [!DNL Profile]存储区与数据湖中的目录数据和标识图中的[!DNL Identity Service]数据分开。

用户档案商店使用Microsoft Azure Cosmos DB基础架构，而平台数据湖使用Microsoft Azure数据湖存储。

### 用户档案护栏

Experience Platform提供了一系列护栏，帮助您避免创建实时客户用户档案无法支持的[体验数据模型(XDM)模式](../xdm/home.md)。 这包括会导致性能降低的软限制，以及会导致错误和系统故障的硬限制。 有关详细信息，包括列表指南和示例用例，请阅读[用户档案护栏](guardrails.md)文档。

### (Alpha)用户档案仪表板{#profile-dashboard}

>[!IMPORTANT]
>
>仪表板功能当前位于alpha中，并非所有用户都可用。 文档和功能可能会发生变化。

Experience PlatformUI提供了一个仪表板，您可以通过它视图有关实时客户用户档案数据的重要信息，这是在每日快照中捕获的。 要了解如何在UI中访问和使用[!DNL Profile]仪表板，以及有关仪表板中显示的度量的详细信息，请参阅[用户档案仪表板UI指南](ui/profile-dashboard.md)。

### 用户档案片段与合并用户档案{#profile-fragments-vs-merged-profiles}

每个客户用户档案都由多个用户档案片段组成，这些片段已合并成该客户的单个视图。 例如，如果客户在多个渠道中与您的品牌互动，您的组织将在多个数据集中显示与该单个客户相关的多个用户档案片段。 当这些片段被引入平台时，它们会合并在一起，以便为该客户创建单一用户档案。

当来自多个来源的列表发生冲突(例如，一个片段将客户为“单一”，而另一个片段将客户列表为“已婚”)时，[合并策略](#merge-policies)将确定要排定优先级并包含在个人用户档案中的信息。 因此，平台内用户档案片段的总数可能始终高于合并用户档案的总数，因为每个用户档案由多个片段组成。

### 记录数据

用户档案是主体、组织或个人的表示，由许多属性（也称为记录数据）组成。 例如，产品的用户档案可能包括SKU和说明，而人员的用户档案则包含诸如名字、姓和电子邮件地址等信息。 使用[!DNL Experience Platform]，您可以自定义用户档案以使用与业务相关的特定数据。 标准[!DNL Experience Data Model](XDM)类[!DNL XDM Individual Profile]是在描述客户记录数据时构建模式的首选类，并提供平台服务之间许多交互的数据集成。 有关使用[!DNL Experience Platform]中的模式的详细信息，请首先阅读[XDM系统概述](../xdm/home.md)。

### 时间系列事件

时间序列数据提供了被主体直接或间接采取行动时系统的快照，以及详细描述事件本身的数据。 由标准模式类XDM ExperienceEvent表示，时间序列数据可以描述事件，如添加到购物车的项目、被点击的链接和观看的视频。 时间序列数据可用于基于细分规则，并且事件可以在用户档案的上下文中单独访问。

### 身份

每家企业都希望以个性化的方式与客户进行沟通。 但是，为客户提供相关数字体验的一个挑战是了解如何将断开连接的数据绑定到一起，这种数据通常分布于不同的数字渠道，如平板电脑、手机和笔记本电脑。 [!DNL Identity Service] 通过将多个渠道的身份关联起来并为每个客户创建一个身份图，您可以拼凑出完整的客户图。有关详细信息，请访问[Identity Service概述](../identity-service/home.md)。

### 合并策略

当将多个来源的视图片段汇总在一起并合并它们，以便查看每个客户的完整用户档案时，合并策略是[!DNL Platform]用来确定数据的优先级以及将哪些数据用于创建客户的规则。 当来自多个数据集的数据有冲突时，合并策略将确定如何处理该数据以及应使用哪个值。 使用REST风格的API或用户界面，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。

有关使用[!DNL Real-time Customer Profile] API处理合并策略的详细信息，请参阅[合并策略端点指南](api/merge-policies.md)。 要使用[!DNL Experience Platform] UI处理合并策略，请参阅[合并策略UI指南](ui/merge-policies.md)。

### 合并模式{#profile-fragments-and-union-schemas}

[!DNL Real-time Customer Profile]的一个主要特点是能够统一多渠道数据。 当[!DNL Real-time Customer Profile]用于访问实体时，它可以为您提供该实体跨数据集的所有用户档案片段的合并视图(称为“合并视图”)，并通过称为合并模式来实现。

要进一步了解合并模式，包括如何在UI中访问合并模式，请访问[合并模式UI指南](ui/union-schema.md)。

### (Alpha)计算属性

>[!IMPORTANT]
>
>计算的属性功能在alpha中。 文档和功能可能会发生变化。

通过计算属性，您可以根据其他值、计算和表达式自动计算字段的值。 计算属性在用户档案级别上操作，这意味着您可以跨所有记录和事件聚合值。 每个计算属性都包含一个表达式，即“规则”，用于评估传入的数据并将所得值存储在用户档案属性或事件中。 这些计算有助于您轻松回答与终身购买价值、购买间隔时间或应用程序打开次数等相关的问题，无需在每次需要信息时手动执行复杂的计算。 有关计算属性以及使用[!DNL Real-time Customer Profile] API使用这些属性的分步说明的详细信息，请参阅[计算属性终结点指南](api/computed-attributes.md)。 本指南将帮助您更好地了解计算属性在Adobe Experience Platform的作用，它包含执行基本CRUD操作的示例API调用。

## 用户档案和细分

Adobe Experience Platform[!DNL Segmentation Service]为每位客户提供体验所需的受众。 创建受众区段后，该区段的ID将添加到所有符合条件的用户档案的区段成员资格列表中。 使用RESTful API和Segment Builder用户界面构建区段规则并将其应用于[!DNL Real-time Customer Profile]数据。 要了解有关分段的更多信息，请首先阅读[分段服务概述](../segmentation/home.md)。

### 流摄取和流细分

通过称为流摄取的过程实现实时输入。 在摄取用户档案和时间序列数据时，[!DNL Real-time Customer Profile]会自动决定在将数据与现有数据合并并更新合并视图之前，通过称为流分段的持续过程将数据包括或排除在数据段中。 因此，在客户与您的品牌互动时，您可以即时执行计算并做出决策，为客户提供增强的个性化体验。 在摄取数据时，还会进行验证，以确保正确摄取数据并符合数据集所基于的模式。 有关摄取过程中执行哪些验证的详细信息，请首先阅读[数据摄取质量概述](../ingestion/quality/overview.md)。

## 边缘投影

为了跨多个渠道为客户实时提供协调、一致、个性化的体验，需要随时提供正确的数据，并在发生变化时不断更新。 Adobe Experience Platform通过使用所谓的边缘，实现对数据的实时访问。 边缘是一个地理上放置的服务器，它存储数据并使应用程序能够方便地访问它。 例如，Adobe应用程序(如Adobe Target和Adobe Campaign)使用边缘，以便实时提供个性化的客户体验。 数据通过投影被路由到边缘，投影目标定义要向其发送数据的边缘，投影配置定义要在边缘上提供的特定信息。 要了解更多信息并开始使用[!DNL Real-time Customer Profile] API处理投影，请参阅[边缘投影端点指南](api/edge-projections.md)。

## 将数据引入[!DNL Profile]

[!DNL Platform] 可以配置为向发送记录和时间序列数据， [!DNL Profile]支持实时流摄取和批量摄取。有关详细信息，请参阅概述如何[向实时客户用户档案添加数据的教程](tutorials/add-profile-data.md)。

>[!NOTE]
>
>通过Adobe解决方案（包括[!DNL Analytics Cloud]、[!DNL Marketing Cloud]和[!DNL Advertising Cloud]）收集的数据会流入[!DNL Experience Platform]并被引入[!DNL Profile]。

### 用户档案摄取指标

可观性洞察使您能够揭示Adobe Experience Platform的关键指标。 除了[!DNL Experience Platform]各种[!DNL Platform]功能的使用统计和性能指标外，还有与用户档案相关的特定指标，使您能够深入了解传入请求率、成功摄取率、摄取的记录大小等。 要了解更多信息，请首先阅读[可观察性洞察API概述](../observability/api/overview.md)，然后阅读有关实时客户用户档案指标的完整列表，请参阅[可用指标](../observability/api/metrics.md#available-metrics)的相关文档。

## [!DNL Data governance] 和 [!DNL Privacy]

[!DNL Data governance] 是用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策的一系列战略和技术。

由于与访问数据相关，数据管理在[!DNL Experience Platform]的不同级别中起着关键作用：
* 数据使用标签
* 数据访问策略
* 访问控制营销行动的数据

[!DNL Data governance] 在几个点进行管理。这包括确定引入[!DNL Platform]的数据，以及针对特定营销操作引入后可访问的数据。 有关详细信息，请首先阅读[数据管理概述](../data-governance/home.md)。

### 处理退出和数据隐私请求

[!DNL Experience Platform] 使客户能够发送与其数据在中的使用和存储相关的退出请求 [!DNL Real-time Customer Profile]。有关如何处理退出请求的详细信息，请参阅[支持退出请求的文档](../segmentation/honoring-opt-outs.md)。

## 后续步骤和其他资源

要进一步了解如何使用Experience PlatformUI或用户档案API处理[!DNL Real-time Customer Profile]数据，请首先阅读[用户档案UI指南](ui/user-guide.md)或[API开发人员指南](api/overview.md)。