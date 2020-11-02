---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;XDM graphs
title: 实时客户用户档案概述
topic: guide
description: 实时用户档案是一个通用查找实体存储，它合并来自各种企业数据资产的数据，然后以单个客户用户档案和相关时间序列事件的形式提供对该数据的访问。 此功能使营销人员能够跨多个渠道通过受众推动协调一致的相关体验。
translation-type: tm+mt
source-git-commit: 47c65ef5bdd083c2e57254189bb4a1f1d9c23ccc
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile]概述

Adobe Experience Platform使您能够为客户提供协调、一致和相关的体验，无论客户在何处或何时与您的品牌互动。 您 [!DNL Real-time Customer Profile]可以看到每个客户的整体视图，该渠道组合了多个的数据，包括在线、离线、CRM和第三方数据。 [!DNL Profile] 允许您将不同的客户数据整合到统一的视图中，为每次客户互动提供一个具有可操作性、时间戳记的帐户。 此概述将帮助您了解中的角色和 [!DNL Real-time Customer Profile] 使用 [!DNL Experience Platform]。

## [!DNL Profile] experience platform

实时客户用户档案与Experience Platform内其他服务之间的关系在下图中突出显示：

![Adobe Experience Platform服务。](images/profile-overview/profile-in-platform.png)

### 用户档案数据存储

尽管 [!DNL Real-time Customer Profile] 处理摄取的数据并使用Adobe Experience Platform [!DNL Identity Service] 通过身份映射来合并相关数据，但它在存储中保留自己的 [!DNL Profile] 数据。 换句话说，存储 [!DNL Profile] 区与数据( [!DNL Catalog] )和[!DNL Data Lake]数据(标 [!DNL Identity Service] 识图)分开。

### 用户档案护栏

Experience Platform提供了一系列护栏，帮助您避 [免创建实时客户用户档案无法支](../xdm/home.md) 持的体验模式模型(XDM)。 这包括会导致性能降低的软限制，以及会导致错误和系统故障的硬限制。 有关详细信息(包括一列表准则和示例用例)，请阅读 [用户档案护栏](guardrails.md) 文档。

## 了解用户档案

[!DNL Real-time Customer Profile] 合并来自各种企业系统的数据，然后以客户用户档案的形式提供对这些数据的访问，同时提供相关的时间序列事件。 此功能使营销人员能够跨多个渠道通过受众推动协调一致的相关体验。 以下各节重点介绍了在平台内有效构建和维护用户档案所必须了解的一些核心概念。

### 用户档案片段与合并用户档案

每个客户用户档案都由多个用户档案片段组成，这些片段已合并成该客户的单个视图。 例如，如果客户在多个渠道中与您的品牌互动，您的组织将在多个数据集中显示与该单个客户相关的多个用户档案片段。 当这些片段被引入平台时，它们会合并在一起，以便为该客户创建单一用户档案。

