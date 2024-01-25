---
title: 管理架构的数据使用标签
description: 了解如何在Adobe Experience Platform UI中将数据使用标签添加到Experience Data Model (XDM)架构字段。
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: 37395e5762c8d54e6fca5c3502bdbf56f5b5472c
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 8%

---

# 管理架构的数据使用标签

>[!IMPORTANT]
>
>基于模式的标签是的一部分 [基于属性的访问控制](../../access-control/abac/overview.md)，目前面向美国医疗保健客户限量发行。 此功能在完全发布后将可供所有Adobe Real-time Customer Data Platform客户使用。

所有带入Adobe Experience Platform的数据都受Experience Data Model (XDM)架构的约束。 贵组织或法律法规可能会对此数据设置使用限制。为此，Platform允许您通过使用来限制某些数据集和字段的使用 [数据使用标签](../../data-governance/labels/overview.md).

应用于架构字段的标签指示应用于该特定字段中包含的数据的使用策略。

标签可应用于单个架构以及这些架构中的字段。 当标签直接应用于架构时，这些标签会传播到基于该架构的所有现有和未来数据集。

此外，在一个架构中添加的任何字段标签会传播到使用来自共享类或字段组的相同字段的所有其他架构。 这有助于确保在整个数据模型中类似字段的使用规则保持一致。

本教程介绍了在Platform UI中使用架构编辑器向架构添加标签的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [[!DNL Experience Data Model (XDM) System]](../home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [架构编辑器](../ui/overview.md)：了解如何在Platform UI中创建和管理架构和其他资源。
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md)：提供用于对Platform操作强制实施数据使用限制的基础架构，其中使用策略定义可以（或不能）对标记数据执行哪些营销操作。

## 选择要将标签添加到的架构或字段 {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="编辑治理标签"
>abstract="将标签应用于架构字段可指示适用于该特定字段中包含的数据的使用策略。"

要开始添加标签，您必须首先 [选择要编辑的现有架构](../ui/resources/schemas.md#edit) 或 [创建新架构](../ui/resources/schemas.md#create) 以在架构编辑器中查看其结构。

要编辑单个字段的标签，您可以在画布中选择该字段，然后选择 **[!UICONTROL 管理访问权限]** 在右边栏中。

>[!IMPORTANT]
>
>最多可以将300个标签应用于任何架构。

![从架构编辑器画布中选择字段](../images/tutorials/labels/manage-access.png)

您还可以选择 **[!UICONTROL 标签]** 选项卡，从列表中选择所需的字段，然后选择 **[!UICONTROL 应用访问和数据治理标签]** 在右边栏中。

![从中选择一个字段 [!UICONTROL 标签] 选项卡](../images/tutorials/labels/select-field-on-labels-tab.png)

要编辑整个架构的标签，请在 **[!UICONTROL 标签]** 选项卡，选中过滤器图标下的复选框。 这将选择架构中的每个可用字段。 接下来，选择 **[!UICONTROL 应用访问和数据治理标签]** 在右边栏中。

![从中选择架构名称 [!UICONTROL 标签] 选项卡](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>当您首次尝试编辑架构或字段的标签时，会出现一条免责声明消息，说明根据您组织的策略，标签的使用对下游操作有何影响。 选择 **[!UICONTROL 继续]** 以继续编辑。
>
>![标签使用免责声明](../images/tutorials/labels/disclaimer.png)

## 编辑架构或字段的标签 {#edit-labels}

将出现一个对话框，允许您编辑所选字段的标签。 如果您选择了单个对象类型字段，右边栏会列出应用标签将传播到的子字段。

![应用访问和数据管理标签对话框，其中突出显示了所选字段。](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>如果您正在编辑整个架构的字段，右边栏不会列出适用的字段，而是显示架构名称。

使用显示的列表选择要添加到架构或字段的标签。 选择标签后， **[!UICONTROL 应用的标签]** 部分更新以显示迄今为止已选择的标签。

![应用访问和数据管理标签对话框突出显示了应用的标签。](../images/tutorials/labels/applied-labels.png)

要按类型筛选显示的标签，请在左边栏中选择所需的类别。 要创建新的自定义标签，请选择 **[!UICONTROL 创建标签]**.

![应用访问和数据治理标签对话框，其中应用了标签类型过滤器，并突出显示创建标签。](../images/tutorials/labels/filter-and-create-custom.png)

在您对所选标签满意后，选择 **[!UICONTROL 保存]** 以将其应用于字段或架构。

![突出显示应用访问和数据治理标签对话框并带有保存。](../images/tutorials/labels/save-labels.png)

此 **[!UICONTROL 标签]** 选项卡将重新出现，其中显示应用于架构的标签。

![突出显示应用字段标签的架构工作区的标签选项卡。](../images/tutorials/labels/field-labels-added.png)

## 后续步骤

本指南介绍了如何管理架构和字段的数据使用标签。 有关管理数据使用标签的信息（包括如何将其添加到特定数据集而非架构级别），请参阅 [数据使用标签UI指南](../../data-governance/labels/user-guide.md).
