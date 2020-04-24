---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据使用标签用户指南
topic: labels
translation-type: tm+mt
source-git-commit: 475e774d5e7ebac036b42aa94736ba8e22c7185f

---


# 数据使用标签用户指南

本用户指南涵盖在Experience Platform用户界面中使用数据使用标签（也称为DULE标签）的步骤。 在使用指南之前，请参阅 [数据管理概述](../home.md) ，了解DULE框架的更强大的介绍。

## 在数据集级别管理数据使用标签

要在数据集级别管理数据使用标签，必须选择现有数据集或创建新数据集。 登录Adobe Experience Platform后，在左侧导 **[!UICONTROL Datasets]** 航中选择以打开数据集工 _作区_ 。 此页列表了属于您组织的所有已创建数据集以及与每个数据集相关的有用详细信息。

![数据工作区中的“数据集”选项卡](../images/labels/datasets.png)

下一节提供了创建新数据集以将标签应用到的步骤。 如果要编辑现有数据集的标签，请从列表中选择数据集，然后跳到向数 [据集添加数据使用标签](#add-labels)。

### 创建新数据集

>[!NOTE] 在此示例中，使用预配置的体验数据模型(XDM)模式创建数据集。 有关XDM模式的详细信息，请参阅 [XDM系统概述](../../xdm/home.md)[和模式合成基础知识](../../xdm/schema/composition.md)。

要创建新数据集，请 **[!UICONTROL Create Dataset]** 单击工作区右上角的 _[!UICONTROL Datasets]_数据集。

![](../images/labels/create_dataset.png)

屏幕 _[!UICONTROL Create Dataset]_出现。 单击此处&#x200B;**[!UICONTROL Create Dataset from Schema]**。

![从模式创建数据集](../images/labels/dataset_create.png)

此时 _[!UICONTROL Select Schema]_会显示屏幕，该屏幕列表可用于创建数据集的所有可用模式。 单击模式旁边的单选按钮以选择它。 右_[!UICONTROL Schemas]_ 侧的部分显示有关所选模式的其他详细信息。 选择模式后，单击 **[!UICONTROL Next]**。

![选择数据集模式](../images/labels/dataset_schema.png)

将显 _示配置数据集_ 。 为新数 **据集提供** （必需） **名称和说明** （可选，但建议），然后单击 **[!UICONTROL Finish]**。

![使用名称和说明配置数据集](../images/labels/dataset_configure.png)

此时 _[!UICONTROL Dataset Activity]_会显示该页面，其中显示有关新创建的数据集的信息。 在此示例中，数据集命名为“Loyalty Members”，因此顶部导航显示的是“数据集”>“_ Loyalty Members”_。

![数据集活动页](../images/labels/dataset_activity.png)

### 向数据集添加数据使用标签 {#add-labels}

创建新数据集或从工作区中的列表中选择现有数据集后， _[!UICONTROL Datasets]_单击以&#x200B;**[!UICONTROL Data Governance]**打开工作_[!UICONTROL Data Governance]_ 区。 工作区允许您管理数据集级别和字段级别的数据使用标签。

![“数据集数据管理”选项卡](../images/labels/dataset_data_governance.png)

要编辑数据集级别的数据使用标签，请通过单击数据集名称旁边的铅笔图标进行开始。

![编辑数据集级别标签](../images/labels/dataset_labels_edit_button.png)

将打 _[!UICONTROL Edit Governance Labels]_开对话框。 在对话框中，选中要应用到数据集的标签旁边的复选框。 请记住，这些标签将由数据集中的所有字段继承。 勾选_[!UICONTROL Applied Labels]_ 每个框时，标题会随之更新，显示您选择的标签。 选择所需的标签后，单击 **[!UICONTROL Save Changes]**。

<img alt="在数据集级别应用管理标签" src="../images/labels/apply-labels-dataset.png" width="700"><br>

将重 _[!UICONTROL Data Governance]_新显示工作区，其中显示您在数据集级别应用的标签。 您还可以看到标签将继承到数据集中的每个字段。

![字段继承的数据集标签](../images/labels/dataset_inherited_labels.png)

请注意，数据集级别的标签旁边会显示“x”，允许您删除标签。 每个字段旁边的继承标签旁边没有“x”，并且显示为“灰显”，无法删除或编辑。 这是因为继 **承的字段是只读的**，这意味着它们无法在字段级别删除。

默 **[!UICONTROL Show Inherited Labels]** 认情况下，此切换处于打开状态，这样您就可以看到从数据集继承到其字段的任何标签。 关闭切换将隐藏数据集中所有继承的标签。

![隐藏继承的标签](../images/labels/hide_inherited_labels.png)

## 在数据集字段级别管理数据使用标签

继续在数据集 [级别添加和编辑数据使用标签的工作流](#add-labels)，您还可以管理该数据集工作区中的字段级 _[!UICONTROL Data Governance]_别标签。

要将数据使用标签应用到单个字段，请选中字段名称旁边的复选框，然后单击 **[!UICONTROL Edit Governance Labels]**。

![编辑字段标签](../images/labels/fields_single_field.png)

将出 _[!UICONTROL Edit Governance Labels]_现对话框。 该对话框显示显示选定字段、应用的标签和继承的标签的标题。 请注意，继承的标签（C2和C5）在对话框中灰显。 它们是从数据集级别继承的只读标签，因此只能在数据集级别编辑。

<img alt="编辑单个字段的管理标签" src="../images/labels/field-label-inheritance.png" width="700"><br>

单击要使用的每个标签旁边的复选框，以选择字段级标签。 在选择标签时，标题 _[!UICONTROL Applied Labels]_将更新为显示应用于标题中显示的字段的标_[!UICONTROL Selected Fields]_ 签。 选择字段级标签后，单击 **[!UICONTROL Save Changes]**。

<img alt="应用字段级标签" src="../images/labels/apply-labels-field.png" width="700"><br>

工 _[!UICONTROL Data Governance]_作区将重新显示，现在在字段名称旁边的行中显示选定的字段级别标签。 请注意，字段级标签旁边有一个“x”，允许您删除该标签。

![显示字段级标签的字段](../images/labels/fields_show_field_level_labels.png)

您可以重复这些步骤以继续为其他字段添加和编辑字段级标签，包括选择多个字段以同时应用字段级标签。

![选择多个字段以同时应用字段级标签。](../images/labels/fields_select_multiple.png)

务必记住，继承仅从顶级向下移动（数据集→字段），这意味着在字段级别应用的标签不会传播到其他字段或数据集。

## 后续步骤

现在，您已在数据集和字段级别添加了数据使用标签，可以开始将数据引入Experience Platform。 要了解更多信息，请阅读数据获取文 [档进行开始](../../ingestion/home.md)。

您现在还可以根据已应用的标签定义数据使用策略。 有关详细信息，请参阅数 [据使用策略概述](../policies/overview.md)。

## Journey Orchestration

以下视频旨在支持您对“数据管理”的理解，并概述如何将标签应用到数据集和单个字段。

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
