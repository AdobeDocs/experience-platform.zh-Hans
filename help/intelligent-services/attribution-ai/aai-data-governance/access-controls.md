---
keywords: Experience Platform；主页；热门主题；访问控制；adobe admin console
solution: Experience Platform
feature: Attribution AI
title: Attribution AI的访问控制
description: 本文档提供了有关Attribution AI的基于属性的访问控制的信息。
exl-id: 3ed672bf-1fa6-4893-99e0-afc2b2179543
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---

# 访问控制

Attribution AI的访问控制通过Adobe Experience Platform提供，位于 [Adobe Admin Console](https://adminconsole.adobe.com/). 此功能利用Admin Console中的产品配置文件，它将用户与权限和沙盒相关联。

有关访问控制的详细信息，请参见 [访问控制概述](../../../access-control/home.md).

## 基于属性的访问控制

>[!IMPORTANT]
>
>基于属性的访问控制当前仅在有限版本中可用。

[基于属性的访问控制](../../../access-control/abac/overview.md) 是Adobe Experience Platform的一项功能，它允许管理员根据属性控制对特定对象和/或功能的访问。 属性可以是添加到对象的元数据，例如添加到架构字段或区段的标签。 管理员定义包含用于管理用户访问权限的属性的访问策略。

此功能允许您使用定义组织或数据使用范围的标签来标记Experience Data Model (XDM)架构字段。 同时，管理员可以使用用户和角色管理界面定义围绕XDM架构字段的访问策略，并更好地管理授予用户或用户组（内部、外部或第三方用户）的访问权限。 此外，基于属性的访问控制还允许管理员管理对特定区段的访问。

通过基于属性的访问控制，管理员可以控制用户对所有平台工作流和资源的敏感个人数据(SPD)和个人身份信息(PII)的访问。 管理员可以定义仅有权访问特定字段以及与这些字段对应的数据的用户角色。

由于基于属性的访问控制，某些字段和功能可能会受到访问限制，并且对于某些Attribution AI服务模型不可用。 示例包括“Identity”、“Score Definition”和“Clone”。

在Attribution AI工作区顶部 **分析页面**&#x200B;中，侧栏中显示的详细信息具有受限访问权限。

![突出显示受限架构字段的Attribution AI工作区。](../images/user-guide/access-restricted.png)

如果您选择的数据集在 **[!UICONTROL 创建模型工作流]** 页面上，数据集名称旁边会显示一个警告符号，并显示消息： [!UICONTROL 已排除受限制的信息].

![突出显示受限Attribution AI字段的数据集工作区。](../images/user-guide/restricted-info-excluded.png)

当您在“ ”上预览架构受限的数据集时 **[!UICONTROL 创建模型工作流]** 页面，会出现一条警告以告知您 [!UICONTROL 由于访问限制，某些信息不会显示在数据集预览中。]

![突出显示受限制预览的架构字段结果的Attribution AI工作区。](../images/user-guide/restricted-dataset-preview.png)

创建包含受限信息的模型并转到 **[!UICONTROL 定义目标]** 步骤，顶部将显示警告： [!UICONTROL 由于访问限制，某些信息不会显示在配置中。]

![突出显示模型结果的受限字段的Attribution AI工作区。](../images/user-guide/information-not-displayed-save-and-exit.png)

## 后续步骤

通过阅读本指南，您已经了解了中访问控制的主要原则 [!DNL Experience Platform]. 您现在可以继续访问 [访问控制用户指南](../overview.md) 有关如何使用 [!DNL Admin Console] 创建产品配置文件并为分配权限 [!DNL Platform].
