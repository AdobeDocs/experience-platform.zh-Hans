---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 实时客户用户档案概述
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 1%

---


# [!DNL Real-time Customer Profile]概述

Adobe Experience Platform使您能够为客户提供协调、一致和相关的体验，无论客户在何处或何时与您的品牌互动。 您 [!DNL Real-time Customer Profile]可以看到每个客户的整体视图，该渠道组合了多个的数据，包括在线、离线、CRM和第三方数据。 [!DNL Profile] 允许您将不同的客户数据整合到统一的视图中，为每次客户互动提供一个具有可操作性、时间戳记的帐户。 此概述将帮助您了解中的角色和 [!DNL Real-time Customer Profile] 使用 [!DNL Experience Platform]。

## 理解 [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] 是一个通用查找实体存储，它合并来自各种企业数据资产的数据，然后以单个客户用户档案和相关时间序列事件的形式提供对该数据的访问。 此功能使营销人员能够跨多个渠道通过受众推动协调一致的相关体验。

### [!DNL Profile] 数据存储

尽管 [!DNL Real-time Customer Profile] 处理摄取的数据并使用Adobe Experience Platform [!DNL Identity Service] 通过身份映射合并相关数据，但它会在存储中保留自己的 [!DNL Profile] 数据。 换句话说，存储 [!DNL Profile] 区与数据( [!DNL Catalog] )和[!DNL Data Lake]数据(标 [!DNL Identity Service] 识图)分开。

### [!DNL Profile] 和服 [!DNL Platform] 务

下图突出 [!DNL Real-time Customer Profile] 显示了中的 [!DNL Experience Platform] 与其他服务之间的关系：

![用户档案与其他Experience Platform服务之间的关系。](images/profile-overview/profile-in-platform.png)

### 用户档案和记录数据

用户档案是主体、组织或个人的代表，也称为记录数据。 例如，产品的用户档案可能包括SKU和说明，而人员的用户档案则包含诸如名字、姓和电子邮件地址等信息。 使 [!DNL Experience Platform]用，您可以自定义用户档案以使用与业务相关的数据类型。 标准( [!DNL Experience Data Model] XDM) [!DNL Individual Profile] 类是在描述客户记录数据时构建模式的首选类，并提供平台服务之间许多交互的数据集成。 有关在中使用模式的更 [!DNL Experience Platform]多信息，请首先阅读XDM [系统概述](../xdm/home.md)。

### 时间系列事件

时间序列数据提供了被主体直接或间接采取行动时系统的快照，以及详细描述事件本身的数据。 由标准模式类XDM ExperienceEvent表示，时间序列数据可以描述事件，如添加到购物车的项目、被点击的链接和观看的视频。 时间序列数据可用于基于细分规则，并且事件可以在用户档案的上下文中单独访问。

### 身份

每家企业都希望以个性化的方式与客户进行沟通。 但是，为客户提供相关数字体验的一个挑战是了解如何将断开连接的数据绑定到一起，这种数据通常分布于不同的数字渠道，如平板电脑、手机和笔记本电脑。 [!DNL Identity Service] 通过将多个渠道的身份关联起来，为每个客户创建一个身份图，让您能够更好地了解客户，从而将客户的全貌拼凑在一起。 有关更 [多信息，请访](../identity-service/home.md) 问Identity Service概述。

### 区段

Adobe Experience Platform [!DNL Segmentation Service] 可以创造受众，为每位客户提供强大的体验。 创建受众区段后，该区段的ID将添加到所有符合条件的用户档案的区段成员资格列表中。 区段规则是使用RESTful API和 [!DNL Real-time Customer Profile] 区段生成器用户界面构建并应用于数据的。 要了解有关分段的更多信息，请首先阅读分段 [服务概述](../segmentation/home.md)。

### 用户档案片段和合并模式 {#profile-fragments-and-union-schemas}

其中一个关键特 [!DNL Real-time Customer Profile] 征是能够统一多渠道数据。 当用 [!DNL Real-time Customer Profile] 于访问实体时，它可以为您提供该实体跨数据集的所有用户档案片段的合并视图(称为合并视图)，并通过称为合并模式来实现。 [!DNL Real-time Customer Profile] 当实体或用户档案通过其ID访问或导出为区段时，数据会跨源合并。 要了解有关使用API访问用户档案和合并视图的更 [!DNL Real-time Customer Profile] 多信息，请访 [问实体端点指南](api/entities.md)。

