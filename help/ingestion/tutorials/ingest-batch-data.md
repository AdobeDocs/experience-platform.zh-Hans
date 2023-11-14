---
keywords: Experience Platform；主页；热门主题；摄取；摄取批量数据；教程；批量摄取；教程；ui指南；
solution: Experience Platform
title: 将数据摄取到Experience Platform
type: Tutorial
description: 通过Adobe Experience Platform，您可以轻松地将数据作为Parquet文件形式的批处理文件或符合已知Experience Data Model (XDM)架构的数据导入。
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
source-git-commit: 8351f6907a0dc4a4bba01c7f6e9dec7c376c8575
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 1%

---

# 将数据摄取到 Adobe Experience Platform

通过Adobe Experience Platform，您可以轻松地将数据导入 [!DNL Platform] 作为批处理文件。 要摄取的数据的示例可能包括CRM系统中平面文件（如Parquet文件）的配置文件数据或与已知符合的数据 [!DNL Experience Data Model] 架构注册表中的(XDM)架构。

## 快速入门

要完成本教程，您必须有权访问 [!DNL Experience Platform]. 如果您无权访问中的组织 [!DNL Experience Platform]，请在继续之前联系您的系统管理员。

如果您希望使用数据摄取API来摄取数据，请先阅读 [批量摄取开发人员指南](../batch-ingestion/api-overview.md).

## 数据集工作区

中的数据集工作区 [!DNL Experience Platform] 允许您查看和管理组织创建的所有数据集，并创建新数据集。

通过单击查看数据集工作区 **[!UICONTROL 数据集]** 在左侧导航栏中。 数据集工作区包含数据集列表，其中包括显示名称、创建（日期和时间）、源、架构和上次批次状态以及上次更新数据集的日期和时间的列。

>[!NOTE]
>
>单击搜索栏旁边的过滤器图标可使用过滤功能仅查看那些为以下项启用的数据集 [!DNL Profile].

![查看所有数据集](../images/tutorials/ingest-batch-data/datasets-overview.png)

## 创建数据集

要创建数据集，请单击 **[!UICONTROL 创建数据集]** 位于数据集工作区的右上角。

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

在 **[!UICONTROL 创建数据集]** 屏幕上，选择是否要&quot;[!UICONTROL 从架构创建数据集]”或“[!UICONTROL 从CSV文件创建数据集]“。

在本教程中，将使用架构创建数据集。 单击 **[!UICONTROL 从架构创建数据集]** 以继续。

![选择数据源](../images/tutorials/ingest-batch-data/create-dataset.png)

## 选择数据集架构

在 **[!UICONTROL 选择架构]** 屏幕上，通过单击要使用的方案旁边的单选按钮来选择方案。 在本教程中，将使用忠诚度成员架构创建数据集。 使用搜索栏筛选架构是一种查找要查找的确切架构的有用方法。

选中要使用的模式旁边的单选按钮后，单击 **[!UICONTROL 下一个]**.

![选择架构](../images/tutorials/ingest-batch-data/select-schema.png)

## 配置数据集

在 **[!UICONTROL 配置数据集]** 屏幕时，您需要为数据集提供一个名称，并且还可以提供数据集的描述。

**有关数据集名称的注释：**

- 数据集名称应简短且具有描述性，以便之后能够在库中轻松找到数据集。
- 数据集名称必须是唯一的，这意味着它还应该足够具体，以便将来不会重复使用。
- 最佳实践是使用描述字段提供有关数据集的附加信息，因为它可能有助于其他用户将来区分数据集。

在数据集获得名称和描述后，单击 **[!UICONTROL 完成]**.

![配置数据集](../images/tutorials/ingest-batch-data/configure-dataset.png)

## 数据集活动

现在已创建一个空的数据集，并且您已经返回到 **[!UICONTROL 数据集活动]** 选项卡。 您应该会在工作区的左上角看到数据集的名称，同时还会看到“未添加任何批次”的通知。 这是正常情况，因为您尚未将任何批次添加到此数据集。

在数据集工作区的右侧，您将看到 **[!UICONTROL 信息]** 选项卡包含与新数据集相关的信息，例如数据集ID、名称、描述、表名称、架构、流和源。 信息选项卡还包括有关数据集的创建时间及其上次修改日期的信息。

另外，在“信息”选项卡中，  **[!UICONTROL 个人资料]** 用于启用数据集以供使用的切换开关 [!DNL Real-Time Customer Profile]. 使用此切换和 [!DNL Real-Time Customer Profile]，将在以下部分中详细解释。

![数据集活动](../images/tutorials/ingest-batch-data/sample-dataset.png)

## 为以下项启用数据集 [!DNL Real-Time Customer Profile]

