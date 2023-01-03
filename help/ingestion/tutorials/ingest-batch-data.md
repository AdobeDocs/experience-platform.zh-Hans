---
keywords: Experience Platform；主页；热门主题；摄取；摄取批量数据；教程；批量摄取；教程；用户界面指南；
solution: Experience Platform
title: 将数据摄取到Experience Platform
topic-legacy: tutorial
type: Tutorial
description: 利用Adobe Experience Platform，可以轻松将数据导入为批处理文件，格式为符合已知Experience Data Model(XDM)架构的Parquet文件或数据。
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 0%

---

# 将数据摄取到Adobe Experience Platform

Adobe Experience Platform允许您轻松将数据导入 [!DNL Platform] 作为批处理文件。 要摄取的数据示例可包括来自CRM系统中平面文件（如Parquet文件）的配置文件数据或符合已知数据的数据 [!DNL Experience Data Model] (XDM)架构。

## 快速入门

要完成本教程，您必须具有 [!DNL Experience Platform]. 如果您在 [!DNL Experience Platform]，请在继续操作之前与系统管理员联系。

如果您希望使用数据摄取API摄取数据，请首先阅读 [批量摄取开发人员指南](../batch-ingestion/api-overview.md).

## 数据集工作区

中的数据集工作区 [!DNL Experience Platform] 允许您查看和管理IMS组织创建的所有数据集，并创建新数据集。

通过单击 **[!UICONTROL 数据集]** 的下游。 数据集工作区包含数据集列表，其中包括显示名称、创建时间（日期和时间）、源、架构和上次批处理状态的列，以及上次更新数据集的日期和时间。

>[!NOTE]
>
>单击搜索栏旁边的过滤器图标，以使用过滤功能仅查看为 [!DNL Profile].

![查看所有数据集](../images/tutorials/ingest-batch-data/datasets-overview.png)

## 创建数据集

要创建数据集，请单击 **[!UICONTROL 创建数据集]** 数据集工作区的右上角。

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

在 **[!UICONTROL 创建数据集]** 屏幕，选择是否要[!UICONTROL 从架构创建数据集]&quot;或&quot;[!UICONTROL 从CSV文件创建数据集]&quot;

在本教程中，将使用一个架构来创建数据集。 单击 **[!UICONTROL 从架构创建数据集]** 继续。

![选择数据源](../images/tutorials/ingest-batch-data/create-dataset.png)

## 选择数据集架构

在 **[!UICONTROL 选择架构]** 屏幕上，单击您要使用的架构旁边的单选按钮以选择架构。 在本教程中，数据集将使用忠诚度会员架构生成。 使用搜索栏筛选架构是查找要查找的确切架构的一种有用方法。

选择您要使用的架构旁边的单选按钮后，单击 **[!UICONTROL 下一个]**.

![选择架构](../images/tutorials/ingest-batch-data/select-schema.png)

## 配置数据集

在 **[!UICONTROL 配置数据集]** 屏幕上，您将需要为数据集指定一个名称，并且还可能会提供数据集的描述。

**数据集名称的注释：**

- 数据集名称应该简短且具有描述性，以便以后可以在库中轻松找到该数据集。
- 数据集名称必须是唯一的，这意味着数据集名称还应具有足够的特定性，以便将来不会重复使用。
- 最佳做法是使用描述字段提供有关数据集的其他信息，因为这可能有助于其他用户将来区分不同的数据集。

在数据集具有名称和描述后，单击 **[!UICONTROL 完成]**.

![配置数据集](../images/tutorials/ingest-batch-data/configure-dataset.png)

## 数据集活动

现在已创建空数据集，并且您已返回到 **[!UICONTROL 数据集活动]** 选项卡。 您应会在工作区的左上角看到数据集的名称，并收到“尚未添加任何批次”通知。 由于您尚未向此数据集添加任何批次，因此应该会出现这种情况。

在数据集工作区的右侧，您将看到 **[!UICONTROL 信息]** 选项卡，其中包含与新数据集相关的信息，如数据集ID、名称、描述、表名、架构、流和源。 “信息”选项卡还包含有关数据集何时创建及其上次修改日期的信息。

“信息”(Info)选项卡中的  **[!UICONTROL 用户档案]** 切换用于启用数据集以供 [!DNL Real-Time Customer Profile]. 使用此切换开关，以及 [!DNL Real-Time Customer Profile]，将在以下章节中详细说明。

![数据集活动](../images/tutorials/ingest-batch-data/sample-dataset.png)

## 为启用数据集 [!DNL Real-Time Customer Profile]

