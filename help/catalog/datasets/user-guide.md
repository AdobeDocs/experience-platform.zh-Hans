---
keywords: Experience Platform；主页；热门主题；启用数据集；数据集；数据集
solution: Experience Platform
title: 数据集用户指南
topic: datasets
description: 本数据集用户指南提供了有关在Adobe Experience Platform用户界面内处理数据集时执行常见操作的说明。
translation-type: tm+mt
source-git-commit: d2ace7cadb06f77bdf14b6a4ef83e879c4ca88fd
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 0%

---


# 数据集用户指南

本用户指南提供了在Adobe Experience Platform用户界面内处理数据集时执行常见操作的说明。

## 入门指南

本用户指南要求您对Adobe Experience Platform的以下组件有充分的了解：

* [数据集](overview.md):存储和管理结构，用于数据持久性 [!DNL Experience Platform]。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成基础](../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器](../../xdm/tutorials/create-schema-ui.md):了解如何使用用户界面内的自定义 [!DNL Schema Editor] XDM [!DNL Platform] 模式。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md):确保遵守有关使用客户数据的法规、限制和政策。

## 视图数据集

在[!DNL Experience Platform] UI中，单击左侧导航中的&#x200B;**[!UICONTROL 数据集]**&#x200B;以打开&#x200B;**[!UICONTROL 数据集]**&#x200B;仪表板。 仪表板列表组织的所有可用数据集。 将显示每个列出的数据集的详细信息，包括其名称、数据集所附的模式以及最新摄取运行的状态。

![](../images/datasets/user-guide/browse_datasets.png)

单击数据集的名称以访问其&#x200B;**[!UICONTROL 数据集活动]**&#x200B;屏幕并查看您选择的数据集的详细信息。 “活动”选项卡包括一个图，该图可视化消息消耗率，以及成功和失败批的列表。

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## 预览数据集

在&#x200B;**[!UICONTROL 数据集活动]**&#x200B;屏幕中，单击屏幕右上角附近的&#x200B;**[!UICONTROL 预览数据集]**&#x200B;预览最多100行数据。 如果预览集为空，则预览链接将停用，而是表示该数据集不可用。

![](../images/datasets/user-guide/click_to_preview.png)

在预览窗口中，右侧显示数据集模式的层次视图。

![](../images/datasets/user-guide/preview_dataset.png)

要获得更可靠的数据访问方法，[!DNL Experience Platform]提供下游服务，如[!DNL Query Service]和[!DNL JupyterLab]来浏览和分析数据。 有关更多信息，请参阅以下文档:

* [查询服务概述](../../query-service/home.md)
* [JupyterLab用户指南](../../data-science-workspace/jupyterlab/overview.md)

## 创建数据集{#create}

要创建新数据集，请单击&#x200B;**[!UICONTROL 数据集]**&#x200B;开始仪表板中的&#x200B;**[!UICONTROL 创建数据集]**。

![](../images/datasets/user-guide/click_to_create.png)

在下一个屏幕中，您将看到以下两个用于创建新数据集的选项：

