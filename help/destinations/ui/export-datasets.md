---
title: 将数据集导出到云存储目标
type: Tutorial
description: 了解如何将数据集从Adobe Experience Platform导出到您首选的云存储位置。
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: 9d3b6409013edc38ef41dd2a184ccbdcf7ab9edd
workflow-type: tm+mt
source-wordcount: '1891'
ht-degree: 4%

---

# 将数据集导出到云存储目标

>[!AVAILABILITY]
>
>* 已购买Real-Time CDP Prime或Ultimate包、Adobe Journey Optimizer或Customer Journey Analytics的客户可使用此功能。 有关更多信息，请与您的Adobe代表联系。

本文介绍使用Experience PlatformUI将[数据集](/help/catalog/datasets/overview.md)从Adobe Experience Platform导出到首选云存储位置（如[!DNL Amazon S3]、SFTP位置或[!DNL Google Cloud Storage]）所需的工作流。

您还可以使用Experience PlatformAPI导出数据集。 有关详细信息，请阅读[导出数据集API教程](/help/destinations/api/export-datasets.md)。

## 可用于导出的数据集 {#datasets-to-export}

根据Experience Platform应用程序(Real-Time CDP、Adobe Journey Optimizer)、层（Prime或Ultimate）以及您购买的任何加载项(例如：Data Distiller)，您可以导出的数据集会有所不同。

根据您购买的应用程序、产品层和任何加载项，从下表了解可以导出哪些数据集类型：

<table>
<thead>
  <tr>
    <th>应用程序/加载项</th>
    <th>层</th>
    <th>可用于导出的数据集</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Real-Time CDP</td>
    <td>Prime</td>
    <td>通过源、Web SDK、Mobile SDK、Analytics Data Connector和Audience Manager摄取或收集数据后，在Experience PlatformUI中创建的配置文件和体验事件数据集。</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td><ul><li>通过源、Web SDK、Mobile SDK、Analytics Data Connector和Audience Manager摄取或收集数据后，在Experience PlatformUI中创建的配置文件和体验事件数据集。</li><li> <a href="https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html#profile-attribute-datasets">系统生成的配置文件快照数据集</a>。</li></td>
  </tr>
  <tr>
    <td rowspan="2">Adobe Journey Optimizer</td>
    <td>Prime</td>
    <td>请参阅<a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a>文档。</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td>请参阅<a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a>文档。</td>
  </tr>
  <tr>
    <td>Customer Journey Analytics</td>
    <td>全部</td>
    <td> 通过源、Web SDK、Mobile SDK、Analytics Data Connector和Audience Manager摄取或收集数据后，在Experience PlatformUI中创建的配置文件和体验事件数据集。 <br> <p> <b>可用性注意事项：</b>将数据集导出到云的功能处于版本的有限测试阶段，可能在您的环境中尚不可用。 当功能正式可用时，将删除此注释。 有关Customer Journey Analytics发布过程的信息，请参阅<a href="https://experienceleague.adobe.com/docs/analytics-platform/using/releases/releases.html">Customer Journey Analytics功能发布</a>。 </p> </td>
  </tr>
  <tr>
    <td>数据 Distiller</td>
    <td>Data Distiller（加载项）</td>
    <td>通过查询服务创建的派生数据集。</td>
  </tr>
</tbody>
</table>

## 视频教程 {#video-tutorial}

观看以下视频，了解此页面上描述的工作流的端到端说明、使用导出数据集功能的好处以及一些建议的用例。

