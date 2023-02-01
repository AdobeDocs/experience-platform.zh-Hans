---
keywords: Experience Platform；用户指南；客户人工智能；热门主题；访问控制；创建模型；
solution: Experience Platform
feature: Customer AI
title: Customer AI的访问控制
description: 本文档提供了有关Customer AI基于属性的访问控制的信息。
source-git-commit: 6f386d859b8553050ead266fad0e473c7cf7095e
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# 基于属性的访问控制

>[!IMPORTANT]
>
>基于属性的访问控制当前仅在有限版本中可用。

[基于属性的访问控制](../../../access-control/abac/overview.md) 是Adobe Experience Platform的一项功能，它使管理员能够根据属性控制对特定对象和/或功能的访问。 属性可以是添加到对象的元数据，如添加到架构字段或区段的标签。 管理员定义包含属性的访问策略以管理用户访问权限。

利用此功能，可为体验数据模型(XDM)架构字段设置标签，以定义组织或数据使用范围。 同时，管理员可以使用用户和角色管理界面来定义围绕XDM架构字段的访问策略，并更好地管理为用户或用户组（内部、外部或第三方用户）授予的访问权限。 此外，基于属性的访问控制允许管理员管理对特定区段的访问。

通过基于属性的访问控制，贵组织的管理员可以控制用户对所有平台工作流和资源中敏感个人数据(SPD)和个人身份信息(PII)的访问。 管理员可以定义用户角色，这些用户角色只能访问与这些字段对应的特定字段和数据。

由于基于属性的访问控制，某些字段和功能将受到限制，并且对某些Customer AI服务模型不可用。 示例包括“身份”、“得分定义”和“克隆”。

![突出显示服务模型结果的受限字段的Customer AI工作区。](../images/user-guide/unavailable-functionalities.png)

位于Customer AI工作区顶部 **分析页面**，请注意侧栏、得分定义、身份和用户档案属性中的详细信息都显示“访问受限”。

![突出显示了架构的受限字段的Customer AI工作区。](../images/user-guide/access-restricted.png)

预览 **[!UICONTROL 创建模型工作流]** 页面时，会显示一条警告，告知您 [!UICONTROL 由于访问限制，某些信息未在数据集预览中显示。]

![预览数据集的受限字段位于Customer AI工作区中，且模式结果受限。](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

创建具有受限信息的模型后，继续 **[!UICONTROL 定义目标]** 步骤，顶部将显示警告： [!UICONTROL 由于访问限制，某些信息未显示在配置中。]

![突出显示服务模型结果的受限字段的Customer AI工作区。](../images/user-guide/information-not-displayed-save-and-exit.png)

使用访问控制时， **查看客户人工智能** 和 **管理客户人工智能** 权限授予对客户AI不同功能的访问权限。 的 **管理客户人工智能** 许可允许您 **创建**,**更新**, **删除**, **启用**&#x200B;或 **禁用** 模型 **查看客户人工智能** 可供您阅读或查看。 的 **创建**, **更新** 和 **删除** 操作由审核日志记录。

请参阅相关文档以了解 [为访问控制分配权限](../../../access-control/home.md) 或如何 [使用审核日志来监控访问和活动](../../../landing/governance-privacy-security/audit-logs/overview.md).

## 后续步骤

通过阅读本指南，您已介绍中访问控制的主要原则 [!DNL Experience Platform]. 您现在可以继续 [访问控制用户指南](../overview.md) 以了解有关如何使用的详细步骤 [!DNL Admin Console] 创建产品配置文件并为 [!DNL Platform].