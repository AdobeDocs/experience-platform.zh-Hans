---
keywords: Experience Platform；主页；热门主题；Marketo Engage;Marketo Engage;Marketo
solution: Experience Platform
title: Marketo Engage连接器
description: 本文档概述了Marketo Engage源连接器，包括有关其身份验证、映射和数据延迟的信息。
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# [!DNL Marketo Engage] 连接器

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (以下简称“[!DNL Marketo]“)是一个完整的解决方案，面向希望通过参与复杂购买历程的每个阶段来转变客户体验的潜在客户管理人员和B2B营销人员。

使用 [!DNL Marketo] 源连接器中，您可以从 [!DNL Marketo] 到平台，并使用与平台连接的应用程序保持此数据最新。

>[!IMPORTANT]
>
>您必须具有 [Adobe Real-time Customer Data Platform B2B版](../../../../rtcdp/b2b-overview.md) 以使用所有Marketo数据集进行 [实时客户资料](../../../../profile/home.md). 如果没有Real-Time CDP B2B Edition，您仍可以使用Marketo源将人员和活动数据集中的数据引入实时客户资料以进行分段。

本文档概述 [!DNL Marketo] 源连接器，包括如何验证连接器、如何映射 [!DNL Marketo] 字段，以及连接器的数据延迟。

## 验证 [!DNL Marketo] 连接器

为了连接 [!DNL Marketo] 对于Platform，您必须先检索 `munchkinId`, `clientId`和 `clientSecret`.

请参阅 [验证Marketo源连接器](./marketo-auth.md) 文档以检索您的凭据。

## 设置Adobe组织映射

在为 [!DNL Marketo]，则必须先设置Adobe组织映射。 有关如何完成此操作的详细步骤，请参阅 [设置Adobe组织映射 [!DNL Marketo]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## 设置B2B命名空间和模式自动生成实用程序

接下来，使用B2B命名空间和模式自动生成实用程序来设置您的平台开发人员控制台和Postman环境。 这允许您自动填充B2B命名空间和架构。 有关详细说明，请参阅 [设置B2B命名空间和模式自动生成实用程序](./marketo-namespaces.md)

## 体验数据模型(XDM)

XDM是一项公开记录的规范，它提供了常用结构和定义，允许您从第三方源中摄取数据，以用于下游Platform服务。

遵循XDM标准，可将数据统一纳入平台生态系统，从而更便于交付数据和收集信息。

要进一步了解XDM及其在Platform中的角色，请参阅 [XDM系统概述](../../../../xdm/home.md).

## 字段映射来源 [!DNL Marketo] 到XDM

在 [!DNL Marketo] 和Platform中，Marketo源数据字段在摄取到Platform之前必须映射到相应的目标XDM字段。

请参阅以下内容，以详细了解 [!DNL Marketo] 数据集和平台：

* [活动](../mapping/marketo.md#activities)
* [项目](../mapping/marketo.md#programs)
* [方案成员资格](../mapping/marketo.md#program-memberships)
* [公司](../mapping/marketo.md#companies)
* [静态列表](../mapping/marketo.md#static-lists)
* [静态列表成员关系](../mapping/marketo.md#static-list-memberships)
* [指定帐户](../mapping/marketo.md#named-accounts)
* [机会](../mapping/marketo.md#opportunities)
* [机会联系角色](../mapping/marketo.md#opportunity-contact-roles)
* [人员](../mapping/marketo.md#persons)

## 预期延迟 [!DNL Marketo] 平台上的数据

下表概述了为 [!DNL Marketo] 根据摄取的性质和所需的目标将数据导入平台：

| 目标 | 预期滞后 |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 1分钟 |
| 数据湖 | &lt; 60 分钟 |

## 后续步骤和其他资源

以下文档提供了有关创建 [!DNL Marketo] 源连接：

* 有关如何连接 [!DNL Marketo] 数据到平台，请参阅 [在UI中创建Marketo源连接器](../../../tutorials/ui/create/adobe-applications/marketo.md).
* 有关B2B命名空间和与 [!DNL Marketo]，请参阅 [B2B命名空间和架构](./marketo-namespaces.md).
* 有关查找 [!DNL Marketo] munchkin ID和生成您的凭据，请参阅 [[!DNL Marketo] 身份验证指南](./marketo-auth.md).
* 有关适用于的特定映射规则的信息 [!DNL Marketo] 数据集，请参阅 [[!DNL Marketo] 字段映射](../mapping/marketo.md).
* 有关 [!DNL Real-Time Customer Data Platform B2B Edition] 及其功能，请参阅 [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
