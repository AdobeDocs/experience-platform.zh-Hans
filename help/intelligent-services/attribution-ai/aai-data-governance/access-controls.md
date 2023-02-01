---
keywords: Experience Platform；主页；热门主题；访问控制；Adobe Admin Console
solution: Experience Platform
feature: Attribution AI
title: Attribution AI访问控制
description: 本文档提供了有关基于属性的Attribution AI访问控制的信息。
source-git-commit: d82fd8dd5efbe314c09d32905f8ab964640cc11a
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---


# 访问控制

Attribution AI的访问控制通过Adobe Experience Platform(位于 [Adobe Admin Console](https://adminconsole.adobe.com/). 此功能可利用Admin Console中的产品配置文件，将用户与权限和沙箱相关联。

有关访问控制的更多信息，请参阅 [访问控制概述](../../../access-control/home.md).

## 基于属性的访问控制

>[!IMPORTANT]
>
>基于属性的访问控制当前仅在有限版本中可用。

[基于属性的访问控制](../../../access-control/abac/overview.md) 是Adobe Experience Platform的一项功能，它使管理员能够根据属性控制对特定对象和/或功能的访问。 属性可以是添加到对象的元数据，如添加到架构字段或区段的标签。 管理员定义包含属性的访问策略以管理用户访问权限。

利用此功能，可为体验数据模型(XDM)架构字段设置标签，以定义组织或数据使用范围。 同时，管理员可以使用用户和角色管理界面来定义围绕XDM架构字段的访问策略，并更好地管理为用户或用户组（内部、外部或第三方用户）授予的访问权限。 此外，基于属性的访问控制允许管理员管理对特定区段的访问。

通过基于属性的访问控制，管理员可以控制用户对所有平台工作流和资源中的敏感个人数据(SPD)和个人身份信息(PII)的访问。 管理员可以定义用户角色，这些用户角色只能访问与这些字段对应的特定字段和数据。

由于基于属性的访问控制，某些字段和功能可能会限制访问，并且对于某些Attribution AI服务模型不可用。 示例包括“身份”、“得分定义”和“克隆”。

Attribution AI工作区顶部 **分析页面**，侧栏中显示的详细信息具有受限访问权限。

![Attribution AI工作区中突出显示了受限架构字段。](../images/user-guide/access-restricted.png)

如果您在 **[!UICONTROL 创建模型工作流]** 页面上，数据集名称旁边会显示一个警告标记，并显示一条消息： [!UICONTROL 排除受限信息].

![Attribution AI工作区中突出显示了受限数据集字段。](../images/user-guide/restricted-info-excluded.png)

预览 **[!UICONTROL 创建模型工作流]** 页面时，会显示一条警告，告知您 [!UICONTROL 由于访问限制，某些信息未在数据集预览中显示。]

![Attribution AI工作区中突出显示了受限制的预览架构字段的结果。](../images/user-guide/restricted-dataset-preview.png)

创建具有受限信息的模型后，继续 **[!UICONTROL 定义目标]** 步骤，顶部将显示警告： [!UICONTROL 由于访问限制，某些信息未显示在配置中。]

![Attribution AI工作区中，模型结果的受限字段突出显示。](../images/user-guide/information-not-displayed-save-and-exit.png)

## 后续步骤

通过阅读本指南，您已介绍中访问控制的主要原则 [!DNL Experience Platform]. 您现在可以继续 [访问控制用户指南](../overview.md) 以了解有关如何使用的详细步骤 [!DNL Admin Console] 创建产品配置文件并为 [!DNL Platform].
