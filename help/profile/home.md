---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API；统一用户档案；统一用户档案；统一；用户档案;rtcp;XDM图
title: 实时客户用户档案概述
topic-legacy: guide
description: 实时用户档案是一个通用的查找实体存储，它合并来自各种企业数据资产的数据，然后以单个客户用户档案和相关时间序列事件的形式提供对该数据的访问。 该功能使营销人员能够跨多个渠道通过受众推动协调一致的相关体验。
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1826'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] 概述

Adobe Experience Platform使您能够在客户与您的品牌互动的任何地方或何时为其提供协调一致的相关体验。 通过[!DNL Real-time Customer Profile]，您可以通过组合来自多个渠道（包括联机、脱机、CRM和第三方）的数据，了解每个客户的整体视图。 [!DNL Profile] 允许您将客户数据整合到一个统一的视图中，为每次客户互动提供一个可操作且有时间戳的帐户。本概述将帮助您了解[!DNL Experience Platform]中[!DNL Real-time Customer Profile]的角色和用法。

## [!DNL Profile] Experience Platform

以下示意图中突出显示了实时用户档案与Experience Platform内其他服务之间的关系：

![](images/profile-overview/profile-in-platform.png)

## 了解用户档案

[!DNL Real-time Customer Profile] 合并来自各种企业系统的数据，然后以客户用户档案的形式提供对这些数据的访问，并提供相关的时间序列事件。该功能使营销人员能够跨多个渠道通过受众推动协调一致的相关体验。 以下部分重点介绍了在平台内有效构建和维护用户档案所必须了解的一些核心概念。

### 用户档案数据存储

尽管[!DNL Real-time Customer Profile]处理摄取的数据并使用Adobe Experience Platform [!DNL Identity Service]通过标识映射合并相关数据，但它会在[!DNL Profile]数据存储中保留自己的数据。 [!DNL Profile]存储区与数据湖中的目录数据和标识图中的[!DNL Identity Service]数据分开。

用户档案存储使用Microsoft Azure Cosmos DB基础架构，而平台数据湖使用Microsoft Azure Data Lake存储。

### 用户档案护栏

Experience Platform提供了一系列护栏，帮助您避免创建“实时客户”用户档案无法支持的[体验模式(XDM)](../xdm/home.md)。 这包括会导致性能降低的软限制，以及会导致错误和系统故障的硬限制。 有关详细信息，包括列表指南和示例用例，请阅读[用户档案护栏](guardrails.md)文档。

### （测试版）用户档案仪表板{#profile-dashboard}

>[!IMPORTANT]
>
>仪表板功能当前处于测试阶段，并非所有用户都可用。 文档和功能可能会发生变化。

Experience Platform UI提供了一个仪表板，您可以通过它视图有关实时客户用户档案数据的重要信息，这些信息是在每日快照中捕获的。 要了解如何在UI中访问和使用[!DNL Profile]仪表板，以及有关仪表板中显示的量度的详细信息，请参阅[用户档案仪表板UI指南](ui/profile-dashboard.md)。

### 用户档案片段与合并用户档案{#profile-fragments-vs-merged-profiles}

每个客户用户档案都由多个用户档案片段组成，这些片段已合并，以形成该客户的单个视图。 例如，如果一个渠道跨多个用户档案与您的品牌互动，则您的组织将在多个数据集中显示与该单个客户相关的多个片段。 当这些片段被收录到平台中时，它们会合并在一起，以便为该客户创建单一用户档案。

