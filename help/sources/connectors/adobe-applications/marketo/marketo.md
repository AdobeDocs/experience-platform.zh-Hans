---
keywords: Experience Platform；主页；热门主题；Marketo Engage；marketo engage；marketo
solution: Experience Platform
title: Marketo Engage连接器
description: 本文档提供了Marketo Engage源连接器的概述，包括有关其身份验证、映射和数据延迟的信息。
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# [!DNL Marketo Engage]连接器

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

[[!DNL Marketo Engage]](https://www.marketo.com/software/)是一个完整的解决方案，面向希望通过参与复杂购买历程的每个阶段来转变客户体验的潜在客户管理人员和B2B营销人员。

使用[!DNL Marketo Engage]源连接器，您可以将B2B数据从[!DNL Marketo Engage]引入到Platform，并使用与平台连接的应用程序使这些数据保持最新。

>[!IMPORTANT]
>
>您必须有权访问[Adobe Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md)，才能将所有Marketo数据集与[实时客户个人资料](../../../../profile/home.md)一起用于分段。 如果没有Real-Time CDP B2B版本，您仍可以使用Marketo源将人员和活动数据集中的数据引入Real-time Customer Profile以进行分段。

本文档提供了[!DNL Marketo Engage]源连接器的概述，包括有关如何对连接器进行身份验证、如何将[!DNL Marketo Engage]字段映射到体验数据模型(XDM)以及连接器的数据延迟的信息。

## 设置Adobe组织映射

在为[!DNL Marketo Engage]建立映射集之前，必须先设置Adobe组织映射。 有关如何完成此操作的详细步骤，请参阅[为 [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html)设置Adobe组织映射指南。

## 验证您的[!DNL Marketo Engage]连接器

为了将[!DNL Marketo Engage]连接到Platform，您必须首先检索`munchkinId`、`clientId`和`clientSecret`的值。

请参阅[对Marketo源连接器进行身份验证](./marketo-auth.md)文档中概述的步骤，以检索您的凭据。

## 设置B2B命名空间和模式自动生成实用程序

接下来，使用B2B命名空间和架构自动生成实用程序来设置您的Platform开发人员控制台和Postman环境。 这允许您自动填充B2B命名空间和架构。 有关详细说明，请参阅[设置B2B命名空间和架构自动生成实用程序的指南](./marketo-namespaces.md)

## Experience Data Model (XDM)

XDM是一个公开记录的规范，它提供了通用结构和定义，允许您从第三方源摄取数据以用于下游平台服务。

遵守XDM标准允许将数据统一纳入平台生态系统，从而更轻松地提供数据和收集信息。

要了解有关XDM及其在Platform中的角色的更多信息，请参阅[XDM系统概述](../../../../xdm/home.md)。

## 从[!DNL Marketo Engage]到XDM的字段映射

要建立[!DNL Marketo Engage]与Platform之间的源连接，在引入Platform之前，必须将Marketo源数据字段映射到其相应的目标XDM字段。

有关[!DNL Marketo Engage]数据集与Platform之间的字段映射规则的详细信息，请参阅以下内容：

* [活动](../mapping/marketo.md#activities)
* [项目](../mapping/marketo.md#programs)
* [计划成员资格](../mapping/marketo.md#program-memberships)
* [公司](../mapping/marketo.md#companies)
* [静态列表](../mapping/marketo.md#static-lists)
* [静态列表成员资格](../mapping/marketo.md#static-list-memberships)
* [指定帐户](../mapping/marketo.md#named-accounts)
* [机会](../mapping/marketo.md#opportunities)
* [机会联系人角色](../mapping/marketo.md#opportunity-contact-roles)
* [人员](../mapping/marketo.md#persons)

## Platform上[!DNL Marketo Engage]数据的预期延迟

下表根据摄取的性质和所需目标，概述了将[!DNL Marketo Engage]数据引入Platform的预期延迟：

| 目标 | 预期延迟 |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10分钟 |
| 数据湖 | &lt; 60分钟 |

>[!NOTE]
>
>以上延迟数字代表了95%置信水平的预期。 实际延迟时间将有所不同，在极少数情况下可能会超出这些数字50%。

## 后续步骤和其他资源

以下文档提供了有关创建[!DNL Marketo Engage]源连接的详细信息：

* 有关如何将[!DNL Marketo Engage]数据连接到Platform的信息，请阅读有关[在UI中创建 [!DNL Marketo Engage] 源连接](../../../tutorials/ui/create/adobe-applications/marketo.md)的教程。
   * 有关如何设置架构和摄取自定义活动数据的信息，请阅读有关[为 [!DNL Marketo Engage] 自定义活动数据创建源连接和数据流](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)的教程
   * 有关如何将ECID映射从[!DNL Person]数据集迁移到[!DNL Activity]数据集的信息，请阅读[ECID映射迁移指南](./migration.md)。
* 有关用于[!DNL Marketo Engage]的B2B命名空间和架构的基础设置的信息，请阅读有关[B2B命名空间和架构](./marketo-namespaces.md)的文档。
* 有关查找[!DNL Marketo Engage] munchkin ID和生成凭据的信息，请阅读[[!DNL Marketo Engage] 身份验证指南](./marketo-auth.md)。
* 有关应用于[!DNL Marketo Engage]数据集的特定映射规则的信息，请阅读有关[[!DNL Marketo Engage] 字段映射](../mapping/marketo.md)的文档。
* 有关[!DNL Real-Time Customer Data Platform B2B Edition]及其功能的一般信息，请阅读[[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md)上的文档。
