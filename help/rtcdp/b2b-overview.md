---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform；实时客户数据平台；实时CDP;b2b;CDP；客户AI
title: Real-time CDP B2B Edition概述
seo-title: Real-time Customer Data Platform B2B Edition overview
description: Real-time Customer Data Platform B2B版帐户概述
seo-description: Overview of Real-time Customer Data Platform B2B Edition Account
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: 6b582683483046efaf880e46e33d7f30a44a61bf
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 1%

---

# Real-time Customer Data Platform B2B版概述

>[!IMPORTANT]
>
>Real-time CDP B2B Edition目前处于测试阶段。 文档和功能可能会发生变化。

Real-time CDP B2B Edition构建于Real-time Customer Data Platform(Real-time CDP)之上，专为在业务到业务服务模型中运营的营销人员而构建。 它将来自多个来源的数据整合在一起，并将其整合为人员和帐户配置文件的单一视图。 通过这种统一的数据，营销人员可以准确定位特定受众并在所有可用渠道中吸引这些受众。

对各种Adobe Experience Platform功能进行了改进，这些功能区分了Real-time CDP B2B Edition与B2C Edition。 这些功能包括对B2B用例的体验数据模型(XDM)进行了改进、对身份分辨率和配置文件分段进行了升级，以及为[!DNL Marketo Engage]构建的自定义连接器和目标。 [!DNL Marketo]连接器允许B2B品牌将其行业领先的B2B参与数据与行为信息连接起来，以培养潜在客户并增强基于帐户的营销操作。

通过Real-time CDP B2B Edition，您可以：

* 将从多个来源收集的数据合并到一个视图中，以创建全面的人员和帐户配置文件。
* 从统一帐户配置文件的集中存储中丰富、划分和导出所有跨源数据。
* 使用集中化流程每个步骤都提供的数据管理工具来管理您的数据，以确保您的数据符合法律法规和业务策略。

有关Real-time CDP B2B Edition改进的更全面的详细信息，请参阅以下各节。

## XDM

Real-time CDP B2B Edition提供了几个新的XDM模式类、字段组和关系类型，用于捕获和构建专门用于B2B的数据。 有关这些增强功能的细目，请参阅实时CDP B2B版本](./schemas/b2b.md)中的[XDM概述。

通过使用预配置的B2B模式，您可以以标准化、可操作的结构导入数据。 许多新架构类几乎直接映射到主流CRM中遇到的类，例如[!DNL Salesforce]、[!DNL Microsoft Dynamics]、[!DNL Marketo]和其他B2B数据源。 借助Real-time CDP B2B Edition ，您可以以简单的方式将数据从B2B源引入平台，并且结果易于审核。

通过这些XDM增强功能，您可以通过以B2B为中心的源和目标更好地摄取和激活数据，从而为更多各种灵活的用例改进数据统一和呈现方式。

## 身份解析

在定义了架构并摄取了符合这些架构的数据后，实时CDP B2B版通过功能强大的实时身份解析系统来识别代表真实世界人员和企业的源记录。

身份解析系统提供以下功能：

* B2B和B2C人员合并记录
* 多级帐户层次结构
* 多对多、人员到帐户连接
* 人员和帐户身份可实时解决

身份解决系统已得到扩大，以支持更多层面的人员分类。 该系统允许人们被识别为商机中的商机和客户。

由源CRM同步并通过系统内多个路径连接的帐户记录由Platform合并在一起。 该系统将那些与业务机会相关的人员和那些记录为客户的人员汇集在一起，但如果他们是可识别的，也能将他们作为一种属性加以区分。

匹配标识符用于链接在一起并合并来自多个系统的帐户记录。 在此过程中，帐户层次结构将保留。 使用不同点来仔细检查某个人是否与某个帐户相关，并在需要时提供将其与帐户分离的功能。

## 用户档案和分段

实时CDP B2B Edition引入与人员、公司、属性和行为相关的数据并解析身份后，该数据便可用于构建用户档案。 然后，这些用户档案可分段为可浏览的受众，这些受众随后可以激活到各种目标。

正确实施后，系统会使用唯一的主标识符来跟踪人员，而不是使用可能发生更改的属性（如电子邮件地址）来跟踪人员。 这意味着当有人更改作业时，系统仍会跟踪这些作业。 该人员仍是同一实体，但却与新帐户相关联。 此本机功能为扩展到新帐户提供了强大的矢量，因为系统会遵循这些人员作为个人，包括其所有属性和行为。

## B2B源

Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 [!DNL Marketo]源允许您将B2B数据流式传输到平台，并使用与平台连接的应用程序保持此数据的最新。 它支持任意数量的[!DNL Marketo]实例（这对具有多个实例的大型公司有利），并提取到合并数据的单个IMS组织中。

>[!NOTE]
>
>[!DNL Marketo]源是使用实时CDP B2B Edition所需的&#x200B;**不**。

有关Marketo和将B2B数据引入平台的更多信息，请参阅Real-time CDP B2B Edition](./sources/b2b.md)中的[源文档。

## B2B目标

Experience Platform目标(如Google、Linkedin和Facebook)可用，并且完全受实时CDP B2B Edition支持。 还有一个Marketo Engage目标，用于从平台中流式传输区段成员资格数据，并将其作为列表在Marketo中提供。

对于具有多个CRM的公司，Real-time CDP B2B Edition提供了配置目标连接器以分隔Marketo或CRM实例的选项。 如果需要，您可以将目标连接器配置到每个实例，并单独将受众发送到每个CRM实例。

## 后续步骤

现在，您可以更好地了解Real-time CDP B2B Edition为营销人员带来的好处，以及它与Real-time CDP之间的差异，接下来就可以了解如何将这些功能应用于您自己的IMS组织。

要了解Real-time CDP B2B Edition如何使您的业务对业务服务模型受益，请参阅[Real-time CDP B2B Edition](./b2b-use-case.md)的示例用例。 或者，您也可以参阅Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)中的[架构文档，以获取有关创建架构和定义基本B2B数据实体关系的更多具体指导。