数据集用于将数据摄取到 [!DNL Experience Platform]，该数据最终用于识别个人并将来自多个来源的信息拼合在一起。 将信息拼合在一起称为 [!DNL Real-Time Customer Profile]. 为了 [!DNL Platform] 了解哪些信息应包含在 [!DNL Real-Time Profile]，可以使用将数据集标记为包含 **[!UICONTROL 个人资料]** 切换。

默认情况下，此切换处于关闭状态。 如果您选择打开 [!DNL Profile]，则摄取到数据集中的所有数据将用于帮助识别个人并将他们的 [!DNL Real-Time Profile].

要了解有关 [!DNL Real-Time Customer Profile] 并使用标识，请查看 [Identity Service](../../identity-service/home.md) 文档。

启用数据集 [!DNL Real-Time Customer Profile]，单击 **[!UICONTROL 个人资料]** 切换到 **[!UICONTROL 信息]** 选项卡。

![配置文件切换](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

此时将显示一个对话框，要求您确认要为以下项启用数据集 [!DNL Real-Time Customer Profile].

![启用配置文件对话框](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

单击 **[!UICONTROL 启用]** 切换将变为蓝色，表示已打开。

![已为配置文件启用](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## 将数据添加到数据集

可以通过多种不同的方式将数据添加到数据集中。 您可以选择使用 [!DNL Data Ingestion] API或ETL合作伙伴，例如 [!DNL Unifi] 或 [!DNL Informatica]. 在本教程中，您将使用将数据添加到数据集 **[!UICONTROL 添加数据]** 选项卡。

要开始将数据添加到数据集，请单击 **[!UICONTROL 添加数据]** 选项卡。 您现在可以拖放文件或浏览计算机以查找要添加的文件。

>[!NOTE]
>
>Platform支持两种用于数据引入的文件类型，即Parquet或JSON。 一次最多可以添加5个文件，每个文件的最大文件大小为1 GB。

![“添加数据”选项卡](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## 上传文件 {#upload-file}

拖放（或浏览并选择）要上载的Parquet或JSON文件后， [!DNL Platform] 将立即开始处理该文件并 **[!UICONTROL 正在上传]** 对话框将显示在 **[!UICONTROL 添加数据]** 选项卡，显示文件上传进度。

![上传对话框](../images/tutorials/ingest-batch-data/uploading-file.png)

## 数据集量度

文件上传完成后， **[!UICONTROL 数据集活动]** 选项卡不再显示“未添加任何批次”。 相反， **[!UICONTROL 数据集活动]** 选项卡现在显示数据集量度。 此时，所有量度都将显示“0”，因为批次尚未加载。

选项卡底部是一个列表，其中显示 **[!UICONTROL 批次ID]** 通过摄取的数据中 [“将数据添加到数据集”](#add-data-to-dataset) 进程。 另外，还包括与批相关的信息，包括摄取日期、摄取记录数和当前批状态。

![数据集量度](../images/tutorials/ingest-batch-data/batch-id.png)

## 批次详细信息

单击 **[!UICONTROL 批次ID]** 查看 **[!UICONTROL 批次概述]**，显示有关批次的其他详细信息。 加载完批次后，批次的相关信息将更新，以显示摄取的记录数和文件大小。 状态还将更改为“成功”或“失败”。 如果批处理失败， **[!UICONTROL 错误代码]** 部分将包含有关摄取期间出现的任何错误的详细信息。

有关批量摄取的更多信息和常见问题解答，请参阅 [批量摄取疑难解答指南](../batch-ingestion/troubleshooting.md).

返回 **[!UICONTROL 数据集活动]** 屏幕上，单击数据集的名称(**[!UICONTROL 忠诚度详细信息]**)。

![批次概述](../images/tutorials/ingest-batch-data/batch-details.png)

## 预览数据集

在数据集准备就绪后，可以使用选项 **[!UICONTROL 预览数据集]** 显示在顶部 **[!UICONTROL 数据集活动]** 选项卡。

单击 **[!UICONTROL 预览数据集]** 以打开一个对话框，其中显示数据集中的示例数据。 如果数据集是使用架构创建的，则数据集架构的详细信息将显示在预览的左侧。 您可以使用箭头展开架构以查看架构结构。 预览数据中的每个列标题表示数据集中的一个字段。

![数据集详细信息](../images/tutorials/ingest-batch-data/dataset-preview.png)

## 后续步骤和其他资源

现在，您已创建一个数据集并成功将数据摄取到 [!DNL Experience Platform]中，您可以重复这些步骤以创建新数据集或将更多数据摄取到现有数据集中。

要了解有关批量摄取的更多信息，请阅读 [批量摄取概述](../batch-ingestion/overview.md) 并通过观看以下视频来补充您的学习。

>[!WARNING]
>
>此 [!DNL Platform] 以下视频中显示的UI已过期。 有关最新的UI屏幕截图和功能，请参阅上述文档。

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