数据集用于将数据摄取到 [!DNL Experience Platform]，并且该数据最终用于识别个人并拼合来自多个来源的信息。 拼合在一起的信息称为 [!DNL Real-Time Customer Profile]. 为 [!DNL Platform] 了解哪些信息应包含在 [!DNL Real-Time Profile]，则可以使用 **[!UICONTROL 用户档案]** 切换。

默认情况下，此切换开关处于关闭状态。 如果选择打开 [!DNL Profile]，则摄取到数据集的所有数据都将用于帮助识别个人并拼合其数据 [!DNL Real-Time Profile].

详细了解 [!DNL Real-Time Customer Profile] 使用身份，请查阅 [Identity Service](../../identity-service/home.md) 文档。

为 [!DNL Real-Time Customer Profile]，请单击 **[!UICONTROL 用户档案]** 在 **[!UICONTROL 信息]** 选项卡。

![配置文件切换](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

将显示一个对话框，要求您确认是否要为 [!DNL Real-Time Customer Profile].

![“启用配置文件”对话框](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

单击 **[!UICONTROL 启用]** 切换开关将变为蓝色，表示它已打开。

![为配置文件启用](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## 将数据添加到数据集

可以通过多种不同方式将数据添加到数据集。 您可以选择使用 [!DNL Data Ingestion] API或ETL合作伙伴，例如 [!DNL Unifi] 或 [!DNL Informatica]. 在本教程中，将使用 **[!UICONTROL 添加数据]** 选项卡。

要开始向数据集添加数据，请单击 **[!UICONTROL 添加数据]** 选项卡。 您现在可以拖放文件或浏览计算机以查找要添加的文件。

>[!NOTE]
>
>Platform支持两种文件类型（Parquet或JSON）进行数据摄取。 一次最多可以添加五个文件，每个文件的最大文件大小为1 GB。

![“添加数据”选项卡](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## 上传文件

拖放（或浏览并选择）要上传的Parquet或JSON文件后， [!DNL Platform] 将立即开始处理文件，并且 **[!UICONTROL 上传]** 对话框将显示在 **[!UICONTROL 添加数据]** 选项卡，其中显示了文件上传的进度。

![上传对话框](../images/tutorials/ingest-batch-data/uploading-file.png)

## 数据集量度

文件上传完成后， **[!UICONTROL 数据集活动]** 选项卡不再显示“尚未添加批次”。 相反， **[!UICONTROL 数据集活动]** 选项卡当前显示数据集量度。 由于尚未加载批处理，因此在此阶段所有量度都将显示“0”。

在选项卡的底部，有一个列表显示 **[!UICONTROL 批处理ID]** 通过 [&quot;向数据集添加数据&quot;](#add-data-to-dataset) 进程。 此外，还包含与批相关的信息，包括摄取日期、摄取的记录数和当前批状态。

![数据集量度](../images/tutorials/ingest-batch-data/batch-id.png)

## 批次详细信息

单击 **[!UICONTROL 批处理ID]** 查看 **[!UICONTROL 批量概述]**，显示有关该批的其他详细信息。 批处理完成加载后，有关该批处理的信息将更新，以显示摄取的记录数和文件大小。 状态还将更改为“成功”或“失败”。 如果批处理失败，则 **[!UICONTROL 错误代码]** 部分将包含有关摄取过程中任何错误的详细信息。

有关批量摄取的更多信息和常见问题解答，请参阅 [批量摄取疑难解答指南](../batch-ingestion/troubleshooting.md).

返回到 **[!UICONTROL 数据集活动]** 屏幕上，单击数据集的名称(**[!UICONTROL 忠诚度详细信息]**)。

![批量概述](../images/tutorials/ingest-batch-data/batch-details.png)

## 预览数据集

数据集准备就绪后，可以选择 **[!UICONTROL 预览数据集]** 在 **[!UICONTROL 数据集活动]** 选项卡。

单击 **[!UICONTROL 预览数据集]** 打开一个对话框，其中显示数据集内的示例数据。 如果数据集是使用架构创建的，则有关数据集架构的详细信息将显示在预览的左侧。 您可以使用箭头展开架构以查看架构结构。 预览数据中的每个列标题都表示数据集中的一个字段。

![数据集详细信息](../images/tutorials/ingest-batch-data/dataset-preview.png)

## 后续步骤和其他资源

现在，您已创建数据集并成功将数据摄取到 [!DNL Experience Platform]，则可以重复这些步骤以创建新数据集或将更多数据摄取到现有数据集。

要了解有关批量摄取的更多信息，请阅读 [批量摄取概述](../batch-ingestion/overview.md) 并通过观看下面的视频来补充您的学习。

>[!WARNING]
>
>的 [!DNL Platform] 以下视频中显示的UI已过期。 有关最新的UI屏幕截图和功能，请参阅上述文档。

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
