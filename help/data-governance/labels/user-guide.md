---
keywords: Experience Platform；主页；热门主题；数据管理；数据使用标签；策略服务；数据使用标签用户指南
solution: Experience Platform
title: 在UI中管理数据使用情况标签
description: 本指南介绍了在Adobe Experience Platform用户界面中使用数据使用标签的步骤。
exl-id: aa44d5cc-416a-4ef2-be14-b4f32aec162c
source-git-commit: 1a4e71ee07900fb4f1581274f740ddb96cb93289
workflow-type: tm+mt
source-wordcount: '1529'
ht-degree: 17%

---

# 在UI中管理数据使用情况标签 {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_description"
>title="在 Platform 中治理数据使用"
>abstract="<h2>描述</h2><p>通过 Experience Platform 中的数据治理框架，可根据数据使用限制为属性和数据集加标签，以及设置标识特定营销活动并为其遵守这些限制的策略。</p>"

本用户指南介绍了在 [!DNL Experience Platform] 用户界面。

## 在数据集级别管理标签

>[!IMPORTANT]
>
>仅支持在数据集级别应用标签用于数据管理用例。 如果您尝试为数据创建访问策略，则必须 [将标签应用到架构](../../xdm/tutorials/labels.md) 数据集所基于的信息。 请参阅 [基于属性的访问控制](../../access-control/abac/overview.md) 以了解更多信息。

要在数据集级别管理数据使用情况标签，您必须选择一个现有数据集或创建一个新数据集。 登录Adobe Experience Platform后，选择 **[!UICONTROL 数据集]** 在左侧导航中打开 **[!UICONTROL 数据集]** 工作区。 此页面列出了属于贵组织的所有已创建数据集，以及与每个数据集相关的有用详细信息。

![数据工作区中的“数据集”选项卡](../images/labels/datasets-tab.png)