### 合并策略

当整合多个来源的视图并合并这些数据以便了解每个客户的完整时，合并策略是确定数据的优先级和合并哪些数据以创建统一视图的规则。 [!DNL Platform] 使用REST风格的API或用户界面，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。 有关使用API处理合并策略的更 [!DNL Real-time Customer Profile] 多信息，请参阅合 [并策略端点指南](api/merge-policies.md)。 要使用UI处理合并策 [!DNL Experience Platform] 略，请参阅合 [并策略用户指南](ui/merge-policies.md)。

### (Alpha)配置计算属性

>[!IMPORTANT]
>此文档中概述的计算属性功能在alpha中。 文档和功能可能会发生变化。

通过计算属性，您可以根据其他值、计算和表达式自动计算字段的值。 计算属性在用户档案级别上操作，这意味着您可以跨所有记录和事件聚合值。 每个计算属性都包含一个表达式，即“规则”，用于评估传入的数据，并将结果值存储在用户档案属性或事件中。 这些计算有助于您轻松回答与终身购买价值、购买间隔时间或应用程序打开次数等相关的问题，无需在每次需要信息时手动执行复杂的计算。 有关计算属性以及使用API使用这些属性的分步说明的更多信 [!DNL Real-time Customer Profile] 息，请参阅计 [算属性端点指南](api/computed-attributes.md)。 本指南将帮助您更好地了解计算属性在Adobe Experience Platform中所起的作用，它包含执行基本CRUD操作的示例API调用。

## 实时组件

本节介绍可实时更 [!DNL Real-time Customer Profile] 新和监视记录和时间序列数据的组件。

### 流摄取和流细分

通过称为流摄取的过程实现实时输入。 在摄取用户档案和时间序列数据时， [!DNL Real-time Customer Profile] 在将与现有数据合并并更新合并视图之前，自动决定通过称为流分段的持续过程将数据包括或排除在细分中。 因此，在客户与您的品牌互动时，您可以即时执行计算并做出决策，为客户提供增强的个性化体验。 在摄取数据时，还会进行验证，以确保正确摄取数据并符合数据集所基于的模式。 有关获取过程中执行的验证操作的详细信息，请首先阅读数据获取 [质量概述](../ingestion/quality/overview.md)。

### 边缘投影配置和目标

为了跨多个渠道为客户实时提供协调、一致、个性化的体验，需要随时提供正确的数据，并在发生变化时不断更新。 Adobe Experience Platform通过使用所谓的边缘实现对数据的实时访问。 边缘是一个地理上放置的服务器，它存储数据并使应用程序能够方便地访问它。 例如，Adobe Target和Adobe Campaign等Adobe应用程序使用边缘来实时提供个性化的客户体验。 数据通过投影被路由到边缘，投影目标定义要向其发送数据的边缘，投影配置定义要在边缘上提供的特定信息。 要了解更多信息并开始使用API处理 [!DNL Real-time Customer Profile] 投影，请参阅 [边缘投影端点指南](api/edge-projections.md)。

## 将数据添加到 [!DNL Real-time Customer Profile]

[!DNL Platform] 可以配置为将记录和时间序列数据发送到 [!DNL Profile]，支持实时流摄取和批量摄取。 有关详细信息，请参阅概述如何 [向实时客户用户档案添加数据的教程](tutorials/add-profile-data.md)。

>[!Note]
>通过Adobe解决方案收集的 [!DNL Analytics Cloud]数据， [!DNL Marketing Cloud]包括 [!DNL Advertising Cloud]、和，流 [!DNL Experience Platform] 入并被引入 [!DNL Profile]。

### [!DNL Profile] 摄取指标

可观性洞察使您能够揭示Adobe Experience Platform中的关键指标。 除了各种功 [!DNL Platform] 能的使用情况统计和性能 [!DNL Platform] 指标外，还有一些特定的相关指标， [!DNL Profile]允许您深入了解传入请求率、成功摄取率、摄取的记录大小等。 要了解更多信息，请首先阅读可观 [性洞察概述](../observability/home.md)，然后查看完整的指标 [!DNL Profile] 列表，参阅可用指标 [的相关文档](../observability/metrics.md)。

## [!DNL Data governance] 和 [!DNL Privacy]