>[!VIDEO](https://video.tv.adobe.com/v/3424392/)

## 支持的目标 {#supported-destinations}

目前，您可以将数据集导出到屏幕快照中突出显示的云存储目标，如下所列。

![显示哪些目标支持数据集导出的目标目录页面。](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## 何时激活受众或导出数据集 {#when-to-activate-audiences-or-activate-datasets}

Experience Platform目录中的一些基于文件的目标同时支持Audience Activation和数据集导出。

* 当您希望将数据结构化为按受众兴趣或资格分组的用户档案时，请考虑激活受众。
* 或者，在要导出未按受众兴趣或资格进行分组或构建的原始数据集时，请考虑数据集导出。 您可以将此数据用于报表、数据科学工作流和许多其他用例。 例如，作为管理员、数据工程师或分析师，您可以从Experience Platform中导出数据以与数据仓库同步、在BI分析工具、外部云ML工具中使用，或存储在您的系统中以满足长期存储需求。

本文档包含导出数据集所需的所有信息。 如果要将&#x200B;*受众*&#x200B;激活到云存储或电子邮件营销目标，请阅读[将受众数据激活到批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)。

## 先决条件 {#prerequisites}

要将数据集导出到云存储目标，您必须已成功[连接到目标](./connect-destination.md)。 如果您尚未这样做，请转到[目标目录](../catalog/overview.md)，浏览支持的目标，然后配置要使用的目标。

### 所需的权限 {#permissions}

要导出数据集，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 查看数据集]**&#x200B;和&#x200B;**[!UICONTROL 管理和激活数据集目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要确保您具有导出数据集的必要权限并且目标支持导出数据集，请浏览目标目录。 如果目标具有&#x200B;**[!UICONTROL 激活]**&#x200B;或&#x200B;**[!UICONTROL 导出数据集]**&#x200B;控件，则您具有相应的权限。

## 选择您的目标 {#select-destination}

按照相关说明选择一个可导出数据集的目标：

1. 转到&#x200B;**[!UICONTROL 连接>目标]**，然后选择&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡。

   ![目录控件突出显示的目标目录选项卡。](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. 在与要将数据集导出到的目标对应的卡片上，选择&#x200B;**[!UICONTROL 激活]**&#x200B;或&#x200B;**[!UICONTROL 导出数据集]**。

   ![突出显示了“激活”控件的“目标目录”选项卡。](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. 选择&#x200B;**[!UICONTROL 数据类型数据集]**&#x200B;并选择要将数据集导出到的目标连接，然后选择&#x200B;**[!UICONTROL 下一步]**。

>[!TIP]
> 
>如果要设置新目标以导出数据集，请选择&#x200B;**[!UICONTROL 配置新目标]**&#x200B;以触发[连接到目标](/help/destinations/ui/connect-destination.md)工作流。

![数据集控件突出显示的目标激活工作流。](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. 出现&#x200B;**[!UICONTROL 选择数据集]**&#x200B;视图。 继续到[选择要导出的数据集](#select-datasets)的下一部分。

## 选择您的数据集 {#select-datasets}

使用数据集名称左侧的复选框选择要导出到目标的数据集，然后选择&#x200B;**[!UICONTROL 下一步]**。

![数据集导出工作流显示“选择数据集”步骤，您可以在其中选择要导出哪些数据集。](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## 计划数据集导出 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="数据集的文件导出选项"
>abstract="选择&#x200B;**导出增量文件**&#x200B;以仅导出自上次导出后添加到数据集的数据。<br>第一个增量文件导出包括数据集中的所有数据，充当回填。后续增量文件仅包含自第一次导出后添加到数据集的数据。"

在&#x200B;**[!UICONTROL 计划]**&#x200B;步骤中，您可以为数据集导出设置开始日期和导出节奏。

已自动选择&#x200B;**[!UICONTROL 导出增量文件]**&#x200B;选项。 这会触发导出一个或多个表示数据集的完整快照的文件。 后续文件是自上次导出以来向数据集添加的增量文件。

>[!IMPORTANT]
>
>第一个增量文件导出包含数据集中的所有现有数据，充当回填。 导出可以包含一个或多个文件。

![数据集导出工作流显示计划步骤。](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. 使用&#x200B;**[!UICONTROL 频率]**&#x200B;选择器选择导出频率：

   * **[!UICONTROL 每日]**：计划每天在指定的时间导出一次增量文件。
   * **[!UICONTROL 小时]**：计划每3、6、8或12小时导出一次增量文件。

2. 使用&#x200B;**[!UICONTROL Time]**&#x200B;选择器以[!DNL UTC]格式选择一天中何时进行导出。

3. 使用&#x200B;**[!UICONTROL 日期]**&#x200B;选择器选择应执行导出的时间间隔。 请注意，您当前无法设置导出的结束日期。 有关详细信息，请查看[已知限制](#known-limitations)部分。

4. 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;保存计划并继续&#x200B;**[!UICONTROL 审阅]**&#x200B;步骤。

>[!NOTE]
> 
>对于数据集导出，文件名具有无法修改的预设默认格式。 有关导出文件的更多信息和示例，请参阅[验证成功的数据集导出](#verify)部分。

## 审查 {#review}

在&#x200B;**[!UICONTROL 审核]**&#x200B;页面上，您可以看到所选内容的摘要。 选择&#x200B;**[!UICONTROL 取消]**&#x200B;以中断流，**[!UICONTROL 返回]**&#x200B;以修改您的设置，或者选择&#x200B;**[!UICONTROL 完成]**&#x200B;以确认您的选择并开始将数据集导出到目标。

![数据集导出工作流显示审核步骤。](/help/destinations/assets/ui/export-datasets/review.png)

## 验证是否成功导出数据集 {#verify}

导出数据集时，Experience Platform会在您提供的存储位置中创建一个或多个文件`.json`或`.parquet`。 希望根据您提供的导出计划将新文件存储在您的存储位置。

Experience Platform会在您指定的存储位置创建一个文件夹结构，存放导出的数据集文件。 每次导出时都会创建一个新文件夹，其模式如下所示：

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

默认文件名是随机生成的，并确保导出的文件名是唯一的。

### 示例数据集文件 {#sample-files}

这些文件在存储位置中的存在是成功导出的确认。 要了解导出文件的结构方式，您可以下载示例[.parquet文件](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet)或[.json文件](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json)。

#### 压缩的数据集文件 {#compressed-dataset-files}

在[连接到目标工作流](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options)中，您可以选择要压缩的导出数据集文件，如下所示：

![连接到目标以导出数据集时文件类型和压缩选择。](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

请注意两种文件类型在压缩后的文件格式差异：

* 导出压缩的JSON文件时，导出的文件格式为`json.gz`
* 导出压缩的parquet文件时，导出的文件格式为`gz.parquet`

## 从目标中删除数据集 {#remove-dataset}

要从现有数据流中删除数据集，请执行以下步骤：

1. 登录到[Experience PlatformUI](https://experience.adobe.com/platform/)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 目标]**。 从顶部标题中选择&#x200B;**[!UICONTROL 浏览]**&#x200B;以查看现有目标数据流。

   ![目标浏览视图，其中显示目标连接，其余连接模糊。](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >选择左上角的过滤器图标![过滤器图标](../assets/ui/edit-activation/filter.png)以启动排序面板。 排序面板提供所有目标的列表。 您可以从列表中选择多个目标，以查看与所选目标关联的数据流的过滤选择。

1. 从&#x200B;**[!UICONTROL 激活数据]**&#x200B;列中，选择数据集控件以查看映射到此导出数据流的所有数据集。

   ![在“激活数据”列中突出显示的可用数据集导航选项。](../assets/ui/export-datasets/go-to-datasets-data.png)

1. [!BADGE Beta]将显示目标的&#x200B;**[!UICONTROL 激活数据]**&#x200B;页面。 使用数据集列表左侧的复选框选择要删除的数据集，然后在右边栏中选择&#x200B;**[!UICONTROL 删除数据集]**&#x200B;以触发删除数据集确认对话框。

   >[!NOTE]
   >
   >此功能为测试版，仅向部分客户提供。 要请求访问此功能，请联系您的Adobe代表。

   ![在右边栏中显示删除数据集控件的“删除数据集”对话框。](../assets/ui/export-datasets/bulk-remove-datasets.png)

1. 在确认对话框中，选择&#x200B;**[!UICONTROL 移除]**&#x200B;以立即从导出到目标的数据集中移除数据集。

   ![显示从数据流中删除确认数据集选项的对话框。](../assets/ui/export-datasets/remove-dataset-confirm.png)

## 数据集导出授权 {#licensing-entitlement}

请参阅产品描述文档，了解您每年有权为每个Experience Platform应用程序导出多少数据。 例如，您可以在[此处](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)查看Real-Time CDP产品说明。

请注意，不同应用程序的数据导出权限不是累加的。 例如，这意味着如果您购买Real-Time CDP Ultimate和Adobe Journey Optimizer Ultimate，则根据产品描述，用户档案导出权利将是两个权利中较大的一个权利。 您的批量权利的计算方法是：获取许可配置文件的总数，然后乘以Real-Time CDP Prime的500 KB或Real-Time CDP Ultimate的700 KB，从而确定您有权获得的数据量。

另一方面，如果您购买了Data Distiller等加载项，则您有权获得的数据导出限制表示产品层和加载项的总和。

您可以在许可控制面板中查看和跟踪配置文件导出是否符合合同限制。

## 已知限制 {#known-limitations}

对于数据集导出的常规可用性版本，请牢记以下限制：

* 目前，您只能导出增量文件，并且无法为数据集导出选择结束日期。
* 当前无法自定义导出的文件名。
* 通过API创建的数据集当前不可导出。
* 目前，UI不会阻止您删除正在导出到目标的数据集。 请勿删除任何正在导出到目标的数据集。 [删除目标数据流中的数据集](#remove-dataset)之前。
* 数据集导出的监控量度当前与用户档案导出的数字混杂在一起，因此它们不反映真正的导出数字。
* 时间戳超过365天的数据将从数据集导出中排除。 有关详细信息，请查看计划数据集导出的[护栏](/help/destinations/guardrails.md#guardrails-for-scheduled-dataset-exports)
