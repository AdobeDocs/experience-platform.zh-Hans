---
keywords: Experience Platform；主页；热门主题；Marketo Engage；marketo engage；marketo
solution: Experience Platform
title: Marketo Engage连接器
description: 本文档概述了Marketo Engage源连接器，包括有关其身份验证、映射和数据延迟的信息。
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: d8cd69524d984fdb828447287f3f4a4fe5913d61
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# [!DNL Marketo Engage] 连接器

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (以下简称“ ”[!DNL Marketo]“)是一个完整的解决方案，面向希望通过参与复杂购买历程的每个阶段来转变客户体验的潜在客户管理人员和B2B营销人员。

使用 [!DNL Marketo] 源连接器，您可以从 [!DNL Marketo] 到Platform ，并使用与平台连接的应用程序使这些数据保持最新。

>[!IMPORTANT]
>
>您必须有权访问 [Adobe Real-time Customer Data Platform B2B版本](../../../../rtcdp/b2b-overview.md) 要将所有Marketo数据集用于分段，请执行以下操作 [Real-time Customer Profile](../../../../profile/home.md). 如果没有Real-Time CDP B2B版本，您仍然可以使用Marketo源将人员和活动数据集中的数据引入实时客户档案以进行分段。

本文档概述了 [!DNL Marketo] 源连接器，包括有关如何验证连接器、如何映射的信息 [!DNL Marketo] Experience Data Model (XDM)的字段以及连接器的数据延迟。

## 验证您的 [!DNL Marketo] 连接器

为了连接 [!DNL Marketo] 到Platform，您必须首先检索 `munchkinId`， `clientId`、和 `clientSecret`.

请参阅中概述的步骤 [验证您的Marketo源连接器](./marketo-auth.md) 文档以检索您的凭据。

## 设置Adobe组织映射

在为建立映射集之前 [!DNL Marketo]中，您必须首先设置Adobe组织映射。 有关如何完成此操作的详细步骤，请参阅以下指南中的 [设置Adobe组织映射 [!DNL Marketo]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## 设置B2B命名空间和模式自动生成实用程序

接下来，使用B2B命名空间和架构自动生成实用程序来设置您的Platform开发人员控制台和Postman环境。 这允许您自动填充B2B命名空间和架构。 有关详细说明，请参阅 [设置B2B命名空间和模式自动生成实用程序](./marketo-namespaces.md)

## 体验数据模型(XDM)

XDM是一个公开记录的规范，它提供了通用结构和定义，允许您从第三方源摄取数据以用于下游平台服务。

遵守XDM标准允许将数据统一纳入平台生态系统，从而更轻松地提供数据和收集信息。

要了解有关XDM及其在Platform中的角色的更多信息，请参阅 [XDM系统概述](../../../../xdm/home.md).

## 字段映射自 [!DNL Marketo] 到XDM

建立源连接： [!DNL Marketo] 和Platform的客户，Marketo源数据字段必须在被摄取到Platform中之前映射到其相应的目标XDM字段。

有关以下字段之间的映射规则的详细信息，请参阅以下内容 [!DNL Marketo] 数据集和平台：

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

## 预期延迟 [!DNL Marketo] 平台上的数据

下表概述了在客户细分市场之前， [!DNL Marketo] 将数据导入Platform，具体取决于摄取的性质和所需的目标：

| 目标 | 预期延迟 |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 1分钟 |
| 数据湖 | &lt; 60 分钟 |

## 后续步骤和其他资源

以下文档提供了有关创建 [!DNL Marketo] 源连接：

* 有关如何连接 [!DNL Marketo] 将数据导入Platform，请阅读以下教程： [创建 [!DNL Marketo] UI中的源连接](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * 有关如何设置架构和摄取自定义活动数据的信息，请阅读以下教程： [创建源连接和数据流 [!DNL Marketo] 自定义活动数据](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
* 有关用于的B2B命名空间和架构的基础设置的信息 [!DNL Marketo]，请阅读相关文档 [B2B命名空间和架构](./marketo-namespaces.md).
* 有关查找 [!DNL Marketo] munchkin ID和生成凭据，请阅读 [[!DNL Marketo] 身份验证指南](./marketo-auth.md).
* 有关适用于的特定映射规则的信息 [!DNL Marketo] 数据集，请阅读相关的文档 [[!DNL Marketo] 字段映射](../mapping/marketo.md).
* 有关以下内容的一般信息： [!DNL Real-Time Customer Data Platform B2B Edition] 及其功能，请阅读以下文档： [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
