---
keywords: Experience Platform；主页；热门主题；Marketo Engage；营销参与；营销
solution: Experience Platform
title: Marketo Engage连接器
topic: 概述
description: 本文档概述了Marketo Engage源连接器，包括有关其身份验证、映射和数据延迟的信息。
translation-type: tm+mt
source-git-commit: 2563b413ec35cb4c5f05a54bce6f7271917e51f3
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---


# （测试版）[!DNL Marketo Engage]连接器

>[!IMPORTANT]
>
>[!DNL Marketo Engage]源当前处于测试状态。 其功能和文档可能会发生更改。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用平台服务构建、标记和增强传入数据。 您可以从各种来源收集数据，如Adobe应用程序、基于云的存储、数据库和许多其他来源。

[[!DNL Marketo Engage]](https://www.marketo.com/software/) （以下简称“”）是一个完整[!DNL Marketo]的解决方案，面向潜在客户管理和B2B营销人员，他们希望通过参与复杂购买旅程的每个阶段来转变客户体验。

借助[!DNL Marketo]源连接器，您可以将[!DNL Marketo]的B2B数据带到平台，并使用连接到平台的应用程序使此数据保持最新。

本文档概述了[!DNL Marketo]源连接器，包括有关如何验证连接器、如何将[!DNL Marketo]字段映射到体验数据模型(XDM)以及连接器的数据延迟的信息。

## 验证[!DNL Marketo]连接器

要将[!DNL Marketo]连接到平台，必须首先检索`munchkinId`、`clientId`和`clientSecret`的值。

请参阅[验证Marketo源连接器](./marketo-auth.md)文档中概述的步骤以检索凭据。

## 体验数据模型(XDM)

XDM是一个公开的文档规范，它提供了常见结构和定义，允许您从第三方源收集数据以用于下游平台服务。

遵循XDM标准，数据可以统一并入平台生态系统中，从而更轻松地交付数据和收集信息。

要进一步了解XDM及其在平台中的作用，请参阅[XDM系统概述](../../../../xdm/home.md)。

## 从[!DNL Marketo]到XDM的字段映射

要在[!DNL Marketo]和平台之间建立源连接，Marketo源数据字段必须映射到相应的目标XDM字段，然后才能被引入平台。

有关[!DNL Marketo]数据集和平台之间的字段映射规则的详细信息，请参见以下内容：

* [活动](../mapping/marketo.md#activities)
* [程序](../mapping/marketo.md#programs)
* [项目会员资格](../mapping/marketo.md#program-memberships)
* [公司](../mapping/marketo.md#companies)
* [静态列表](../mapping/marketo.md#static-lists)
* [静态列表成员关系](../mapping/marketo.md#static-list-memberships)
* [指定帐户](../mapping/marketo.md#named-accounts)
* [机会](../mapping/marketo.md#opportunities)
* [机会联系角色](../mapping/marketo.md#opportunity-contact-roles)
* [人](../mapping/marketo.md#persons)

## 平台上[!DNL Marketo]数据的预期延迟

下表根据摄取的性质和所需目标概述了将[!DNL Marketo]数据引入平台的预期延迟：

| 目标 | 预期延迟 |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| 数据湖 | &lt; 60 分钟 |

## 后续步骤和其他资源

以下文档提供了有关创建[!DNL Marketo]源连接的更多信息：

* 有关如何将[!DNL Marketo]数据连接到平台的信息，请参阅有关在UI](../../../tutorials/ui/create/adobe-applications/marketo.md)中创建Marketo源连接器的教程。[
* 有关与[!DNL Marketo]一起使用的B2B命名空间和模式的基础设置的信息，请参阅[B2B命名空间和模式](./marketo-namespaces.md)的文档。
* 有关查找[!DNL Marketo]验证ID和生成凭据的信息，请参阅[[!DNL Marketo] 验证指南](./marketo-auth.md)。
* 有关适用于[!DNL Marketo]数据集的特定映射规则的信息，请参阅有关[[!DNL Marketo] 字段映射](../mapping/marketo.md)的文档。