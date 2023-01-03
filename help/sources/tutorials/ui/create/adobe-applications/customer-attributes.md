---
keywords: Experience Platform；主页；热门主题；客户属性
solution: Experience Platform
title: 在UI中创建客户属性源连接
topic-legacy: overview
type: Tutorial
description: 了解如何在UI中创建源连接，以将客户属性配置文件数据引入Adobe Experience Platform。
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 4%

---

# 在UI中创建客户属性源连接

本教程提供了在UI中创建源连接以将客户属性配置文件数据导入Adobe Experience Platform的步骤。 有关客户属性的更多信息，请参阅 [客户属性概述](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=zh-Hans).

>[!IMPORTANT]
>
>客户属性来源当前不支持启用或禁用数据流。

## 创建源连接

>[!NOTE]
>
>如果您已经为客户属性配置文件数据建立了源连接，则与源连接的选项将被禁用。

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕显示您可以创建连接的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在 [!UICONTROL Adobe应用程序] 类别，选择 **[!UICONTROL 客户属性]** 然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/customer-attributes/catalog.png)

### 选择客户属性数据源

的 [!UICONTROL 添加数据] 屏幕列出了客户属性的所有可用数据源。 每个“客户属性”源连接只能选择一个数据集。

>[!NOTE]
>
>字段组、架构和数据集作为流量配置的一部分现成创建。 它们将保持原样，您将需要手动删除它们。

客户属性来源不支持架构演变。 如果客户属性数据源的架构输入发生更改，则它将与Platform不兼容。 作为解决方法，您可以删除现有客户属性数据流及其关联的数据集、架构和字段组，然后使用更新的架构和数据源创建一个新数据流。

>[!IMPORTANT]
>
>虽然您可以删除客户属性数据流，但即使在删除数据流后，其相应的数据集仍将保留。 请参阅 [删除数据集](../../../../../catalog/datasets/user-guide.md) 以了解有关如何手动删除数据集的步骤。

要创建新连接，请从列表中选择数据源，然后选择 **[!UICONTROL 下一个]**.

![添加数据](../../../../images/tutorials/create/customer-attributes/add-data.png)

### 提供数据流详细信息

的 [!UICONTROL 数据流详细信息] 步骤，以便为数据流提供名称和简要说明。 在此过程中，您还可以配置 [!UICONTROL 错误诊断], [!UICONTROL 部分摄取]和 [!UICONTROL 警报].

[!UICONTROL 错误诊断] 为数据流中发生的任何错误记录启用详细的错误消息生成，而 [!UICONTROL 部分摄取] 允许您摄取包含错误的数据，最多可达您手动定义的特定阈值。 请参阅 [部分批量摄取概述](../../../../../ingestion/batch-ingestion/partial.md) 以了解更多信息。

您可以启用警报以接收有关数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅源警报](../../alerts.md).

完成向数据流提供详细信息后，选择 **[!UICONTROL 下一个]**.

![数据流详细信息](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### 审核数据流

的 [!UICONTROL 审阅] 步骤，允许您在创建新数据流之前查看新数据流。 详细信息按以下类别分组：

* **[!UICONTROL 连接]**:显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **[!UICONTROL 分配数据集和映射字段]**:显示源数据被摄取到的数据集，包括该数据集附加的架构。

![审查](../../../../images/tutorials/create/customer-attributes/review.png)

## 后续步骤

创建连接后，将自动创建目标架构和数据集，以包含传入数据。完成初始摄取后，下游Platform服务(例如 [!DNL Real-Time Customer Profile] 和 [!DNL Segmentation Service]. 有关更多详细信息，请参阅以下文档：

* [[!DNL Real-Time Customer Profile] 概述](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概述](../../../../../segmentation/home.md)
