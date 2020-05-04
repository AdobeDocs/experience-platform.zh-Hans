---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Adobe Analytics源连接器
topic: overview
translation-type: tm+mt
source-git-commit: d2f8e11591b30a0bfd345e56a33a8bb62501358c

---


# 在UI中创建Adobe Analytics源连接器

本教程提供了在UI中创建Adobe Analytics源连接器以将消费者数据引入Adobe Experience Platform的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
* [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [沙箱](../../../../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和改进数字体验应用程序。

## 使用Adobe Analytics创建源连接

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左 **[!UICONTROL Sources]** 侧导航栏中选择以访问源工作区。 “目 *录* ”屏幕显示用于创建入站连接的可用源，每个源显示与它们关联的现有帐户和数据集流的数量。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在Adobe *应用程序* 类别下， **[!UICONTROL Adobe Analytics]** 选择以在屏幕右侧显示一个信息栏。 信息栏提供所选源的简短描述以及与源或视图其文档的选项。 要视图现有帐户，请选择 **[!UICONTROL Accounts]**。

![](../../../../images/tutorials/create/analytics/catalog.png)

### 选择数据

此时 *将显示Adobe* Analytics步骤。 此屏幕上列出了以前为Analytics建立的数据集流。 您可以通过单击创建新数据集流 **[!UICONTROL Select data]**。

>[!NOTE] 可以建立与源的多个绑定连接以引入不同的数据。

![](../../../../images/tutorials/create/analytics/dataset-flows.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

从可用报表包的列表中，选择要引入平台的报表包，然后单击 **[!UICONTROL Next]**。

![](../../../../images/tutorials/create/analytics/select-data.png)

### 命名数据集流

出现 *数据集流详细信* 息步骤，您必须在该步骤中为数据集流提供名称和可选描述。 选择 **[UICONTROL! 完成后]** ，下一步。

![](../../../../images/tutorials/create/analytics/dataset-flow-detail.png)

### 查看数据集流

此时 *会显示* “审阅”步骤，允许您在创建新的Analytics绑定数据集流之前查看该流。 连接的详细信息按类别分组，包括：

* *连接*: 显示源连接的类型和所选报表包。
* *分配数据集和地图字段*: 创建其他源连接器时，此容器显示源数据正被引入的数据集，包括数据集所附加的模式。 输出模式和数据集会自动为Analytics数据集流配置。

![](../../../../images/tutorials/create/analytics/review.png)

### 监控数据集流

创建数据集流后，您可以监视通过它摄取的数据。 从“目 *录* ”屏幕中，选 *择“数据集流* ”以视图与您的Analytics帐户关联的已建立流的列表。

![](../../../../images/tutorials/create/analytics/catalog-dataset-flows.png)

出现 *“Dataset flows* （数据集流）”屏幕。 此页上是一对数据集流，包括有关其名称、源数据、创建时间和状态的信息。

连接器将实例化两个数据集流。 一个流代表回填数据，另一个流代表实时数据。 回填数据未配置为用户档案，而是发送到数据湖以用于分析和数据科学用例。

有关回填、实时数据及其各自延迟的详细信息，请参 [阅Analytics Data Connector概述](../../../../connectors/adobe-applications/analytics.md)。

从列表中选择要视图的数据集流。

![](../../../../images/tutorials/create/analytics/backfill.png)

此时将 *显示“数据集活动* ”页。 此页以图表形式显示消息的消费率。 从顶 *部标题* 中选择数据管理以访问标记字段。

![](../../../../images/tutorials/create/analytics/batches.png)

您可以从“视图管理”屏幕数据集流的继 *承标签* 。 要访问特定标签，请选择右上方的编辑按钮。

![](../../../../images/tutorials/create/analytics/data-gov.png)

将出 *现“编辑管理标签* ”面板。 此屏幕允许您访问和编辑数据集流的合同、身份和敏感标签。

有关如何标记来自Analytics的数据的更多信息，请访问数 [据使用标签指南](../../../../../data-governance/labels/user-guide.md)。

![](../../../../images/tutorials/create/analytics/labels.png)

## 后续步骤

创建连接后，将自动创建目标模式和数据集流以包含传入数据。 此外，还会进行数据回填，并收集长达13个月的历史数据。 初始摄取完成时，Analytics数据可供下游平台服务(如实时客户用户档案和细分服务)使用。 有关更多详细信息，请参阅以下文档:

* [实时客户用户档案概述](../../../../../profile/home.md)
* [分段服务概述](../../../../../segmentation/home.md)
* [数据科学工作区概述](../../../../../data-science-workspace/home.md)
* [查询服务概述](../../../../../query-service/home.md)