下一部分提供了创建新数据集以将标签应用到的步骤。 如果要编辑现有数据集的标签，请从列表中选择该数据集，然后跳到 [向数据集添加数据使用标签](#add-labels).

### 创建新数据集

>[!NOTE]
>
>在此示例中，使用预配置的 [!DNL Experience Data Model] (XDM)架构。 有关XDM模式的更多信息，请参阅 [XDM系统概述](../../xdm/home.md) 和 [架构组合基础知识](../../xdm/schema/composition.md).

要创建新数据集，请选择 **[!UICONTROL 创建数据集]** 的右上角 **[!UICONTROL 数据集]** 工作区。

![](../images/labels/create-dataset.png)

的 **[!UICONTROL 创建数据集]** 屏幕。 从此处选择 **[!UICONTROL 从架构创建数据集]**.

![从架构创建数据集](../images/labels/create-from-dataset.png)

的 **[!UICONTROL 选择架构]** 屏幕，其中列出了可用于创建数据集的所有可用架构。 选择架构旁边的单选按钮以将其选中。 的 **[!UICONTROL 模式]** 右侧的部分显示有关所选架构的其他详细信息。 选择架构后，选择 **[!UICONTROL 下一个]**.

![选择数据集架构](../images/labels/select-schema.png)

的 **[!UICONTROL 配置数据集]** 屏幕。 为新数据集提供名称（必需）和描述（可选，但推荐），然后选择 **[!UICONTROL 完成]**.

![使用名称和描述配置数据集](../images/labels/configure-dataset.png)

的 **[!UICONTROL 数据集活动]** 页面，其中显示了有关新创建数据集的信息。 在此示例中，数据集名为“忠诚会员”，因此，顶部导航会显示 **数据集>忠诚度会员**.

![“数据集活动”页面](../images/labels/dataset-created.png)

### 向数据集添加数据使用情况标签 {#add-labels}

创建新数据集或从 **[!UICONTROL 数据集]** 工作区，选择 **[!UICONTROL 数据管理]** 打开 **[!UICONTROL 数据管理]** 工作区。 利用工作区，可在数据集级别和字段级别管理数据使用情况标签。

![“数据集数据管理”选项卡](../images/labels/dataset-governance.png)

要在数据集级别编辑数据使用情况标签，请首先选择数据集名称旁边的铅笔图标。

![编辑数据集级别的标签](../images/labels/dataset-level-edit.png)

的 **[!UICONTROL 编辑管理标签]** 对话框。 在对话框中，选中要应用于数据集的标签旁边的复选框。 请记住，这些标签将由数据集内的所有字段继承。 的 **[!UICONTROL 应用的标签]** 标题会随您选中每个框而更新，并显示您选择的标签。 选择所需的标签后，选择 **[!UICONTROL 保存更改]**.

![在数据集级别应用管理标签](../images/labels/apply-labels-dataset.png)

的 **[!UICONTROL 数据管理]** 工作区会重新显示，其中显示了您在数据集级别应用的标签。 您还可以看到标签将继承到数据集中的每个字段。

![字段继承的数据集标签](../images/labels/dataset-labels-applied.png)

请注意，数据集级别的标签旁边会显示一个“x”，允许您删除这些标签。 每个字段旁边的继承标签旁边没有“x”，并且显示为“灰显”，无法删除或编辑。 这是因为 **继承字段为只读字段**，这表示无法在字段级别删除这些值。

的 **[!UICONTROL 显示继承的标签]** 默认情况下，会开启切换开关，以便您查看从数据集继承到其字段的任何标签。 关闭此切换开关会隐藏数据集中的任何继承标签。

![隐藏继承的标签](../images/labels/inherited-labels.png)

## 在数据集字段级别管理标签 {#manage-labels-at-dataset-field-level}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_instructions"
>title="说明"
>abstract="<ol><li>在左侧导航中选择<a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/user-guide.html">数据集</a>，然后选择要限制其数据的数据集。</li><li>从数据集详细信息视图中，选择<b>数据治理</b>选项卡。</li><li>选择要限制的数据集字段，然后选择<b>编辑治理标签</b>以根据使用限制为数据加标签。</li><li>为数据加标签后，在左侧导航中选择<a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=zh-Hans">策略</a>，然后选择<b>创建策略</b>。</li><li>选择创建一个<a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html#create-governance-policy">数据治理策略</a>，然后选择将应用于该策略的数据使用标签。</li><li>选择该策略将拒绝对任何包含这些标签的数据执行的营销操作。创建该策略后，从列表中选择它，然后使用右边栏中的切换开关启用它。</li><li>对于每个启用的策略，Platform 阻止将任何包含指定标签的数据用于所定义的营销操作。当您尝试对于具有关联的营销操作（用例）的目标激活加了标签的数据时，将自动施加此强制。</li></ol>"

>[!IMPORTANT]
>
>仅在数据管理用例支持在数据集字段级别应用标签。 如果您尝试为数据创建访问策略，则必须 [将标签应用到架构](../../xdm/tutorials/labels.md) 数据集所基于的信息。 请参阅 [基于属性的访问控制](../../access-control/abac/overview.md) 以了解更多信息。

继续工作流 [在数据集级别添加和编辑数据使用情况标签](#add-labels)，您还可以在 **[!UICONTROL 数据管理]** 工作区。

要将数据使用情况标签应用于单个字段，请选中字段名称旁边的复选框，然后选择 **[!UICONTROL 编辑管理标签]**.

![编辑字段标签](../images/labels/field-label-edit.png)

的 **[!UICONTROL 编辑管理标签]** 对话框。 该对话框显示标题，其中显示了选定字段、应用的标签和继承的标签。 请注意，继承的标签（C2和C5）在对话框中呈灰显状态。 它们是从数据集级别继承的只读标签，因此只能在数据集级别编辑。

![编辑单个字段的管理标签](../images/labels/field-label-inheritance.png)

通过选中您要使用的每个标签旁边的复选框，选择字段级别的标签。 当您选择标签时， **[!UICONTROL 应用的标签]** 标题更新，以显示应用于中显示的字段的标签 **[!UICONTROL 选定字段]** 标题。 选择完字段级别标签后，请选择 **[!UICONTROL 保存更改]**.

![应用字段级别的标签](../images/labels/apply-labels-field.png)

的 **[!UICONTROL 数据管理]** 工作区会重新显示，现在该工作区会在字段名称旁边的行中显示选定的字段级别标签。 请注意，字段级别的标签旁边有一个“x”，允许您删除该标签。

![显示字段级别标签的字段](../images/labels/field-labels-applied.png)

您可以重复这些步骤以继续为其他字段添加和编辑字段级别标签，包括选择多个字段以同时应用字段级别标签。

![选择多个字段以同时应用字段级别标签。](../images/labels/multiple-fields.png)

请务必记住，继承仅从顶级向下移动(数据集→字段)，这意味着在字段级别应用的标签不会传播到其他字段或数据集。

## 在架构级别管理标签

您可以直接将标签添加到该架构中的一个或多个字段。 在架构级别应用的任何字段都将传播到基于该架构的所有数据集。

请参阅 [管理模式级别的标签](../../xdm/tutorials/labels.md) 以了解更多信息。

## 管理自定义标签 {#manage-custom-labels}

>[!CONTEXTUALHELP]
>id="platform_governance_createlabels"
>title="创建标签"
>abstract="通过标签，可根据适用于数据的使用策略将数据集和字段分类。Platform 提供了一组标准标签供您使用，但您也可以创建特定于您的组织的自定义标签。"

您可以在 **[!UICONTROL 策略]** 工作区 [!DNL Experience Platform] UI。 选择 **[!UICONTROL 策略]** 在左侧导航中，选择 **[!UICONTROL 标签]** 查看现有标签的列表。 从此处选择 **[!UICONTROL 创建标签]**.

![](../images/labels/create-label-btn.png)

的 **[!UICONTROL 创建标签]** 对话框。 从此处，为新标签提供以下信息：

* **[!UICONTROL 标识符]**:标签的唯一标识符。 此值用于查找目的，因此应简短明了。
* **[!UICONTROL 名称]**:标签的易记显示名称。
* **[!UICONTROL 描述]**:（可选）用于提供更多上下文的标签描述。

完成后，选择 **[!UICONTROL 创建]**.

![](../images/labels/create-label.png)

此时对话框将关闭，新创建的自定义标签将显示在 **[!UICONTROL 标签]** 选项卡。

![](../images/labels/label-created.png)

现在，可以在 **[!UICONTROL 自定义标签]** 编辑数据集和字段的使用情况标签时，或创建数据使用策略时。

<img src="../images/labels/add-custom-label.png" width="600" /><br>

## 后续步骤

现在，您已在数据集和字段级别添加了数据使用情况标签，接下来可以开始将数据摄取到 [!DNL Experience Platform]. 要了解更多信息，请首先阅读 [数据获取文档](../../ingestion/home.md).

您现在还可以根据已应用的标签定义数据使用策略。 有关更多信息，请参阅 [数据使用策略概述](../policies/overview.md).

## 其他资源

以下视频旨在支持您对“数据管理”的理解，并概述了如何将标签应用于数据集和各个字段。

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
