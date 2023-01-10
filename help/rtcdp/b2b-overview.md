---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform；实时客户数据平台；实时CDP;b2b;CDP；客户AI
title: Real-Time CDP B2B版概述
description: Real-Time Customer Data Platform B2B 版本帐户概述
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 1%

---

# Real-time Customer Data Platform B2B版概述

Real-Time CDP B2B Edition基于Adobe Real-time Customer Data Platform(Real-Time CDP)而构建，专为以企业对企业服务模式运营的营销人员而构建。 它将来自多个来源的数据整合在一起，并将其整合为人员和帐户配置文件的单一视图。 通过这种统一的数据，营销人员可以准确定位特定受众并在所有可用渠道中吸引这些受众。

Real-Time CDP B2B Edition与其B2C版本相比，Adobe Experience Platform的各种功能都有所改进。 这些功能包括对B2B用例的体验数据模型(XDM)进行了改进、对身份分辨率和配置文件分段进行了升级，以及自定义的连接器和目标 [!DNL Marketo Engage]. 的 [!DNL Marketo] 连接器允许B2B品牌将其行业领先的B2B参与数据与行为信息连接起来，以培养潜在客户并增强基于帐户的营销操作。

使用Real-Time CDP B2B Edition，您可以：

* 将从多个来源收集的数据合并到一个视图中，以创建全面的人员和帐户配置文件。
* 从统一帐户配置文件的集中存储中丰富、划分和导出所有跨源数据。
* 使用集中化流程每个步骤都提供的数据管理工具来管理您的数据，以确保您的数据符合法律法规和业务策略。

有关Real-Time CDP B2B Edition改进的更全面详细信息，请参阅以下各节。

## XDM

Real-Time CDP B2B Edition提供了多个新的XDM模式类、字段组和关系类型，用于捕获和构建专门用于B2B的数据。 请参阅 [Real-Time CDP B2B版中的XDM](./schemas/b2b.md) 以细分这些增强功能。

通过使用预配置的B2B模式，您可以以标准化、可操作的结构导入数据。 许多新架构类几乎直接映射到主流CRM中遇到的类，例如 [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo]、和其他B2B数据源。 借助Real-Time CDP B2B Edition，您可以以简单的方式将数据从B2B源导入平台，并且结果易于审核。

通过这些XDM增强功能，您可以通过以B2B为中心的源和目标更好地摄取和激活数据，从而为更多各种灵活的用例改进数据统一和呈现方式。

## 身份解析

在定义了架构并摄取了符合这些架构的数据后，Real-Time CDP B2B Edition通过功能强大的实时身份解析系统来识别代表真实人员和企业的源记录。

身份解析系统提供以下功能：

* B2B和B2C人员合并记录
* 多级帐户层次结构
* 多对多、人员到帐户连接
* 人员和帐户身份可实时解决

身份解决系统已得到扩大，以支持更多层面的人员分类。 该系统允许人们被识别为商机中的商机和客户。

由源CRM同步并通过系统内多个路径连接的帐户记录由Platform合并在一起。 该系统将那些与业务机会相关的人员和那些记录为客户的人员汇集在一起，但如果他们是可识别的，也能将他们作为一种属性加以区分。

匹配标识符用于链接在一起并合并来自多个系统的帐户记录。 在此过程中，帐户层次结构将保留。 使用不同点来仔细检查某个人是否与某个帐户相关，并在需要时提供将其与帐户分离的功能。

## 用户档案和分段

Real-Time CDP B2B版引入与人员、公司、属性和行为相关的数据和已解析的身份后，该数据将用于构建用户档案。 然后，这些用户档案可分段为可浏览的受众，这些受众随后可以激活到各种目标。

正确实施后，系统会使用唯一的主标识符来跟踪人员，而不是使用可能发生更改的属性（如电子邮件地址）来跟踪人员。 这意味着当有人更改作业时，系统仍会跟踪这些作业。 该人员仍是同一实体，但却与新帐户相关联。 此本机功能为扩展到新帐户提供了强大的矢量，因为系统会遵循这些人员作为个人，包括其所有属性和行为。

## B2B源

Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 的 [!DNL Marketo] 源允许您将B2B数据流式传输到平台，并使用与平台连接的应用程序保持此数据为最新。 它支持任意数量的 [!DNL Marketo] （对具有多个实例的大型公司有利）并提取到合并数据的单个IMS组织。

>[!NOTE]
>
>的 [!DNL Marketo] 源 **not** 使用Real-Time CDP B2B Edition时需要。

请参阅 [Real-Time CDP B2B版中的源](./sources/b2b.md) 文档，以了解有关Marketo和将B2B数据引入平台的更多信息。

## B2B目标

Experience Platform目标(如Google客户匹配、Facebook、LinkedIn、Marketo Engage、Amazon S3、Google Display &amp; Video 360、Google Ads和Google Ad Manager)均可用，并且Real-Time CDP B2B Edition完全支持这些目标。 Marketo Engage目标还会将区段成员资格数据流式传输到平台之外，并在Marketo中作为列表提供。

请参阅 [Marketo Engage目标](../destinations/catalog/adobe/marketo-engage.md) 以了解更多信息。

对于具有多个CRM的公司，Real-Time CDP B2B Edition提供了配置目标连接器以分隔Marketo或CRM实例的选项。 如果需要，您可以将目标连接器配置到每个实例，并单独将受众发送到每个CRM实例。

## 后续步骤

现在，您已更好地了解Real-Time CDP B2B Edition为营销人员带来的好处，以及它与Real-Time CDP之间的差异，接下来可以了解如何将这些功能应用于您自己的IMS组织。

要了解Real-Time CDP B2B Edition如何使您的企业对企业服务模式受益，请参阅以下文档以帮助您入门：

* [Real-Time CDP B2B Edition的示例用例](./b2b-use-case.md)
* [Real-time Customer Data Platform B2B版的端到端教程](./b2b-tutorial.md)
* [如何摄取数据](./sources/b2b.md)
* [如何访问用户档案](./profile/profile-overview.md)
* [Real-time Customer Data Platform B2B版中的模式](./schemas/b2b.md)
* [如何构建区段](./segmentation/b2b.md)
* [如何将区段激活到目标](./destinations/b2b.md)
* [如何定义和实施数据管理策略](./privacy/data-governance-overview.md)
