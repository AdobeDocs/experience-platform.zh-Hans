---
keywords: RTCDP；CDP；B2B edition；Real-Time Customer Data Platform；实时客户数据平台；real time cdp；b2b；cdp；客户人工智能
title: Real-Time CDP B2B edition概述
description: Real-Time Customer Data Platform B2B 版本帐户概述
feature: Get Started, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 4%

---

# Real-Time Customer Data Platform B2B edition概述

Real-Time CDP B2B edition构建于Adobe Real-Time Customer Data Platform (Real-Time CDP)之上，专为以B2B服务模式运营的营销人员而构建。 它将来自多个来源的数据汇集在一起&#x200B;，并将其组合成人员和帐户轮廓的单一视图。这种统一的数据使营销人员能够精确锁定特定受众，并通过所有可用渠道吸引这些受众。

Adobe Experience Platform的各项功能都有改进，可将Real-Time CDP B2B edition与其B2C对应功能区分开来。 其中包括对B2B用例的Experience Data Model (XDM)的改进、对身份解析和配置文件分段的升级，以及针对[!DNL Marketo Engage]的自定义构建连接器和目标。 [!DNL Marketo]连接器允许B2B品牌将其行业领先的B2B参与数据与行为信息连接起来，以培育潜在客户并加强基于帐户的营销运营。

通过Real-Time CDP B2B edition，您可以：

* 将从多个来源收集的数据合并到单个视图中，以创建全面的用户和帐户配置文件。
* 扩充、分段和导出统一帐户配置文件的集中存储中的所有跨源数据。
* 使用可在集中流程的每个步骤中使用的数据治理工具来管理您的数据，以确保您的数据符合法律法规和业务策略。

有关Real-Time CDP B2B edition改进功能的更全面详细信息分为以下部分。

## XDM

Real-Time CDP B2B edition提供了多个新的XDM架构类、字段组和关系类型，用于专门为B2B目的捕获和构建数据。 有关每个增强功能的细目，请参阅Real-Time CDP B2B edition[中有关](./schemas/b2b.md)XDM的概述。

通过使用预配置的B2B架构，您可以采用标准化、可操作的结构引入数据。 许多新架构类几乎直接映射到主流CRM中遇到的那些类，如[!DNL Salesforce]、[!DNL Microsoft Dynamics]、[!DNL Marketo]和其他B2B数据源。 借助Real-Time CDP B2B edition，您可以采用一种简单明了的方式将数据从B2B来源引入Experience Platform，其结果易于审核。

这些XDM增强功能允许您通过以B2B为中心的源和目标更好地摄取和激活数据，从而改进数据统一和呈现，以实现更多样化和灵活的用例。

## 身份解析

在定义架构并摄取符合这些架构的数据后，Real-Time CDP B2B edition通过强大的实时身份解析系统识别代表现实世界人员和企业的源记录。

身份解析系统提供以下功能：

* 合并的B2B和B2C人员记录
* 多级帐户层次结构
* 多对多、人员到帐户连接
* 实时解析人员和帐户身份

身份解析系统已得到扩展，以支持更加多方面的人员分类。 系统允许将人员识别为商业机会中的潜在客户以及客户。

由源CRM同步并通过系统中的多个路径连接的帐户记录由Experience Platform合并在一起。 该系统将与业务机会相关的人员和记录为客户的人员，但如果可识别，则还能够将他们之间的区别保留为属性。

匹配标识符用于链接在一起并合并来自多个系统的帐户记录。 在整个过程中将保留帐户层次结构。 差异化功能用于审查人员是否与帐户关联，并提供在需要时将其与帐户分离的功能。

## 用户档案和分段

一旦Real-Time CDP B2B edition摄取了数据并解决了与人员、公司、属性和行为相关的身份信息，该数据就会用于构建用户档案。 然后，这些配置文件可以划分为可浏览的受众，这些受众随后可以激活到各种目标。

正确实施后，系统将使用唯一的主要标识符而不是可更改的属性（如电子邮件地址）来跟踪人员。 这意味着，当有人更换工作时，系统仍会跟踪他们。 此人仍然是同一实体，但他们已链接到新帐户。 此本机功能为扩展到新帐户提供了很好的载体，因为系统以包括他们所有属性和行为的个人身份跟踪这些人员。

## B2B源

Experience Platform允许从外部源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。 [!DNL Marketo]源允许您将B2B数据流式传输到Experience Platform中，并使用与Experience Platform连接的应用程序使这些数据保持最新。 它支持[!DNL Marketo]的任意数量的实例（这对具有多个实例的大型公司有利），并拉入合并数据的单个组织。

>[!NOTE]
>
>[!DNL Marketo]源是&#x200B;**不需要**&#x200B;才能使用Real-Time CDP B2B edition。

有关Real-Time CDP以及将B2B数据引入Experience Platform的更多信息，请参阅Marketo B2B edition中的[源](./sources/b2b.md)文档。

## B2B目标

Experience Platform目标(如Google Customer Match、Facebook、LinkedIn、Marketo Engage、Amazon S3、Google Display &amp; Video 360、Google Ads和Google Ad Manager)可用，并由Real-Time CDP B2B edition提供完全支持。 Marketo Engage目标还通过Experience Platform流式传输区段成员资格数据，并将其作为Marketo中的列表提供。

有关详细信息，请参阅[Marketo Engage目标](../destinations/catalog/adobe/marketo-engage.md)的概述。

对于拥有多个CRM的公司，Real-Time CDP B2B edition提供将目标连接器配置为单独的Marketo或CRM实例的选项。 如果需要，您可以为每个实例配置目标连接器，并单独将受众发送到每个CRM实例。

## 后续步骤

现在，您已更好地了解Real-Time CDP B2B edition为营销人员提供的好处以及它与Real-Time CDP之间的差异，您可以了解如何将这些功能应用于您自己的组织。

要了解Real-Time CDP B2B edition如何使您的企业到企业服务模式受益，请参阅以下文档以帮助您入门：

* [Real-Time CDP B2B edition的示例用例](./b2b-use-case.md)
* [Real-Time Customer Data Platform B2B edition的端到端教程](./b2b-tutorial.md)
* [如何摄取数据](./sources/b2b.md)
* [如何访问用户档案](./profile/profile-overview.md)
* [Real-Time Customer Data Platform B2B edition中的架构](./schemas/b2b.md)
* [如何构建受众](./segmentation/b2b.md)
* [如何将受众激活到目标](./destinations/b2b.md)
* [如何定义和执行数据治理策略](./privacy/data-governance-overview.md)
