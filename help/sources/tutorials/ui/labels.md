---
title: 应用访问标签以管理用户对用户界面中源数据流的访问
description: 了解如何使用Experience Platform UI应用访问标签和管理用户对您的源数据流的访问权限。
hide: true
hidefromtoc: true
source-git-commit: 80fb60abdf33eb2a7ca691a9a48a811c632b34fc
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 2%

---

# 应用访问标签以管理用户对用户界面中源数据流的访问

您可以使用Real-Time CDP中由[基于属性的访问控制](../../../access-control/abac/overview.md)提供的功能将标签应用于源数据流。 利用此功能，您可以确保组织中只有一部分用户有权访问特定源数据流。

向特定数据流添加访问标签时，只有对分配了该标签的角色具有访问权限的用户才能查看和编辑该数据流。 如果源数据流未标记任何标签，则它对于属于您组织的所有用户都可见。 例如，如果将C12标签应用于数据流，则分配到没有C12标签的角色的用户将无法查看和编辑具有C12标签的数据流。

有关如何使用Adobe Experience Platform用户界面将访问标签应用于源数据流的信息，请阅读本指南。

## 快速入门

在使用访问控制标签之前，请确保您首先要熟悉基于属性的访问控制的功能。 有关详细信息，请阅读以下文档：

* [基于属性的访问控制概述](../../../access-control/abac/overview.md)
* [基于属性的访问控制端到端指南](../../../access-control/abac/end-to-end-guide.md)
* [使用权限UI管理标签](../../../access-control/abac/ui/labels.md)
* [数据使用标签词汇表](../../../data-governance/labels/reference.md)

## 将访问标签应用于源数据流

>[!NOTE]
>
>* 不能将标签应用于流运行。 但是，流运行会继承您应用于父数据流的任意标签。
>
>* 如果您没有数据流的查看访问权限，则也无法查看其对应的流运行。

要将访问标签应用于源数据流，请导航到&#x200B;**[!UICONTROL 源]** > **[!UICONTROL 数据流]**，然后找到要更新的数据流并限制用户访问。

接下来，选择[!UICONTROL 名称]列中的省略号(`...`)，然后选择&#x200B;**[!UICONTROL 应用访问标签]**&#x200B;以添加和管理所选数据流的标签。

![源中已选择“应用访问标签”选项的数据流页面。](../../images/tutorials/labels/apply_access_labels.png)

出现[!UICONTROL 应用访问和数据治理标签]窗口。 使用此窗口选择要应用于数据流的标签。 您还可以按标签类型筛选标签。 完成后，选择&#x200B;**[!UICONTROL 保存]**。

![已选择C2标签的数据治理标签窗口。](../../images/tutorials/labels/labels_window.png)

成功配置数据流访问标签后，任何无权访问该标签的用户将无法再检索数据流。 您还可以使用[!UICONTROL 访问标签]列查看应用于给定数据流的标签。

## 后续步骤

您现在知道如何将访问标签应用于源数据流。 现在，您可以确保只有贵组织中的特定用户组才能访问特定源数据流。 有关其他信息，请阅读以下文档：

* [将访问标签应用于API中的源数据流](../api/labels.md)
* [访问控制概述](../../../access-control/home.md)