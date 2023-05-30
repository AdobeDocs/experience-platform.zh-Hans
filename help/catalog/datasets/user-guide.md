---
keywords: Experience Platform；主页；热门主题；启用数据集；数据集；数据集
solution: Experience Platform
title: 数据集UI指南
description: 了解如何在Adobe Experience Platform用户界面中使用数据集时执行常见操作。
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: 11d6cf09dede8c7c14bbbcd3c109e703a5d053de
workflow-type: tm+mt
source-wordcount: '1504'
ht-degree: 7%

---

# 数据集UI指南

本用户指南提供有关在Adobe Experience Platform用户界面中使用数据集时执行常见操作的说明。

## 快速入门

本用户指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [数据集](overview.md)：用于数据持久化的存储和管理结构 [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器](../../xdm/tutorials/create-schema-ui.md)：了解如何使用构建自己的自定义XDM架构 [!DNL Schema Editor] 在 [!DNL Platform] 用户界面。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md)：确保遵守有关使用客户数据的法规、限制和策略。

## 查看数据集 {#view-datasets}

>[!CONTEXTUALHELP]
>id="platform_datasets_negative_numbers"
>title="数据集活动中的负数"
>abstract="摄取的记录中的负数表示用户已删除选定时间范围内的某些批次。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_datasets_browse_daysRemaining"
>title="数据集过期"
>abstract="此列指示目标数据集在自动过期前剩余的天数。"

在 [!DNL Experience Platform] UI，选择 **[!UICONTROL 数据集]** 在左侧导航中打开 **[!UICONTROL 数据集]** 仪表板。 仪表板列出您组织的所有可用数据集。 会显示每个列出数据集的详细信息，包括其名称、数据集所遵循的架构以及最近摄取运行的状态。

![一个图像，突出显示左侧导航栏中的“数据集”项目。](../images/datasets/user-guide/browse-datasets.png)

默认情况下，只会显示已摄取到的数据集。如果要查看系统生成的数据集，请启用 **[!UICONTROL 显示系统数据集]** 切换。 系统生成的数据集仅用于处理其他组件。 例如，系统生成的配置文件导出数据集用于处理配置文件仪表板。

![用于选择是否应显示系统数据集的切换会高亮显示。](../images/datasets/user-guide/system-datasets.png)

选择数据集名称以访问其 **[!UICONTROL 数据集活动]** 屏幕并查看选定数据集的详细信息。 活动选项卡包含一个图表，其中可查看消息使用率，以及成功批次和失败批次的列表。

![选定数据集的详细信息会突出显示。](../images/datasets/user-guide/dataset-activity-1.png)
![属于选定数据集的示例批次会突出显示。](../images/datasets/user-guide/dataset-activity-2.png)

## 预览数据集

从 **[!UICONTROL 数据集活动]** 屏幕，选择 **[!UICONTROL 预览数据集]** 在屏幕的右上角附近，最多可预览100行数据。 如果数据集为空，预览链接将被停用，并改为表示预览不可用。

![预览数据集按钮突出显示。](../images/datasets/user-guide/select-preview.png)

在预览窗口中，数据集的架构的分层视图显示在右侧。

![此时将显示数据集的预览。 显示了有关结构以及示例值的信息。](../images/datasets/user-guide/preview-dataset.png)

要获得更可靠的数据访问方法， [!DNL Experience Platform] 提供下游服务，例如 [!DNL Query Service] 和 [!DNL JupyterLab] 探索和分析数据。 有关更多信息，请参阅以下文档：

* [查询服务概述](../../query-service/home.md)
* [JupyterLab用户指南](../../data-science-workspace/jupyterlab/overview.md)

## 创建数据集 {#create}

要创建新数据集，请首先选择“数据集”仪表板中的&#x200B;**[!UICONTROL 创建数据集]**。****

![创建数据集按钮会突出显示。](../images/datasets/user-guide/select-create.png)

在下一个屏幕中，您将看到以下两个用于创建新数据集的选项：