* [从模式创建数据集](#schema)
* [通过CSV文件创建数据集](#csv)

### 使用现有模式{#schema}创建数据集

在&#x200B;**[!UICONTROL 创建数据集]**&#x200B;屏幕中，单击&#x200B;**[!UICONTROL 从模式]**&#x200B;创建数据集以创建新的空数据集。

![](../images/datasets/user-guide/create_dataset_schema.png)

出现&#x200B;**[!UICONTROL 选择模式]**&#x200B;步骤。 在单击&#x200B;**[!UICONTROL Next]**&#x200B;之前，浏览模式列表并选择数据集将遵循的模式。

![](../images/datasets/user-guide/select_schema.png)

出现&#x200B;**[!UICONTROL 配置数据集]**&#x200B;步骤。 为数据集提供名称和可选说明，然后单击&#x200B;**[!UICONTROL 完成]**&#x200B;以创建数据集。

![](../images/datasets/user-guide/configure_dataset_schema.png)

### 使用CSV文件{#csv}创建数据集

使用CSV文件创建数据集时，会创建一个专门模式，以为数据集提供与提供的CSV文件匹配的结构。 在&#x200B;**[!UICONTROL 创建数据集]**&#x200B;屏幕中，单击标有&#x200B;**[!UICONTROL 从CSV文件创建数据集]**&#x200B;的框。

![](../images/datasets/user-guide/create_dataset_csv.png)

出现&#x200B;**[!UICONTROL 配置]**&#x200B;步骤。 为数据集提供名称和可选说明，然后单击&#x200B;**[!UICONTROL 下一步]**。

![](../images/datasets/user-guide/configure_dataset_csv.png)

出现&#x200B;**[!UICONTROL 添加数据]**&#x200B;步骤。 通过将CSV文件拖放到屏幕的中心来上传该文件，或单击&#x200B;**[!UICONTROL 浏览]**&#x200B;浏览文件目录。 文件最大可为10GB。 上传CSV文件后，单击&#x200B;**[!UICONTROL 保存]**&#x200B;以创建数据集。

>[!NOTE]
>
>CSV列名必须与字母数字字符开始，并且只能包含字母、数字和下划线。

![](../images/datasets/user-guide/add_csv_data.png)

## 为实时客户用户档案启用数据集

每个数据集都能用摄取的数据丰富客户用户档案。 要这样做，数据集附带的模式必须兼容，才能在[!DNL Real-time Customer Profile]中使用。 兼容模式满足以下要求：

* 该模式至少具有一个指定为标识属性的属性。
* 模式具有定义为主标识的标识属性。

有关为[!DNL Profile]启用模式的详细信息，请参阅[模式编辑器用户指南](../../xdm/tutorials/create-schema-ui.md)。

要启用用户档案集，请访问其&#x200B;**[!UICONTROL 数据集活动]**&#x200B;屏幕，然后单击&#x200B;**[!UICONTROL 用户档案]**&#x200B;在&#x200B;**[!UICONTROL 属性]**&#x200B;列中切换。 启用后，引入数据集中的数据也将用于填充客户用户档案。

>[!NOTE]
>
>如果数据集已包含数据，然后启用[!DNL Profile]，则[!DNL Profile]不会自动消耗现有数据。 在为[!DNL Profile]启用数据集后，建议您重新摄取任何现有数据，让其贡献给客户用户档案。

![](../images/datasets/user-guide/enable_dataset_profiles.png)

## 管理并强制对数据集进行数据管理

数据使用标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 请参见[数据管理概述](../../data-governance/home.md)了解有关标签的更多信息，或参阅[数据使用标签用户指南](../../data-governance/labels/overview.md)了解如何将标签应用到数据集的说明。

## 删除数据集

您可以先访问数据集的&#x200B;**[!UICONTROL 活动集]**&#x200B;屏幕，删除数据集。 然后，单击&#x200B;**[!UICONTROL 删除数据集]**&#x200B;以将其删除。

>[!NOTE]
>
>无法删除由Adobe应用程序和服务(如Adobe Analytics、Adobe Audience Manager或[!DNL Offer Decisioning])创建和利用的数据集。

![](../images/datasets/user-guide/delete_dataset.png)

将显示确认框。 单击&#x200B;**[!UICONTROL 删除]**&#x200B;以确认删除数据集。

![](../images/datasets/user-guide/confirm_delete.png)

## 删除启用用户档案的数据集

如果[!DNL Profile]启用了数据集，则通过UI删除该数据集将从Data Lake和Platform中的用户档案存储中删除它。

您只能使用实时客户用户档案API从[!DNL Profile]存储中删除数据集（将数据保留在数据湖中）。 有关详细信息，请参阅[用户档案系统作业API端点指南](../../profile/api/profile-system-jobs.md)。

## 监控数据获取

在[!DNL Experience Platform] UI中，单击左侧导航中的&#x200B;**[!UICONTROL 监视]**。 通过&#x200B;**[!UICONTROL 监视]**&#x200B;仪表板，可以视图来自批处理或流式摄取的入站数据的状态。 要视图单个批的状态，请单击&#x200B;**[!UICONTROL 批端到端]**&#x200B;或&#x200B;**[!UICONTROL 流端到端]**。 仪表板列表所有批处理或流式摄取运行，包括成功、失败或仍在进行的运行。 每个列表都提供批的详细信息，包括批ID、目标数据集的名称和摄取的记录数。 如果为[!DNL Profile]启用目标数据集，则还会显示所摄取的身份和用户档案记录数。

![](../images/datasets/user-guide/batch_listing.png)

单击单个&#x200B;**[!UICONTROL 批ID]**&#x200B;可访问&#x200B;**[!UICONTROL 批概述]**&#x200B;仪表板并查看该批的详细信息，包括当该批未能收录时的错误日志。

![](../images/datasets/user-guide/batch_overview.png)

如果要删除批，可以单击仪表板右上方附近的&#x200B;**[!UICONTROL 删除批]**。 这样做还会从最初摄取批次的数据集中删除其记录。

![](../images/datasets/user-guide/delete_batch.png)

## 后续步骤

本用户指南提供了有关在[!DNL Experience Platform]用户界面中处理数据集时执行常见操作的说明。 有关执行涉及数据集的常见[!DNL Platform]工作流的步骤，请参阅以下教程：

* [使用API创建数据集](create.md)
* [查询数据集数据（使用Data Access API）](../../data-access/home.md)
* [使用API为实时客户用户档案和身份服务配置数据集](../../profile/tutorials/dataset-configuration.md)