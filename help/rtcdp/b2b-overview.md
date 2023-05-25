---
keywords: RTCDP；CDP；B2B版本；Real-time Customer Data Platform；实时客户数据平台；real time cdp；b2b；cdp；客户人工智能
title: Real-Time CDP B2B版本概述
description: Real-Time Customer Data Platform B2B 版本帐户概述
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 1%

---

# Real-time Customer Data Platform B2B版本概述

Real-Time CDP B2B版构建于Adobe Real-time Customer Data Platform (Real-Time CDP)之上，专为以B2B服务模式运营的营销人员而构建。 它将来自多个来源的数据整合在一起，并将其合并到人员和帐户配置文件的单一视图中。 此统一数据允许营销人员准确地定位特定受众，并在所有可用渠道中吸引这些受众。

多项Adobe Experience Platform功能都得到了改进，从而将Real-Time CDP B2B版本与其对应的B2C版本区分开来。 这些改进包括改进了用于B2B用例的体验数据模型(XDM)，升级了身份解析和配置文件分段，以及针对以下对象的自定义构建的连接器和目标 [!DNL Marketo Engage]. 此 [!DNL Marketo] 连接器允许B2B品牌将其行业领先的B2B参与数据与行为信息连接起来，以培育潜在客户并加强基于帐户的营销操作。

使用Real-Time CDP B2B版本，您可以：

* 将从多个来源收集的数据合并到单个视图中，以创建全面的用户和帐户配置文件。
* 从统一帐户配置文件的集中存储中扩充、分段和导出所有跨源数据。
* 使用可在集中化过程的每个步骤中使用的数据治理工具来管理您的数据，以确保您的数据符合法律法规和业务策略。

有关Real-Time CDP B2B版本改进的更全面的详细信息分为以下部分。

## XDM

Real-Time CDP B2B版本提供了几个新的XDM架构类、字段组和关系类型，以专门为B2B目的捕获和构建数据。 请参阅概述，位于 [Real-Time CDP B2B版本中的XDM](./schemas/b2b.md) 以了解每个增强功能的细目。

通过使用预配置的B2B架构，您可以引入标准化可操作结构的数据。 许多新的架构类几乎直接映射到主流CRM中遇到的架构类，例如 [!DNL Salesforce]， [!DNL Microsoft Dynamics]， [!DNL Marketo]和其他B2B数据源。 借助Real-Time CDP B2B版本，您可以直接将数据从B2B源引入平台，并生成易于审核的结果。

这些XDM增强功能允许您通过以B2B为中心的源和目标更好地摄取和激活数据，从而改进数据统一和呈现，以实现更多样化和灵活的用例。

## 身份解析

定义架构并摄取符合这些架构的数据后，Real-Time CDP B2B Edition通过功能强大的实时身份解析系统识别代表真实世界人员和企业的源记录。

身份解析系统提供以下功能：

* 合并的B2B和B2C人员记录
* 多级帐户层次结构
* 多对多、人员到帐户连接
* 实时解析人员和帐户身份

身份解析系统已得到扩展，以支持更加多方面的人员分类。 该系统允许将人们识别为商业机会中的潜在客户以及客户。

由源CRM同步并通过系统内的多个路径连接的帐户记录由Platform合并在一起。 该系统将与业务机会相关的人员和记录为客户的人员，但如果他们可识别，则还能够保留他们之间的区别作为属性。

匹配标识符用于链接在一起并合并来自多个系统的帐户记录。 在整个过程中，帐户层次结构都会被保留。 区分条件用于详细检查人员是否与帐户关联，并提供在需要时将其与帐户区分开的功能。

## 用户档案和分段

一旦Real-Time CDP B2B Edition摄取了数据并解决了与人员、公司、属性和行为相关的身份信息，该数据就会用于构建用户档案。 然后，可以将这些配置文件分段为可浏览的受众，这些受众随后可以激活到各种目标。

正确实施后，系统将使用唯一的主要标识符而不是可更改的属性（如电子邮件地址）来跟踪人员。 这意味着，当有人更改工作时，系统仍会跟踪他们。 人员仍然是同一实体，但他们链接到新帐户。 此本机功能为向新客户扩展提供了很好的媒介，因为系统以包括他们所有属性和行为的个人身份跟踪这些人员。

## B2B源

Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 此 [!DNL Marketo] 通过source，可将B2B数据流式传输到Platform，并使用与平台连接的应用程序使这些数据保持最新。 它支持任意数量的实例 [!DNL Marketo] （这对拥有多个实例的大型公司很有用），并将数据提取到合并数据的单个组织中。

>[!NOTE]
>
>此 [!DNL Marketo] 源是 **非** 需要才能使用Real-Time CDP B2B版本。

请参阅 [Real-Time CDP B2B版本中的源](./sources/b2b.md) 文档，以了解有关Marketo和将B2B数据引入平台的更多信息。

## B2B目标

Google Customer Match、Facebook、LinkedIn、Marketo Engage、Amazon S3、Google Display &amp; Video 360、Google Ads和Google Ad Manager等Experience Platform目标均由Real-Time CDP B2B Edition提供和完全支持。 Marketo Engage目标还会通过Platform流式传输区段成员资格数据，并将其作为Marketo中的列表提供。

请参见 [Marketo Engage目标](../destinations/catalog/adobe/marketo-engage.md) 了解更多信息。

对于拥有多个CRM的公司，Real-Time CDP B2B版本提供了将目标连接器配置为单独的Marketo或CRM实例的选项。 如果需要，您可以为每个实例配置目标连接器，并单独将受众发送到每个CRM实例。

## 后续步骤

现在，您已更好地了解Real-Time CDP B2B版本为营销人员提供的好处以及它与Real-Time CDP之间的差异，您可以了解如何将这些功能应用于您自己的组织。

要了解Real-Time CDP B2B版本如何使您的企业到企业服务模式受益，请参阅以下文档以帮助您入门：

* [Real-Time CDP B2B版本的示例用例](./b2b-use-case.md)
* [Real-time Customer Data Platform B2B版本的端到端教程](./b2b-tutorial.md)
* [如何摄取数据](./sources/b2b.md)
* [如何访问用户档案](./profile/profile-overview.md)
* [Real-time Customer Data Platform B2B版本中的架构](./schemas/b2b.md)
* [如何构建区段](./segmentation/b2b.md)
* [如何将区段激活到目标](./destinations/b2b.md)
* [如何定义和执行数据治理策略](./privacy/data-governance-overview.md)
