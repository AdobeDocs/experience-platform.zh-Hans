---
keywords: Experience Platform;home;popular topics;enable dataset;Dataset;dataset
solution: Experience Platform
title: 数据集用户指南
topic: datasets
description: 本数据集用户指南提供了有关在Adobe Experience Platform用户界面内处理数据集时执行常见操作的说明。
translation-type: tm+mt
source-git-commit: 43d568a401732a753553847dee1b4a924fcc24fd
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 0%

---


# 数据集用户指南

本用户指南提供了在Adobe Experience Platform用户界面内处理数据集时执行常见操作的说明。

## 入门指南

本用户指南要求您对Adobe Experience Platform的以下组件有充分的了解：

* [数据集](overview.md):存储和管理结构，用于数据持久性 [!DNL Experience Platform]。
* [[!DNL体验数据模型(XDM)系统]](../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成基础](../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器](../../xdm/tutorials/create-schema-ui.md):了解如何使用用户界面内的自定义XDM [!DNL Schema Editor] 模式 [!DNL Platform] 构建自己。
* [[!DNL实时客户用户档案]](../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [[!DNL数据管理]](../../data-governance/home.md):确保遵守有关使用客户数据的法规、限制和政策。

## 视图数据集

在UI [!DNL Experience Platform] 中，单击左 **[!UICONTROL 侧导航]** 中的数据集以打开 *[!UICONTROL 数据集]* 仪表板。 仪表板列表组织的所有可用数据集。 将显示每个列出的数据集的详细信息，包括其名称、数据集所附的模式以及最新摄取运行的状态。

![](../images/datasets/user-guide/browse_datasets.png)

单击数据集的名称以访问其“数 *[!UICONTROL 据集活动]* ”屏幕，并查看所选数据集的详细信息。 “活动”选项卡包括一个图，该图可视化消息消耗率，以及成功和失败批的列表。

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## 预览数据集

在“ *[!UICONTROL 活动]* ”屏幕中，单 **[!UICONTROL 击屏幕右上角附近的]** “预览数据集”以预览最多100行数据。 如果预览集为空，则预览链接将被取消激活，而是表示 **[!UICONTROL 不可用]**。

![](../images/datasets/user-guide/click_to_preview.png)

在预览窗口中，右侧显示数据集模式的层次视图。

![](../images/datasets/user-guide/preview_dataset.png)

要获得更可靠的数据访问方法， [!DNL Experience Platform] 请提供下游服务， [!DNL Query Service] 如 [!DNL JupyterLab] 探索和分析数据。 有关更多信息，请参阅以下文档:

* [查询服务概述](../../query-service/home.md)
* [JupyterLab用户指南](../../data-science-workspace/jupyterlab/overview.md)

## 创建数据集 {#create}

要创建新数据集，请单击“数据集” **[!UICONTROL 开始中的]** “创建 *[!UICONTROL 数据集]* ”。

![](../images/datasets/user-guide/click_to_create.png)

在下一个屏幕中，您将看到以下两个用于创建新数据集的选项：

* [从模式创建数据集](#create-a-dataset-with-an-existing-schema)
* [通过CSV文件创建数据集](#create-a-dataset-with-a-csv-file)

### 使用现有模式创建数据集

在“创 *[!UICONTROL 建数据集]* ”屏幕中，单 **[!UICONTROL 击“从模式创建数据集]** ”以创建新的空数据集。

![](../images/datasets/user-guide/create_dataset_schema.png)

将出 *[!UICONTROL 现“选择模式]* ”(Select Sect)步骤。 浏览模式列表，选择数据集将遵循的模式，然后单击“下 **[!UICONTROL 一步”]**。

![](../images/datasets/user-guide/select_schema.png)

将显 *[!UICONTROL 示配置数据集]* 步骤。 为数据集提供名称和可选描述，然后单 **[!UICONTROL 击]** “完成”创建数据集。

![](../images/datasets/user-guide/configure_dataset_schema.png)

### 使用CSV文件创建数据集

使用CSV文件创建数据集时，会创建一个专门模式，以为数据集提供与提供的CSV文件匹配的结构。 在“创 *[!UICONTROL 建数据集]* ”屏幕中，单击“从CSV文 **[!UICONTROL 件创建数据集”框]**。

![](../images/datasets/user-guide/create_dataset_csv.png)

将显 *[!UICONTROL 示]* “配置”步骤。 为数据集提供名称和可选说明，然后单击“下 **[!UICONTROL 一步]**”。

![](../images/datasets/user-guide/configure_dataset_csv.png)

将出 *[!UICONTROL 现添加数]* 据步骤。 通过将CSV文件拖放到屏幕的中心，或单击“浏览 **[!UICONTROL ”]** ，浏览文件目录。 文件最大可为10GB。 上传CSV文件后，单击“ **[!UICONTROL 保存]** ”以创建数据集。

>[!NOTE]
>
>CSV列名必须与字母数字字符开始，并且只能包含字母、数字和下划线。

![](../images/datasets/user-guide/add_csv_data.png)

## 为实时客户用户档案启用数据集

每个数据集都能用摄取的数据丰富客户用户档案。 为此，数据集附带的模式必须兼容才能在中使用 [!DNL Real-time Customer Profile]。 兼容模式满足以下要求：

* 该模式至少具有一个指定为标识属性的属性。
* 模式具有定义为主标识的标识属性。

有关为模式启用的详细 [!DNL Profile]信息，请参 [阅模式编辑器用户指南](../../xdm/tutorials/create-schema-ui.md)。

要启用用户档案集，请访问其“数 *[!UICONTROL 据集活动]* ”屏幕，然后单 **[!UICONTROL 击“属性]** ”列中的 *[!UICONTROL “用户档案”切]* 换。 启用后，引入数据集中的数据也将用于填充客户用户档案。

![](../images/datasets/user-guide/enable_dataset_profiles.png)

如果数据集已包含数据，然后启 [!DNL Profile]用该数据集，则现有数据不会被占 [!DNL Profile]用。 启用数据集后， [!DNL Profile]建议您重新摄取任何现有数据，让其填充客户用户档案。

## 管理并强制对数据集进行数据管理

数据使用标签和执行(DULE)是核心的数据治理机制 [!DNL Experience Platform]。 DULE标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 请参阅数 [据管理概述](../../data-governance/home.md) ，进一步了解标签 [，或参阅数据使用标签用户指南](../../data-governance/labels/overview.md) ，了解如何将标签应用到数据集。

## 删除数据集

您可以先访问数据集活动屏幕， *[!UICONTROL 删除数据集]* 。 然后，单击 **[!UICONTROL 删除数据集]** ，以将其删除。

>[!NOTE]
>
>无法删除由Adobe应用程序和服务(如Adobe Analytics、Adobe Audience Manager或)创建和 [!DNL Decisioning Service]利用的数据集。

![](../images/datasets/user-guide/delete_dataset.png)

将显示确认框。 单击 **[!UICONTROL 删除]** ，以确认删除数据集。

![](../images/datasets/user-guide/confirm_delete.png)

## 删除启用用户档案的数据集

如果启用了数据集， [!DNL Profile]则通过UI删除该数据集将禁用数据集以进行摄取，但不会自动在后端删除数据集。 为了完全删除数据集，包括它提供的用户档案和身份数据，必须另外发出删除请求。 有关如何从存储中正确删除数 [!DNL Profile] 据的步骤，请参 [!DNL Real-time Customer Profile] 阅 [用户档案系统作业的API子指南，也称为“删除请求”](../../profile/api/profile-system-jobs.md)。

## 监控数据获取

在UI [!DNL Experience Platform] 中，单击左 **[!UICONTROL 侧导]** 航中的“监视”。 通过 *[!UICONTROL 监视仪表板]* ，您可以视图来自批处理或流式摄取的入站数据的状态。 要视图单个批的状态，请 *[!UICONTROL 单击“批端到端]* ” *[!UICONTROL 或“流端到端”]*。 仪表板列表所有批处理或流式摄取运行，包括成功、失败或仍在进行的运行。 每个列表都提供批的详细信息，包括批ID、目标数据集的名称和摄取的记录数。 如果为目标数据集启 [!DNL Profile]用，则还会显示所摄取的身份和用户档案记录数。

![](../images/datasets/user-guide/batch_listing.png)

您可以单击单个批 **[!UICONTROL ID]** ，访问批 *[!UICONTROL 概述仪表板并查看该批的详细信息]* ，包括当该批未能收录时的错误日志。

![](../images/datasets/user-guide/batch_overview.png)

如果要删除批，可以单击仪表板右上方 **[!UICONTROL 的“删除]** ”批。 这样做还会从最初摄取批次的数据集中删除其记录。

![](../images/datasets/user-guide/delete_batch.png)

## 后续步骤

本用户指南提供了有关在用户界面中处理数据集时执行常见操作 [!DNL Experience Platform] 的说明。 有关执行涉及数据集 [!DNL Platform] 的常见工作流的步骤，请参阅以下教程：

* [使用API创建数据集](create.md)
* [查询数据集数据（使用Data Access API）](../../data-access/home.md)
* [使用API为实时客户用户档案和身份服务配置数据集](../../profile/tutorials/dataset-configuration.md)