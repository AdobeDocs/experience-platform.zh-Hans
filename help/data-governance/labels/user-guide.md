---
keywords: Experience Platform；主页；热门主题；数据管理；数据使用标签；策略服务；数据使用标签用户指南
solution: Experience Platform
title: 在UI中管理数据使用标签
description: 本指南介绍了在Adobe Experience Platform用户界面中使用数据使用标签的步骤。
exl-id: aa44d5cc-416a-4ef2-be14-b4f32aec162c
source-git-commit: 663d1e20a7b8a56b1395047124fdf4b6fc3c214b
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 18%

---

# 在UI中管理数据使用标签 {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_description"
>title="在 Platform 中治理数据使用"
>abstract="<h2>描述</h2><p>通过 Experience Platform 中的数据治理框架，可根据数据使用限制为属性和架构加标签，以及设置标识特定营销活动并为其遵守这些限制的策略。</p>"

本用户指南介绍了在中使用数据使用标签的步骤。 [!DNL Experience Platform] 用户界面。

## 管理标签 {#manage-labels}

要将标签应用于数据，您需要 **[!UICONTROL 管理使用情况标签]** 对名为“prod”的默认生产沙盒的使用权限。 要创建自定义标签，您还必须对产品配置文件具有管理权限。 每个组织只有一个适用的标签列表，当前不支持删除标签。

请参阅指南，了解如何 [配置权限](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html) 或 [访问控制概述](../../access-control/home.md) 有关如何分配权限的更多信息。 如果您无权访问组织的Admin Console，请联系您的组织管理员。

## 在架构级别管理标签

您可以直接将标签添加到该架构中的一个或多个字段。 在架构级别应用的任何字段都将传播到基于该架构的所有数据集。

要在架构级别管理数据使用标签，您必须选择现有架构或创建新架构。 登录Adobe Experience Platform后，选择 **[!UICONTROL 架构]** 在左侧导航中打开 **[!UICONTROL 架构]** 工作区。 此页面列出了属于您组织的所有已创建方案，以及与每个方案相关的有用详细信息。

![突出显示了“架构”选项卡的Adobe Experience Platform UI。](../images/labels/schema-tab.png)

