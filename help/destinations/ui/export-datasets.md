---
title: （测试版）将数据集导出到云存储目标
type: Tutorial
description: 了解如何将数据集从Adobe Experience Platform导出到首选的云存储位置。
source-git-commit: 97a39e12d916e4fbd048c0fb9ddfa9bdfa10d438
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 1%

---

# （测试版）将数据集导出到云存储目标

>[!IMPORTANT]
>
>* 导出数据集的功能目前处于测试阶段，并非所有用户都能使用。 文档和功能可能会发生变化。
>* 此测试版功能支持导出第一代数据(在Real-time Customer Data Platform中定义) [产品说明](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
>* 购买了Real-Time CDP Prime和Ultimate产品包的客户可以使用此功能。 有关更多信息，请联系您的Adobe代表。


本文介绍了导出所需的工作流 [数据集](/help/catalog/datasets/overview.md) 从Adobe Experience Platform到首选云存储位置，例如 [!DNL Amazon S3]、SFTP位置，或 [!DNL Google Cloud Storage].

## 何时激活区段或导出数据集 {#when-to-activate-segments-or-activate-datasets}

Experience Platform目录中某些基于文件的目标同时支持区段激活和数据集导出。

* 当您希望将数据构建为按受众兴趣或资格分组的用户档案时，请考虑激活区段。
* 或者，当您想要导出未按受众兴趣或资格进行分组或构建的原始数据集时，请考虑数据集导出。 您可以将此数据用于报告、数据科学工作流、满足法规遵从性要求以及许多其他用例。

本文档包含导出数据集所需的所有信息。 如果要将区段激活到云存储或电子邮件营销目标，请阅读 [激活受众数据以批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md).

## 先决条件 {#prerequisites}

要将数据集导出到云存储目标，您必须成功 [连接到目标](./connect-destination.md). 如果您尚未执行此操作，请转到 [目标目录](../catalog/overview.md)，浏览支持的目标，并配置要使用的目标。

### 所需权限 {#permissions}

要导出数据集，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 查看目标]**, **[!UICONTROL 激活目标]**&#x200B;和 **[!UICONTROL 管理和激活数据集目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要确保您拥有导出数据集的必要权限，并且目标支持导出数据集，请浏览目标目录。 如果目标具有 **[!UICONTROL 激活]** 或 **[!UICONTROL 导出数据集]** 控制，则您拥有相应的权限。

## 选择您的目标 {#select-destination}

按照相关说明选择可以导出数据集的目标：