* [使用模式创建数据集。](#schema)
* [从CSV文件创建数据集](#csv)

### 使用现有架构创建数据集 {#schema}

在 **[!UICONTROL 创建数据集]** 屏幕，选择 **[!UICONTROL 从架构创建数据集]** 以创建新的空数据集。

![突出显示了从架构创建数据集按钮。](../images/datasets/user-guide/create-dataset-schema.png)

此 **[!UICONTROL 选择架构]** 步骤。 浏览架构列表并选择数据集将遵循的架构，然后再选择 **[!UICONTROL 下一个]**.

![将显示架构列表。 将用于创建数据集的架构会突出显示。](../images/datasets/user-guide/select-schema.png)

此 **[!UICONTROL 配置数据集]** 步骤。 为数据集提供名称和可选描述，然后选择 **[!UICONTROL 完成]** 以创建数据集。

![插入数据集的配置详细信息。 这包括数据集名称和描述等详细信息。](../images/datasets/user-guide/configure-dataset-schema.png)

### 使用CSV文件创建数据集 {#csv}

使用CSV文件创建数据集时，将创建一个临时架构，以便为数据集提供与提供的CSV文件匹配的结构。 在 **[!UICONTROL 创建数据集]** 屏幕，选择 **[!UICONTROL 从CSV文件创建数据集]**.

![突出显示了从CSV文件创建数据集按钮。](../images/datasets/user-guide/create-dataset-csv.png)

此 **[!UICONTROL 配置]** 步骤。 为数据集提供名称和可选描述，然后选择 **[!UICONTROL 下一个]**.

![插入数据集的配置详细信息。 这包括数据集名称和描述等详细信息。](../images/datasets/user-guide/configure-dataset-csv.png)

此 **[!UICONTROL 添加数据]** 步骤。 通过将CSV文件拖放到屏幕的中心来上传该文件，或者选择 **[!UICONTROL 浏览]** 浏览您的文件目录。 文件大小最多可达10 GB。 上传CSV文件后，选择 **[!UICONTROL 保存]** 以创建数据集。

>[!NOTE]
>
>CSV列名称必须以字母数字字符开头，并且只能包含字母、数字和下划线。

![此时将显示“添加数据”屏幕。 您可以为数据集上传CSV文件的位置会突出显示。](../images/datasets/user-guide/add-csv-data.png)

## 为Real-time Customer Profile启用数据集 {#enable-profile}

每个数据集都能够使用其摄取的数据扩充客户用户档案。 要实现此目的，数据集所遵循的架构必须兼容才能在中使用 [!DNL Real-Time Customer Profile]. 兼容模式满足以下要求：

* 架构至少有一个指定为标识属性的属性。
* 架构具有被定义为主标识的标识属性。

有关启用架构的详细信息 [!DNL Profile]，请参见 [架构编辑器用户指南](../../xdm/tutorials/create-schema-ui.md).

要为配置文件启用数据集，请访问其 **[!UICONTROL 数据集活动]** 屏幕并选择 **[!UICONTROL 个人资料]** 在中切换 **[!UICONTROL 属性]** 列。 启用后，摄取到数据集中的数据也将用于填充客户个人资料。

>[!NOTE]
>
>如果数据集已包含数据，然后启用 [!DNL Profile]，则现有数据不会自动由使用 [!DNL Profile]. 为以下项启用数据集后 [!DNL Profile]，建议您重新摄取任何现有数据，以使其贡献给客户档案。

![配置文件切换在数据集详细信息页面中突出显示。](../images/datasets/user-guide/enable-dataset-profiles.png)

## 管理和实施数据集上的数据治理 {#manage-and-enforce-data-governance}

在架构级别应用的数据使用标签，允许您根据应用于该数据的使用策略对数据集和字段进行分类。 请参阅 [数据治理概述](../../data-governance/home.md) 要了解有关标签的更多信息，或参阅 [数据使用标签用户指南](../../data-governance/labels/overview.md) 有关如何将标签应用于架构以便传播到数据集的说明。

## 删除数据集 {#delete}

您可以先访问某个数据集的 **[!UICONTROL 数据集活动]** 屏幕。 然后，选择 **[!UICONTROL 删除数据集]** 删除它。

>[!NOTE]
>
>由Adobe应用程序和服务(如Adobe Analytics、Adobe Audience Manager或 [!DNL Offer Decisioning])无法删除。

![“删除数据集”按钮会在数据集详细信息页面中突出显示。](../images/datasets/user-guide/delete-dataset.png)

将出现一个确认框。 选择 **[!UICONTROL 删除]** 以确认删除数据集。

![将显示删除的确认模式，并突出显示删除按钮。](../images/datasets/user-guide/confirm-delete.png)

## 删除启用配置文件的数据集

如果为配置文件启用了某个数据集，则通过UI删除该数据集会将其从数据湖、Identity Service以及Platform中的配置文件存储中删除。

您可以从中删除数据集 [!DNL Profile] 使用实时客户个人资料API仅存储（将数据保留在数据湖中）。 欲了解更多信息，请参见 [配置文件系统作业API端点指南](../../profile/api/profile-system-jobs.md).

## 监测数据提取

在 [!DNL Experience Platform] UI，选择 **[!UICONTROL 监测]** 左侧导航栏中。 此 **[!UICONTROL 监测]** 通过仪表板，可查看来自批量摄取或流式摄取的集客数据的状态。 要查看各个批的状态，请选择 **[!UICONTROL 批量端到端]** 或 **[!UICONTROL 端到端的流式传输]**. 仪表板会列出所有批次或流式摄取运行，包括成功、失败或仍在进行的批次或流式摄取运行。 每个列表都提供批次的详细信息，包括批次ID、目标数据集的名称和摄取的记录数。 如果为目标数据集启用了 [!DNL Profile]，也会显示摄取的身份和配置文件记录数。

![此时将显示监控批次的端到端屏幕。 监视和批量处理都突出显示。](../images/datasets/user-guide/batch-listing.png)

您可以选择个人 **[!UICONTROL 批次ID]** 以访问 **[!UICONTROL 批次概述]** 仪表板，查看批次的详细信息，包括批次摄取失败时的错误日志。

![此时将显示选定批次的详细信息。 这包括摄取的记录数、失败的记录数、批次状态、文件大小、摄取的开始和结束时间、数据集和批次ID、组织ID、数据集名称和访问信息。](../images/datasets/user-guide/batch-overview.png)

如果要删除批次，可以通过选择 **[!UICONTROL 删除批次]** 在仪表板的右上角附近找到。 这样做还会从最初引入批次的数据集中删除其记录。

![“数据集详细信息”页面上会高亮显示删除批次按钮。](../images/datasets/user-guide/delete-batch.png)

## 后续步骤

本用户指南提供了在中处理数据集时执行常用操作的说明。 [!DNL Experience Platform] 用户界面。 有关执行常见操作的步骤 [!DNL Platform] 涉及数据集的工作流，请参阅以下教程：

* [使用API创建数据集](create.md)
* [使用数据访问API查询数据集数据](../../data-access/home.md)
* [使用API为Real-time Customer Profile和Identity Service配置数据集](../../profile/tutorials/dataset-configuration.md)
