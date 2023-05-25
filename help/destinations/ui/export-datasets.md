---
title: （测试版）将数据集导出到云存储目标
type: Tutorial
description: 了解如何将数据集从Adobe Experience Platform导出到您首选的云存储位置。
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: d0de642eb6118e6597925c12c76917ffa98c3a5a
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 5%

---

# （测试版）将数据集导出到云存储目标

>[!IMPORTANT]
>
>* 导出数据集的功能当前为测试版，并非对所有用户都可用。 文档和功能可能会发生变化。
>* 此测试版功能支持导出第一代数据，如Real-time Customer Data Platform中所定义 [产品描述](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
>* 已购买Real-Time CDP Prime和Ultimate软件包的客户可以使用此功能。 有关更多信息，请联系您的Adobe代表。


本文说明了导出所需的工作流 [数据集](/help/catalog/datasets/overview.md) 从Adobe Experience Platform到您的首选云存储位置，例如 [!DNL Amazon S3]、 SFTP位置或 [!DNL Google Cloud Storage] 通过使用Experience PlatformUI。

您还可以使用Experience PlatformAPI导出数据集。 阅读 [导出数据集API教程](/help/destinations/api/export-datasets.md) 了解更多信息。

## 支持的目标 {#supported-destinations}

目前，您可以将数据集导出到屏幕快照中突出显示的云存储目标，如下所列。

![支持数据集导出的目标](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## 何时激活区段或导出数据集 {#when-to-activate-segments-or-activate-datasets}

Experience Platform目录中的一些基于文件的目标同时支持区段激活和数据集导出。

* 当您希望将数据结构化为按受众兴趣或资格分组的用户档案时，请考虑激活区段。
* 或者，在要导出未按受众兴趣或资格进行分组或构建的原始数据集时，请考虑数据集导出。 您可以将此数据用于报告、数据科学工作流、满足合规性要求以及许多其他用例。

本文档包含导出数据集所需的所有信息。 如果要将区段激活到云存储或电子邮件营销目标，请阅读 [将受众数据激活到批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md).

## 先决条件 {#prerequisites}

要将数据集导出到云存储目标，您必须已成功完成 [已连接到目标](./connect-destination.md). 如果您尚未这样做，请转到 [目标目录](../catalog/overview.md)，浏览支持的目标，并配置要使用的目标。

### 所需权限 {#permissions}

要导出数据集，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**、和 **[!UICONTROL 管理和激活数据集目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要确保您具有导出数据集的必要权限并且目标支持导出数据集，请浏览目标目录。 如果目标具有 **[!UICONTROL 激活]** 或 **[!UICONTROL 导出数据集]** 则您具有相应的权限。

## 选择您的目标 {#select-destination}

按照相关说明选择导出数据集的目标：

1. 转到 **[!UICONTROL 连接>目标]**，并选择 **[!UICONTROL 目录]** 选项卡。

   ![突出显示目录控件的目标目录选项卡。](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. 选择 **[!UICONTROL 激活]** 或 **[!UICONTROL 导出数据集]** 在与要将数据集导出到的目标对应的信息卡上。

   ![突出显示了“激活”控件的目标目录选项卡。](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. 选择 **[!UICONTROL 数据类型数据集]** 并选择要将数据集导出到的目标连接，然后选择 **[!UICONTROL 下一个]**.

>[!TIP]
> 
>如果要设置新目标以导出数据集，请选择 **[!UICONTROL 配置新目标]** 触发 [连接到目标](/help/destinations/ui/connect-destination.md) 工作流。

![突出显示数据集控件的目标激活工作流。](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. 此 **[!UICONTROL 选择数据集]** 视图。 继续下一节至 [选择数据集](#select-datasets) 以导出。

## 选择您的数据集 {#select-datasets}

使用数据集名称左侧的复选框选择要导出到目标的数据集，然后选择 **[!UICONTROL 下一个]**.

![数据集导出工作流程显示“选择数据集”步骤，您可以在其中选择要导出的数据集。](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## 计划数据集导出 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="数据集的文件导出选项"
>abstract="选择&#x200B;**导出增量文件**&#x200B;以仅导出自上次导出后添加到数据集的数据。<br>第一个增量文件导出包括数据集中的所有数据，充当回填。后续增量文件仅包含自第一次导出后添加到数据集的数据。"

在 **[!UICONTROL 计划]** 步骤，您可以设置数据集导出的开始日期和导出节奏。

此 **[!UICONTROL 导出增量文件]** 选项。 这会触发导出，其中第一个文件是数据集的完整快照，后续文件是自上次导出以来向数据集添加的增量文件。

>[!IMPORTANT]
>
>第一个导出的增量文件包含数据集中的所有现有数据，充当回填。

![显示计划步骤的数据集导出工作流。](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. 使用 **[!UICONTROL 频率]** 选择器以选择导出频率：

   * **[!UICONTROL 每日]**：计划每天在指定的时间导出一次增量文件。
   * **[!UICONTROL 每小时]**：计划每3、6、8或12小时导出一次增量文件。

2. 使用 **[!UICONTROL 时间]** 选择器以选择一天中的时间，在 [!DNL UTC] 格式，应何时进行导出。

3. 使用 **[!UICONTROL 日期]** 选择器来选择应进行导出的时间间隔。 请注意，在该功能的测试版中，无法设置导出的结束日期。 有关详细信息，请查看 [已知限制](#known-limitations) 部分。

4. 选择 **[!UICONTROL 下一个]** 保存计划并转到 **[!UICONTROL 审核]** 步骤。

>[!NOTE]
> 
>对于数据集导出，文件名具有无法修改的预设默认格式。 请参阅部分 [验证是否成功导出数据集](#verify) 有关导出的文件的更多信息和示例。

## 请查看 {#review}

在 **[!UICONTROL 审核]** 页面时，您可以看到所选内容的摘要。 选择 **[!UICONTROL 取消]** 来打破气流， **[!UICONTROL 返回]** 修改设置，或者 **[!UICONTROL 完成]** 以确认您的选择并开始将数据集导出到目标。

![显示审核步骤的数据集导出工作流。](/help/destinations/assets/ui/export-datasets/review.png)

## 验证是否成功导出数据集 {#verify}

导出数据集时，Experience Platform创建 `.json` 或 `.parquet` 文件存储位置。 根据您提供的导出计划，期望将新文件存储到您的存储位置。

Experience Platform会在您指定的存储位置创建一个文件夹结构，存放导出的数据集文件。 每次导出时都会创建一个新文件夹，其模式如下：

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

默认文件名是随机生成的，并确保导出的文件名是唯一的。

### 示例数据集文件 {#sample-files}

这些文件在您的存储位置中存在就是成功导出的确认。 要了解导出文件的结构形式，您可以下载一个示例 [.parquet文件](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) 或 [.json文件](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

## 从目标删除数据集 {#remove-dataset}

要从现有数据流中删除数据集，请执行以下步骤：

1. 登录到 [EXPERIENCE PLATFORMUI](https://platform.adobe.com/) 并选择 **[!UICONTROL 目标]** 左侧导航栏中的。 选择 **[!UICONTROL 浏览]** 查看现有目标数据流。

   ![目标浏览视图，其中显示了一个目标连接，其余连接被模糊处理。](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >选择过滤器图标 ![筛选图标](../assets/ui/edit-activation/filter.png) 以启动“排序”面板。 排序面板提供所有目标的列表。 您可以从列表中选择多个目标，以查看与所选目标关联的数据流的筛选选择。

1. 从 **[!UICONTROL 激活数据]** 列中，选择数据集控件以查看映射到此导出数据流的所有数据集。

   ![可用数据集导航选项在激活数据列中突出显示。](../assets/ui/export-datasets/go-to-datasets-data.png)

1. 此 **[!UICONTROL 激活数据]** 此时将显示目标页面。 选择 **[!UICONTROL 删除数据集]** ，以触发删除数据集确认对话框。

   ![删除数据集对话框在右边栏中显示“删除数据集”控件。](../assets/ui/export-datasets/remove-dataset-control.png)

1. 在确认对话框中，选择 **[!UICONTROL 移除]** 以立即从到目标的导出中删除数据集。

   ![显示确认从数据流中删除数据集选项的对话框。](../assets/ui/export-datasets/remove-dataset-confirm.png)

## 已知限制 {#known-limitations}

请牢记数据集导出测试版的以下限制：

* 当前只有一个权限(**[!UICONTROL 管理和激活数据集目标]**)中包含管理和激活数据集目标权限。 这些控件将在将来拆分为更细粒度的权限。 查看 [所需权限](#permissions) 部分，以获取导出数据集所需的权限的完整列表。
* 目前，您只能导出增量文件，并且无法为数据集导出选择结束日期。
* 导出的文件名当前不可自定义。
* UI当前不会阻止您删除正在导出到目标的数据集。 请勿删除任何正在导出到目标的数据集。 [删除数据集](#remove-dataset) 删除之前从目标数据流中删除的数据。
* 数据集导出的监控量度当前与配置文件导出的数字混杂在一起，因此它们不能反映真正的导出数字。
