---
keywords: Experience Platform；主页；热门主题；访问控制；adobe admin console
solution: Experience Platform
feature: Attribution AI
title: Attribution AI的访问控制
description: 本文档提供了有关Attribution AI的基于属性的访问控制的信息。
exl-id: 3ed672bf-1fa6-4893-99e0-afc2b2179543
source-git-commit: f28558d5939607cabf449cbc03b7e0f5406f6326
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# Attribution AI中的访问控制

通过[Adobe Admin Console](https://adminconsole.adobe.com/)中的Adobe Experience Platform提供Attribution AI的访问控制。 此功能利用Admin Console中的产品配置文件，它将用户与权限和沙盒关联起来。

有关访问控制的详细信息，请参阅[访问控制概述](../../../access-control/home.md)。

## 基于属性的访问控制

>[!IMPORTANT]
>
>基于属性的访问控制当前仅在有限版本中可用。

[基于属性的访问控制](../../../access-control/abac/overview.md)是Adobe Experience Platform的一项功能，它使管理员能够根据属性控制对特定对象和/或功能的访问。 属性可以是添加到对象的元数据，例如添加到架构字段或区段的标签。 管理员定义包括管理用户访问权限的属性的访问策略。

此功能允许您使用定义组织或数据使用范围的标签来标记Experience Data Model (XDM)架构字段。 同时，管理员可以使用用户和角色管理界面定义围绕XDM架构字段的访问策略，并更好地管理授予用户或用户组（内部、外部或第三方用户）的访问权限。 此外，基于属性的访问控制允许管理员管理对特定区段的访问。

通过基于属性的访问控制，管理员可以控制用户对所有平台工作流和资源的敏感个人数据(SPD)和个人身份信息(PII)的访问。 管理员可以定义仅有权访问特定字段以及与这些字段对应的数据的用户角色。

由于基于属性的访问控制，某些字段和功能可能会受到访问限制，并且对于某些Attribution AI服务模型不可用。 示例包括“Identity”、“Score Definition”和“Clone”。

在Attribution AI工作区&#x200B;**分析页面**&#x200B;的顶部，侧栏中显示的详细信息具有受限访问权限。

![已突出显示受限架构字段的Attribution AI工作区。](../images/user-guide/access-restricted.png)

如果在&#x200B;**[!UICONTROL 创建模型工作流]**&#x200B;页面上选择具有受限架构的数据集，则数据集名称旁边会显示一个警告符号，消息为： [!UICONTROL 已排除受限信息]。

![突出显示受限数据集字段的Attribution AI工作区。](../images/user-guide/restricted-info-excluded.png)

当您在&#x200B;**[!UICONTROL 创建模型工作流]**&#x200B;页面上预览具有受限架构的数据集时，会显示一条警告，让您知道[!UICONTROL 由于访问限制，某些信息不会显示在数据集预览中。]

![Attribution AI工作区中突出显示了受限制的预览的架构字段的结果。](../images/user-guide/restricted-dataset-preview.png)

创建包含受限信息的模型并继续&#x200B;**[!UICONTROL 定义目标]**&#x200B;步骤后，顶部将显示警告： [!UICONTROL 由于访问限制，某些信息不会显示在配置中。]

![模型结果的受限字段突出显示的Attribution AI工作区。](../images/user-guide/information-not-displayed-save-and-exit.png)

## 后续步骤

通过阅读本指南，您已了解[!DNL Experience Platform]中访问控制的主要原则。 您现在可以继续阅读[访问控制用户指南](../overview.md)，以了解有关如何使用[!DNL Admin Console]创建产品配置文件和为[!DNL Platform]分配权限的详细步骤。