当来自多个来源的列表发生冲突(例如，一个片段将客户为“单一”，而另一个列表客户为“已婚”)时，合并策略将确定要排定优先级的信息，并将其包含在个人的用户档案中。 [](#merge-policies) 因此，平台内用户档案片段的总数可能始终高于合并用户档案的总数，因为每个用户档案由多个片段组成。

### 记录数据

用户档案是主体、组织或个人的表示，由许多属性（也称为记录数据）组成。 例如，产品的用户档案可能包括SKU和说明，而人员的用户档案则包含诸如名字、姓和电子邮件地址等信息。 您可 [!DNL Experience Platform]以通过自定义用户档案来使用与业务相关的特定数据。 标准 [!DNL Experience Data Model] (XDM)类 [!DNL XDM Individual Profile]是描述客户记录数据时构建模式的首选类，并提供平台服务之间许多交互的数据集成部分。 有关在中使用模式的更 [!DNL Experience Platform]多信息，请首先阅读XDM [系统概述](../xdm/home.md)。

### 时间系列事件

时间序列数据提供了被主体直接或间接采取行动时系统的快照，以及详细描述事件本身的数据。 由标准模式类XDM ExperienceEvent表示，时间序列数据可以描述事件，如添加到购物车的项目、被点击的链接和观看的视频。 时间序列数据可用于基于细分规则，并且事件可以在用户档案的上下文中单独访问。

### 身份

每家企业都希望以个性化的方式与客户进行沟通。 但是，为客户提供相关数字体验的一个挑战是了解如何将断开连接的数据绑定到一起，这种数据通常分布于不同的数字渠道，如平板电脑、手机和笔记本电脑。 [!DNL Identity Service] 通过将多个渠道的身份关联起来并为每个客户创建一个身份图，您可以拼凑出完整的客户图。 有关更 [多信息，请访](../identity-service/home.md) 问Identity Service概述。

### 合并策略

当将多个来源的视图片段整合在一起并合并它们，以便了解每个客户的完整时，合并策略是确定数据的优先级以及将哪些数据用于创建客户用户档案的规则。 [!DNL Platform] 当来自多个数据集的数据有冲突时，合并策略将确定如何处理该数据以及应使用哪个值。 使用REST风格的API或用户界面，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。 有关使用API处理合并策略的更 [!DNL Real-time Customer Profile] 多信息，请参阅合 [并策略端点指南](api/merge-policies.md)。 要使用UI处理合并策 [!DNL Experience Platform] 略，请参阅合 [并策略用户指南](ui/merge-policies.md)。

### 合并模式 {#profile-fragments-and-union-schemas}

其中一个关键特 [!DNL Real-time Customer Profile] 征是能够统一多渠道数据。 当用 [!DNL Real-time Customer Profile] 于访问实体时，它可以为您提供该实体跨数据集的所有用户档案片段的合并视图(称为合并视图)，并通过称为合并模式来实现。 [!DNL Real-time Customer Profile] 当实体或用户档案通过其ID访问或导出为区段时，数据会跨源合并。 要了解有关使用API访问用户档案和合并视图的更 [!DNL Real-time Customer Profile] 多信息，请访 [问实体端点指南](api/entities.md)。

### 区段

Adobe Experience Platform [!DNL Segmentation Service] 提供为个人客户提供体验所需的受众。 创建受众区段后，该区段的ID将添加到所有符合条件的用户档案的区段成员资格列表中。 区段规则是使用RESTful API和 [!DNL Real-time Customer Profile] 区段生成器用户界面构建并应用于数据的。 要了解有关分段的更多信息，请首先阅读分段 [服务概述](../segmentation/home.md)。

### (Alpha)配置计算属性

>[!IMPORTANT]
>
>计算的属性功能在alpha中。 文档和功能可能会发生变化。

通过计算属性，您可以根据其他值、计算和表达式自动计算字段的值。 计算属性在用户档案级别上操作，这意味着您可以跨所有记录和事件聚合值。 每个计算属性都包含一个表达式，即“规则”，用于评估传入的数据并将所得值存储在用户档案属性或事件中。 这些计算有助于您轻松回答与终身购买价值、购买间隔时间或应用程序打开次数等相关的问题，无需在每次需要信息时手动执行复杂的计算。 有关计算属性以及使用API使用这些属性的分步说明的更多信 [!DNL Real-time Customer Profile] 息，请参阅计 [算属性端点指南](api/computed-attributes.md)。 本指南将帮助您更好地了解计算属性在Adobe Experience Platform的作用，它包含执行基本CRUD操作的示例API调用。

## 实时组件

本节介绍可实时更 [!DNL Real-time Customer Profile] 新和监视记录和时间序列数据的组件。

### 流摄取和流细分

通过称为流摄取的过程实现实时输入。 在摄取用户档案和时间序列数据时， [!DNL Real-time Customer Profile] 在将与现有数据合并并更新合并视图之前，自动决定通过称为流分段的持续过程将数据包括或排除在细分中。 因此，在客户与您的品牌互动时，您可以即时执行计算并做出决策，为客户提供增强的个性化体验。 在摄取数据时，还会进行验证，以确保正确摄取数据并符合数据集所基于的模式。 有关获取过程中执行的验证操作的详细信息，请首先阅读数据获取 [质量概述](../ingestion/quality/overview.md)。

### 边缘投影配置和目标

为了跨多个渠道为客户实时提供协调、一致、个性化的体验，需要随时提供正确的数据，并在发生变化时不断更新。 Adobe Experience Platform通过使用所谓的边缘，实现对数据的实时访问。 边缘是一个地理上放置的服务器，它存储数据并使应用程序能够方便地访问它。 例如，Adobe应用程序(如Adobe Target和Adobe Campaign)使用边缘，以便实时提供个性化的客户体验。 数据通过投影被路由到边缘，投影目标定义要向其发送数据的边缘，投影配置定义要在边缘上提供的特定信息。 要了解更多信息并开始使用API处理 [!DNL Real-time Customer Profile] 投影，请参阅 [边缘投影端点指南](api/edge-projections.md)。

## Ingest data into [!DNL Profile]

[!DNL Platform] 可以配置为向发送记录和时间序列数据， [!DNL Profile]支持实时流摄取和批量摄取。 有关详细信息，请参阅概述如何 [向实时客户用户档案添加数据的教程](tutorials/add-profile-data.md)。

>[!NOTE]
>
>通过Adobe解决方案收集的 [!DNL Analytics Cloud]数据 [!DNL Marketing Cloud]，包括 [!DNL Advertising Cloud]、和，流 [!DNL Experience Platform] 入并被引入 [!DNL Profile]。

### [!DNL Profile] 摄取指标

可观性洞察使您能够揭示Adobe Experience Platform的关键指标。 除了各种功 [!DNL Platform] 能的使用情况统计和性能 [!DNL Platform] 指标外，还有一些特定的相关指标， [!DNL Profile]允许您深入了解传入请求率、成功摄取率、摄取的记录大小等。 要了解更多信息，请首先阅读 [Oncebility Insights API概述](../observability/api/overview.md)，然后查看完整的 [!DNL Profile] 指标列表，参阅可用 [指标文档](../observability/api/metrics.md#available-metrics)。

## [!DNL Data governance] 和 [!DNL Privacy]

[!DNL Data governance] 是用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策的一系列战略和技术。

在数据访问方面，数据管理在不同级别中起 [!DNL Experience Platform] 着关键作用：
* 数据使用标签
* 数据访问策略
* 访问控制营销行动的数据

[!DNL Data governance] 在几个点进行管理。 这包括决定引入哪些数据，以 [!DNL Platform] 及在针对特定营销操作引入哪些数据后可访问。 有关详细信息，请首先阅读数 [据治理概述](../data-governance/home.md)。

### 处理退出和数据隐私请求

[!DNL Experience Platform] 使客户能够发送与其数据在中的使用和存储相关的退出请求 [!DNL Real-time Customer Profile]。 有关如何处理退出请求的更多信息，请参阅支持退 [出请求的相关文档](../segmentation/honoring-opt-outs.md)。

## 后续步骤和其他资源

要了解有关使用的更多 [!DNL Real-time Customer Profile]信息，请阅读 [用户档案UI指南](ui/user-guide.md) 或API开 [发人员指南](api/overview.md)。

>[!WARNING]
>
>Experience Platform用户界面经常更新，自录制此视频以来可能已更改。 有关最新的UI [屏幕截图和功能，请参阅](ui/user-guide.md) “实时客户用户档案用户指南”。

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)