当来自多个源的列表发生冲突(例如，一个片段将客户为“单一”，而其他片段将客户列表为“已婚”)时，[合并策略](#merge-policies)将确定要排定优先级并包含在个人用户档案中的信息。 因此，平台内的用户档案片段总数可能始终高于合并用户档案的总数，因为每个用户档案由多个片段组成。

### 记录数据

用户档案是主体、组织或个人的表示，由许多属性（也称为记录数据）组成。 例如，产品的用户档案可能包括SKU和说明，而个人的用户档案则包含名、姓和电子邮件地址等信息。 使用[!DNL Experience Platform]，您可以自定义用户档案以使用与业务相关的特定数据。 标准[!DNL Experience Data Model](XDM)类[!DNL XDM Individual Profile]是在描述客户记录数据时构建模式的首选类，并为平台服务之间的许多交互提供数据集成。 有关使用[!DNL Experience Platform]中的模式的详细信息，请首先阅读[ XDM系统概述](../xdm/home.md)。

### 时间系列事件

时间序列数据提供了在被拍摄者直接或间接采取行动时系统的快照，以及详细描述事件本身的数据。 由标准模式类XDM ExperienceEvent表示，时间序列数据可以描述事件，如添加到购物车的项目、被点击的链接和查看的视频。 时间序列数据可用于基于细分规则，并且事件可在用户档案的上下文中单独访问。

### 身份

每家企业都希望以个性化的方式与客户进行沟通。 但是，向客户提供相关数字体验的挑战之一是了解如何将互不关联的数据绑定到一起，这些数据通常分布在不同的数字渠道，如平板电脑、手机和笔记本电脑。 [!DNL Identity Service] 通过将多个渠道的身份关联并为每个客户创建一个身份图，您可以拼凑出客户的完整图。有关详细信息，请访问[Identity Service概述](../identity-service/home.md)。

### 合并策略

当将多个来源的数据片段汇集在一起并合并，以便了解每个客户的完整视图时，合并策略是[!DNL Platform]用来确定数据的优先级以及将哪些数据用于创建用户档案的规则。 当来自多个数据集的数据有冲突时，合并策略将确定如何处理该数据以及应使用哪个值。 使用REST风格的API或用户界面，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。

有关使用[!DNL Real-time Customer Profile] API处理合并策略的详细信息，请参阅[合并策略端点指南](api/merge-policies.md)。 要使用[!DNL Experience Platform] UI处理合并策略，请参阅[合并策略UI指南](ui/merge-policies.md)。

### 合并模式{#profile-fragments-and-union-schemas}

[!DNL Real-time Customer Profile]的一个关键功能是统一多渠道数据的能力。 当[!DNL Real-time Customer Profile]用于访问实体时，它可以为您提供跨数据集的该实体的所有用户档案片段的合并视图(称为“合并视图”)，并通过所谓的合并模式实现。

要进一步了解合并模式，包括如何在UI中访问合并模式，请访问[合并模式UI指南](ui/union-schema.md)。

### (Alpha)计算属性

>[!IMPORTANT]
>
>计算的属性功能在Alpha中。 文档和功能可能会发生更改。

计算属性是用于将事件级数据聚合为用户档案级属性的函数。 这些函数会自动计算，以便能够跨细分、激活和个性化使用。 这些计算可以帮助您轻松回答与终身购买价值、购买间隔时间或应用程序打开次数等相关的问题，无需在每次需要信息时手动执行复杂计算。 有关计算属性的详细信息(包括了解计算属性在Adobe Experience Platform中所起的作用)，请首先阅读[计算属性概述](computed-attributes/overview.md)。

## 用户档案和细分

Adobe Experience Platform [!DNL Segmentation Service]提供为个人客户提供体验所需的受众。 创建受众区段后，该区段的ID将添加到所有符合条件的用户档案的区段成员资格列表。 使用RESTful API和区段生成器用户界面构建区段规则并将其应用于[!DNL Real-time Customer Profile]数据。 要了解有关分段的更多信息，请首先阅读[分段服务概述](../segmentation/home.md)。

### 流摄取和流细分

通过称为流摄取的过程实现实时输入。 在摄取用户档案和时间序列数据时，[!DNL Real-time Customer Profile]会自动决定在将数据与现有数据合并并更新合并视图之前，通过称为流分段的持续过程将数据包括或排除在数据段中。 因此，在客户与您的品牌互动时，您可以即时执行计算并做出决策，为客户提供增强的个性化体验。 在摄取数据时，数据也会进行验证，以确保正确摄取数据并符合数据集所基于的模式。 有关摄取过程中执行哪些验证的详细信息，请首先阅读[数据摄取质量概述](../ingestion/quality/overview.md)。

## 边缘投影

为了实时为跨多个渠道的客户提供协调、一致和个性化的体验，需要随时提供正确的数据并在发生变化时不断更新。 Adobe Experience Platform通过使用所谓的边缘实现对数据的实时访问。 边缘是一个地理上放置的服务器，它存储数据并使应用程序能够轻松访问它。 例如，Adobe应用程序(如Adobe Target和Adobe Campaign)使用边缘，以实时提供个性化的客户体验。 通过投影将数据路由到边缘，投影目标定义要向其发送数据的边缘，以及定义将在边缘上提供的特定信息的投影配置。 要了解更多信息并开始使用[!DNL Real-time Customer Profile] API处理投影，请参阅[边缘投影端点指南](api/edge-projections.md)。

## 将数据收录到[!DNL Profile]

[!DNL Platform] 可以配置为向发送记录和时间序列数 [!DNL Profile]据，支持实时流摄取和批量摄取。有关详细信息，请参阅概述如何[向实时客户用户档案](tutorials/add-profile-data.md)添加数据的教程。

>[!NOTE]
>
>通过Adobe解决方案（包括[!DNL Analytics Cloud]、[!DNL Marketing Cloud]和[!DNL Advertising Cloud]）收集的数据会流入[!DNL Experience Platform]并被引入[!DNL Profile]。

### 用户档案摄取指标

可观察性洞察使您能够揭示Adobe Experience Platform中的关键指标。 除了[!DNL Experience Platform]各种[!DNL Platform]功能的使用情况统计和性能指标外，还有与用户档案相关的特定指标，使您能够洞察传入请求率、成功摄取率、摄取的记录大小等。 要了解更多信息，请首先阅读[可观察性洞察API概述](../observability/api/overview.md)，然后阅读[可用量度](../observability/api/metrics.md#available-metrics)的相关文档，了解实时客户用户档案量度的完整列表。

## [!DNL Data governance] 和 [!DNL Privacy]

[!DNL Data governance] 是用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策的一系列战略和技术。

由于与访问数据相关，数据治理在[!DNL Experience Platform]的不同级别中起着关键作用：
* 数据使用标签
* 数据访问策略
* 访问控制营销行动的数据

[!DNL Data governance] 在几个点进行管理。这包括确定引入[!DNL Platform]的数据以及针对给定营销操作引入后可访问的数据。 有关详细信息，请首先阅读[数据治理概述](../data-governance/home.md)。

### 处理退出和数据隐私请求

[!DNL Experience Platform] 使客户能够发送与其数据在中的使用和存储相关的退出请求 [!DNL Real-time Customer Profile]有关如何处理退出请求的详细信息，请参阅[支持退出请求](../segmentation/honoring-opt-outs.md)的相关文档。

## 后续步骤和其他资源

要了解有关使用Experience Platform UI或用户档案 API处理[!DNL Real-time Customer Profile]数据的更多信息，请首先阅读[用户档案UI指南](ui/user-guide.md)或[API开发人员指南](api/overview.md)。
