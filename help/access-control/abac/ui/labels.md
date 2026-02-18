---
keywords: Experience Platform；主页；热门主题；访问控制；基于属性的访问控制
title: 基于属性的访问控制管理标签
description: 通过Adobe Experience Cloud中的“权限”界面管理标签。
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: 855f0a1384f658d39aa9d4fbb6bcb032933e59db
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 11%

---

# 管理标签

您可以使用标签根据数据使用情况和基于属性的访问控制策略对数据集和字段进行分类。 您可以随时应用标签，灵活地选择管理数据的方式。 最佳实践鼓励在将数据摄取到Adobe Experience Platform中后立即为其设置标签，或者在数据可供使用后立即为其设置标签。 请阅读本文档，了解如何在权限UI中管理标签。

有关标签及其相应治理策略的完整列表，请阅读有关[核心数据使用标签](../../../data-governance/labels/reference.md){target="_blank"}的指南。

>[!NOTE]
>
>要创建或查看字段包含给定标签的[计算属性](../../../profile/computed-attributes/overview.md){target="_blank"}，您必须有权访问该标签。

## 浏览标签 {#explore-labels}

要查看所有可用的标签，请在&#x200B;**[!UICONTROL Permissions]** Adobe Experience Cloud[中导航到](https://experience.adobe.com/){target="_blank"}。 从左侧面板中选择&#x200B;**[!UICONTROL Labels]**。

![权限中的标签工作区，其标签在左侧面板中突出显示。](../../images/ui/labels/labels-home.png){zoomable="yes"}

标签按类型分类，并属于以下类别之一：

| 类型 | 描述 |
| --- | --- |
| [合同](../../../data-governance/labels/reference.md#contract){target="_blank"} | 此类别用于对具有合同义务或与组织的数据治理策略相关的数据进行分类。 |
| [身份标识](../../../data-governance/labels/reference.md#identity){target="_blank"} | 此类别用于对可直接或间接识别人员的数据进行分类。 |
| [敏感](../../../data-governance/labels/reference.md#sensitive){target="_blank"} | 此类别用于对组织认为敏感的数据进行分类。 |
| [合作伙伴生态系统](../../../data-governance/labels/reference.md#partner){target="_blank"} | 此类别用于对从组织外部来源获取的数据进行分类。 |
| 负责任的参与 | 此类别包含单个标签&#x200B;**[!UICONTROL Potential for Bias]**，该标签反映有可能引入偏差的数据。 |
| 自定义 | 此类别包含您的组织创建的标签。 |

要筛选标签，请选择筛选器图标（![筛选器图标](/help/images/icons/filter.png)），然后从&#x200B;**[!UICONTROL Type]**&#x200B;下拉列表中选择所需的标签类型。

![标签工作区中扩展了筛选器选项并突出显示类型下拉列表。](../../images/ui/labels/label-filter.png){zoomable="yes"}

要查看单个标签，请从列表中选择标签名称。 此时将显示标签的详细信息页面。 Adobe的核心标签&#x200B;**不**&#x200B;可编辑。

![单个标签的详细信息页面。](../../images/ui/labels/label-details.png){zoomable="yes"}

## 创建自定义标签 {#create-custom-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="标签使用"
>abstract="您可以使用自定义标签将数据治理和访问控制配置应用于您的数据。"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="创建新标签"
>abstract="可自行创建自定义标签以适合组织需求。自定义标签可用于将数据治理和访问控制配置应用于您的数据。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=zh-Hans#manage-labels" text="管理自定义标签"

>[!NOTE]
>
>要创建自定义标签，您需要一个包含&#x200B;**[!UICONTROL Manage Usage Labels]**&#x200B;权限和`Prod`沙盒的角色。

要创建新标签，请从&#x200B;**[!UICONTROL Labels]**&#x200B;工作区的左侧面板中选择&#x200B;**[!UICONTROL Permissions]**，然后选择&#x200B;**[!UICONTROL Create label]**。

![突出显示了“创建标签”选项的标签工作区。](../../images/ui/labels/create-label.png){zoomable="yes"}

出现&#x200B;**[!UICONTROL Create new label]**&#x200B;对话框，提示您输入&#x200B;**[!UICONTROL Name]**、**[!UICONTROL Friendly name]**&#x200B;和&#x200B;**[!UICONTROL Description]**。

>[!IMPORTANT]
>
> 在创建标签后无法更改标签的[!UICONTROL Name]，当前不支持删除标签。

选择&#x200B;**[!UICONTROL Confirm]**&#x200B;以完成创建标签。

![已填写“名称”、“友好名称”和“描述”并突出显示“确认”选项的“创建新标签”对话框。](../../images/ui/labels/create-new-label.png){zoomable="yes"}

## 编辑自定义标签 {#edit-custom-label}

虽然您无法编辑自定义标签的&#x200B;**[!UICONTROL Name]**，但可以编辑&#x200B;**[!UICONTROL Friendly name]**&#x200B;和&#x200B;**[!UICONTROL Description]**。 要编辑自定义标签，请从&#x200B;**[!UICONTROL Labels]**&#x200B;工作区内的列表中选择该标签。

![标签突出显示的标签工作区。](../../images/ui/labels/select-label.png){zoomable="yes"}

编辑任一字段，然后单击文本框之外的任意位置以保存更改。 屏幕上将显示一条确认消息，**[!UICONTROL Modified by]**&#x200B;名称和&#x200B;**[!UICONTROL Modified]**&#x200B;日期将会更改。

![显示带有“更新成功”消息的标签详细信息页面。](../../images/ui/labels/edit-label.png){zoomable="yes"}

## 后续步骤

现在，您已更深入地了解了标签，可以开始[将它们应用于架构](../../../xdm/tutorials/labels.md)。