1. 转到 **[!UICONTROL 连接>目标]**，然后选择 **[!UICONTROL 目录]** 选项卡。

   ![目标目录选项卡，其中突出显示了目录控件。](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. 选择 **[!UICONTROL 激活]** 或 **[!UICONTROL 导出数据集]** 在与要将数据集导出到的目标对应的卡上。

   ![“目标目录”选项卡，其中突出显示了“激活”控件。](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. 选择 **[!UICONTROL 数据类型数据集]** ，然后选择要将数据集导出到的目标连接，然后选择 **[!UICONTROL 下一个]**.

>[!TIP]
> 
>如果要设置新目标以导出数据集，请选择 **[!UICONTROL 配置新目标]** 来触发 [连接到目标](/help/destinations/ui/connect-destination.md) 工作流。

![突出显示数据集控件的目标激活工作流。](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. 的 **[!UICONTROL 选择数据集]** 视图。 转到下一节以 [选择数据集](#select-datasets) 导出时。

## 选择数据集 {#select-datasets}

使用数据集名称左侧的复选框选择要导出到目标的数据集，然后选择 **[!UICONTROL 下一个]**.

![数据集导出工作流，其中显示了选择数据集步骤，您可以在此步骤中选择要导出的数据集。](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## 计划数据集导出 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="数据集的文件导出选项"
>abstract="选择 **导出增量文件** 以仅导出自上次导出后添加到数据集的数据。 <br> 第一个增量文件导出包含数据集中的所有数据，充当回填。 将来的增量文件仅包含自首次导出以来添加到数据集的数据。"

在 **[!UICONTROL 计划]** 步骤中，您可以为数据集导出设置开始日期和导出频率。

的 **[!UICONTROL 导出增量文件]** 选项。 这会触发导出，其中第一个文件是数据集的完整快照，后续文件是自上次导出以来对数据集的增量添加。

>[!IMPORTANT]
>
>第一个导出的增量文件包含数据集中的所有现有数据，可用作回填。

![显示计划步骤的数据集导出工作流。](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. 使用 **[!UICONTROL 频率]** 选择器以选择导出频率：

   * **[!UICONTROL 每日]**:在您指定的时间，安排增量文件每天导出一次。
   * **[!UICONTROL 每小时]**:计划每3、6、8或12小时执行一次增量文件导出。

2. 使用 **[!UICONTROL 时间]** 选择器，以选择一天中的时间 [!DNL UTC] 格式，应在何时进行导出。

3. 使用 **[!UICONTROL 日期]** 选择器以选择应执行导出的间隔。 请注意，在该功能的测试版中，无法设置导出的结束日期。 有关更多信息，请查看 [已知限制](#known-limitations) 中。

4. 选择 **[!UICONTROL 下一个]** 保存计划并继续 **[!UICONTROL 审阅]** 中。

>[!NOTE]
> 
>对于数据集导出，文件名具有默认格式的预设，无法修改。 请参阅部分 [验证数据集导出是否成功](#verify) ，以了解导出文件的详细信息和示例。

## 审阅 {#review}

在 **[!UICONTROL 审阅]** 页面，则可以查看所选内容的摘要。 选择 **[!UICONTROL 取消]** 来分解流量， **[!UICONTROL 返回]** 修改设置，或 **[!UICONTROL 完成]** 以确认您的选择并开始将数据集导出到目标。

![显示审核步骤的数据集导出工作流。](/help/destinations/assets/ui/export-datasets/review.png)

## 验证数据集导出是否成功 {#verify}

导出数据集时，Experience Platform会创建 `.json` 或 `.parquet` 文件。 您希望根据提供的导出计划将新文件存入您的存储位置。

Experience Platform会在您指定的存储位置中创建文件夹结构，其中会保存导出的数据集文件。 每次导出时都会按照以下模式创建新文件夹：

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

默认文件名是随机生成的，并确保导出的文件名是唯一的。

### 示例数据集文件 {#sample-files}

这些文件在您的存储位置中的存在是成功导出的确认。 要了解导出文件的结构方式，您可以下载示例 [.parquet文件](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) 或 [.json文件](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

## 从目标中删除数据集 {#remove-dataset}

要从现有数据流中删除数据集，请执行以下步骤：

1. 登录到 [Experience PlatformUI](https://platform.adobe.com/) 选择 **[!UICONTROL 目标]** 中。 选择 **[!UICONTROL 浏览]** 来查看现有目标数据流。

   ![显示了目标连接的目标浏览视图，其余视图模糊。](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >选择过滤器图标 ![过滤器图标](../assets/ui/edit-activation/filter.png) 来启动排序面板。 排序面板提供了所有目标的列表。 您可以从列表中选择多个目标，以查看与选定目标关联的已过滤数据流选项。

1. 从 **[!UICONTROL 激活数据]** 列中，选择数据集控件以查看映射到此导出数据流的所有数据集。

   ![激活数据列中突出显示的可用数据集导航选项。](../assets/ui/export-datasets/go-to-datasets-data.png)

1. 的 **[!UICONTROL 激活数据]** 页面。 选择 **[!UICONTROL 删除数据集]** 在右边栏中触发删除数据集确认对话框。

   ![删除数据集对话框，其中在右边栏中显示删除数据集控件。](../assets/ui/export-datasets/remove-dataset-control.png)

1. 在确认对话框中，选择 **[!UICONTROL 删除]** 可立即将数据集从导出到目标中删除。

   ![显示从数据流确认数据集删除选项的对话框。](../assets/ui/export-datasets/remove-dataset-confirm.png)

## 已知限制 {#known-limitations}

请记住，数据集导出测试版存在以下限制：

* 当前只有一个权限(**[!UICONTROL 管理和激活数据集目标]**)，包括管理和激活数据集目标的权限。 这些控件将来会拆分为更多粒度权限。 查看 [所需权限](#permissions) 部分，以获取导出数据集所需权限的完整列表。
* 目前，您只能导出增量文件，并且无法为数据集导出选择结束日期。
* 当前无法自定义导出的文件名。
* UI当前不会阻止您删除要导出到目标的数据集。 请勿删除要导出到目标的任何数据集。 [删除数据集](#remove-dataset) 从目标数据流删除。
* 数据集导出的监控量度当前与配置文件导出的数字混合在一起，以便它们不反映真实的导出数字。