下一部分提供了创建新架构以将标签应用于其中的步骤。 如果要编辑现有架构的标签，请从列表中选择架构并跳至 [将数据使用标签添加到架构](#add-labels).

### 创建新架构

要创建新架构，请选择 **[!UICONTROL 创建架构]** 右上角的 **[!UICONTROL 架构]** 工作区。 请参阅指南，网址为 [如何使用架构编辑器创建架构](../../xdm/tutorials/create-schema-ui.md#create) 以获取完整的说明。 或者，您可以 [使用架构注册表API创建架构](../../xdm/tutorials/create-schema-api.md) 如果需要。

### 将数据使用标签添加到架构 {#add-labels-to-schema}

创建新架构，或从的列表中选择现有架构后 [!UICONTROL 浏览] 的选项卡 [!UICONTROL 架构] 在架构编辑器中，从架构中选择一个字段。 在 [!UICONTROL 字段属性] 侧栏，选择 **[!UICONTROL 应用访问和数据管理标签]**.

![架构工作区“结构”选项卡显示架构的可视化图表，其中突出显示了应用访问和数据管理标签。](../images/labels/schema-label-governance.png)

此时将显示一个对话框，允许您在架构级别和字段级别应用和管理数据使用标签。 有关以下内容的完整说明，请参阅XDM教程 [如何添加或编辑XDM架构的数据使用标签](../../xdm/tutorials/labels.md#select-schema-field).

### 向特定数据集添加数据使用标签 {#add-labels-to-dataset}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_instructions"
>title="说明"
>abstract="<ol><li>在左侧导航中选择<a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/user-guide.html?lang=zh-Hant">数据集</a>，然后选择要限制其数据的数据集。</li><li>从数据集详细信息视图中，选择<b>数据治理</b>选项卡。</li><li>选择要限制的数据集字段，然后选择<b>编辑治理标签</b>以根据使用限制为数据加标签。</li><li>为数据加标签后，在左侧导航中选择<a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=zh-Hans">策略</a>，然后选择<b>创建策略</b>。</li><li>选择创建一个<a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=zh-Hans#create-governance-policy">数据治理策略</a>，然后选择将应用于该策略的数据使用标签。</li><li>选择该策略将拒绝对任何包含这些标签的数据执行的营销操作。创建该策略后，从列表中选择它，然后使用右边栏中的切换开关启用它。</li><li>对于每个启用的策略，Platform 阻止将任何包含指定标签的数据用于所定义的营销操作。当您尝试对于具有关联的营销操作（用例）的目标激活加了标签的数据时，将自动施加此强制。</li></ol>"

>[!IMPORTANT]
>
>标签无法再应用于数据集级别的字段。 此工作流已弃用，支持在架构级别应用标签。 在2024年5月31日之前，之前在数据集对象级别应用的任何标签仍将通过Platform UI受到支持。 要确保您的标签在所有架构中保持一致，任何之前附加到数据集级别字段的标签，必须在未来一年中由您迁移到架构级别。 有关说明，请参阅文档 [如何将以前应用的标签从数据集迁移到架构级别](../e2e.md#migrate-labels).

标签可以应用于来自的整个数据集 **[!UICONTROL 数据管理]** 的选项卡 **[!UICONTROL 数据集]** 工作区。 工作区允许您在数据集级别管理数据使用标签。

![此 [!UICONTROL 数据管理] 的选项卡 [!UICONTROL 数据集] 突出显示了“数据管理”的工作区。](../images/labels/dataset-governance.png)

要在数据集级别编辑数据使用标签，请从选择铅笔图标(![铅笔图标。](../images/labels/edit-icon.png))的任意位置。

![此 [!UICONTROL 数据管理] 的选项卡 [!UICONTROL 数据集] 工作区中突出显示了编辑铅笔图标。](../images/labels/dataset-level-edit.png)

此 **[!UICONTROL 编辑治理标签]** 对话框打开。 在该对话框中，选中要应用于数据集的标签旁边的复选框。 请记住，这些标签将由数据集中的所有字段继承。 此 **[!UICONTROL 应用的标签]** 选中每个框时，标题都会更新，并显示您选择的标签。 选择所需的标签后，选择 **[!UICONTROL 保存更改]**.

![选中带有标签复选框和保存更改的“编辑治理标签”对话框。](../images/labels/apply-labels-dataset.png)

此 **[!UICONTROL 数据管理]** 工作区会重新显示，其中显示在表的初始行中已应用于数据集级别的标签。 您还可以看到标签，由各个信息卡指示，这些标签继承到数据集中的每个字段。

![此 [!UICONTROL 数据管理] 的选项卡 [!UICONTROL 数据集] 突出显示应用了数据集级别标签和继承的数据集字段标签的工作区。](../images/labels/applied-dataset-labels.png)

### 从数据集中删除标签 {#remove-labels-from-a-dataset}

在数据集级别添加的标签卡旁有“x”标记。 这允许您从整个数据集中删除标签。 每个字段旁边的继承标签旁边没有“x”，并且显示“灰显”。 这些 **继承的标签为只读**，这意味着无法在字段级别删除或编辑它们。

<!-- ## View labels at the dataset field level {#view-labels-at-dataset-field-level} -->

<!-- To view labels inherited by the dataset from the schema level, select **[!UICONTROL Datasets]** to navigate to the datasets workspace and select the relevant dataset from the list. 

![The Browse tab of the Datasets workspace with Datasets highlighted in the left sidebar.](../images/labels/dataset-navigation.png)

Next, select the **[!UICONTROL Data Governance]** tab to show the labels that have been applied to the dataset. You can also see that the labels are inherited down to each of the fields within the dataset.

![Dataset Labels inherited by fields](../images/labels/dataset-labels-applied.png)

The inherited labels beside each field do not have an "x" next to them and appear "greyed out" with no ability to remove or edit. This is because **inherited fields are read-only**, meaning they cannot be removed at the field level. -->

<!--Beleive can cut above here  -->

此 **[!UICONTROL 显示继承的标签]** 切换默认处于打开状态，允许您查看从架构继承到其字段的任何标签。 关闭切换会隐藏数据集中的任何继承标签。

![突出显示显示继承标签切换开关的数据集工作区的数据治理选项卡。](../images/labels/inherited-labels.png)

<!-- Labels applied to the dataset appear in read-only form within the **[!UICONTROL Data Governance]** view for that dataset. 

![The Data Governance tab of the Datasets workspace with labels highlighted.](../images/labels/read-only-governance-labels.png) -->

>[!NOTE]
>
>可以在数据集标签功能被弃用之前应用的标签，通过查找相关数据集并选择标签上的取消图标从数据集中删除。
>![突出显示可删除标签的数据集工作区的数据治理选项卡。](../images/labels/remove-governance-labels.png)
>有关说明，请参阅文档 [如何将以前应用的标签从数据集迁移到架构级别](../e2e.md#migrate-labels).

## 管理自定义标签 {#manage-custom-labels}

>[!CONTEXTUALHELP]
>id="platform_governance_createlabels"
>title="创建标签"
>abstract="通过标签，可根据适用于数据的使用策略将数据集和字段分类。Platform 提供了一组标准标签供您使用，但您也可以创建特定于您的组织的自定义标签。"

您可以在中创建自己的自定义使用标签 **[!UICONTROL 策略]** 中的工作区 [!DNL Experience Platform] UI。 选择 **[!UICONTROL 策略]** 在左侧导航中，然后选择 **[!UICONTROL 标签]** 查看现有标签的列表。 从此处选择 **[!UICONTROL 创建标签]**.

![突出显示了创建策略的策略工作区。](../images/labels/create-label-btn.png)

此 **[!UICONTROL 创建标签]** 对话框。 从这里，为新标签提供以下信息：

* **[!UICONTROL 名称]**：标签的唯一标识符。 此值用于查找目的，因此应简明扼要。
* **[!UICONTROL 友好名称]**：标签的友好显示名称。
* **[!UICONTROL 描述]**：（可选）用于提供进一步上下文的标签描述。

完成后，选择 **[!UICONTROL 创建]**.

![策略工作区的“创建标签”对话框突出显示“创建”。](../images/labels/create-label-dialog.png)

对话框随即关闭，新建的自定义标签将显示在 **[!UICONTROL 标签]** 选项卡。

![突出显示了新自定义标签的“策略”工作区的“标签”选项卡。](../images/labels/label-created.png)

现在可以选择以下位置的标签 **[!UICONTROL 自定义标签]** 编辑数据集和字段的使用标签，或创建数据使用策略时。

![突出显示自定义标签的应用访问和数据管理标签对话框。](../images/labels/add-custom-label.png)

## 后续步骤

现在，您已在数据集和字段级别添加数据使用标签，接下来可以开始将数据摄取到 [!DNL Experience Platform]. 要了解更多信息，请从阅读 [数据摄取文档](../../ingestion/home.md).

您现在还可以根据已应用的标签定义数据使用策略。 欲了解更多信息，请参见 [数据使用策略概述](../policies/overview.md).

<!-- The workflow of this video is now outdated. This can be enabled once the video has been updated

## Additional resources

The following video is intended to support your understanding of Data Governance, and outlines how to apply labels to a dataset and individual fields.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on) -->