[!DNL Data governance] 是用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策的一系列战略和技术。

在数据访问方面，数据管理在不同级别中起 [!DNL Experience Platform] 着关键作用：
* 数据使用标签
* 数据访问策略
* 访问控制营销行动的数据

[!DNL Data governance] 在几个点进行管理。 这包括决定引入哪些数据，以 [!DNL Platform] 及在针对特定营销操作引入哪些数据后可访问。 有关详细信息，请首先阅读数 [据治理概述](../data-governance/home.md)。

### 处理退出和数据隐私请求

[!DNL Experience Platform] 使客户能够发送与其数据在中的使用和存储相关的退出请求 [!DNL Real-time Customer Profile]。 有关如何处理退出请求的更多信息，请参阅支持退 [出请求的相关文档](../segmentation/honoring-opt-outs.md)。

## [!DNL Profile] 准则

[!DNL Experience Platform] 有一系列的指导方针，以便有效地使用 [!DNL Profile]。

| 区域 | 边界 |
| ------- | -------- |
| [!DNL Profile] 合并模式 | 最多20个 **数据集** 可以贡献于 [!DNL Profile] 合并模式。 |
| 多实体关系 | 最多可 **创建** 5个多实体关系。 |
| 多实体关联的JSON深度 | JSON的最大深度为 **4**。 |
| 时间序列数据 | 非人员实体 **不** 允 [!DNL Profile] 许使用时间序列数据。 |
| 非人模式关系 | 不允许非人模式 **关系** 。 |
| 用户档案片段 | 建议的用户档案片段最大大小 **为10kB**。<br><br> 用户档案片段的绝对最大大 **小为1MB**。 |
| 非人员实体 | 单个非人员实体的最大总大小 **为200MB**。 |
| 每个非人实体的数据集 | 最多可以 **将** 1个数据集关联到非人员实体。 |

<!--
| Section | Boundary | Enforcement |
| ------- | -------- | ----------- |
| Profile union schema | A maximum of **20** datasets can contribute to the Profile union schema. | A message stating you've reached the maximum number of datasets appears. You must either disable or clean up other obsolete datasets in order to create a new dataset. |
| Multi-entity relationships | A maximum of **5** multi-entity relationship can be created. | A message stating all available mappings have been used appears when the fifth relationship is mapped. An error message letting you know you have exceeded the number of available mappings appears when attempting to map a sixth relationship. | 
| JSON depth for multi-entity association | The maximum JSON depth is **4**. | When trying to use the relationship selector with a field that is more than four levels deep, an error message appears, stating it is ineligible for multi-entity association. |
| Time series data | Time-series data is **not** permitted in Profile for non-people entities. | A message stating that this data cannot be enabled for Profile because it is of an unsupported type appears. |
| Non-people schema relationships | Non-people schema relationships are **not** permitted. | Relationships between two non-people schemas cannot be created. The relationships checkbox will be disabled. |
| Profile fragment | The recommended maximum size of a profile fragment is **10kB**.<br><br> The absolute maximum size of a profile fragment is **1MB**. | If you upload a fragment that is larger than 10kB, a warning appears, stating that performance may be degraded since the fragment exceeds the recommended maximum working size.<br><br> If you upload a fragment that is larger than 1MB, ingestion will fail, and an alert letting you know that records have failed will be sent. |
| Non-person entity | The maximum total size for a single non-person entity is **200MB**. | If you load an object as a non-person entity that is larger than 200MB, an alert will appear, stating that the entity has exceeded the maximum allowable size and will not be useable for segmentation. |
| Datasets per non-person entity | A maximum of **1** dataset can be associated to a non-person entity. | If you try to create a second dataset that is associated to the same non-person entity, an error appears, stating that only one dataset can be active per non-person entity. |

--->

>[!NOTE]
>
>
>非人员实体引用不属于的任何 **XDM** 类 [!DNL Profile]。

## 后续步骤和其他资源

要了解更多相 [!DNL Real-time Customer Profile]关信息，请继续阅读文档，并通过观看以下视频或浏览其他Experience Platform视频教程来补充您 [的学习内容](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html)。

>[!WARNING]
>以 [!DNL Platform] 下视频中显示的UI已过期。 有关最新的UI [屏幕截图和功能，请参阅](ui/user-guide.md) “实时客户用户档案用户指南”。

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)