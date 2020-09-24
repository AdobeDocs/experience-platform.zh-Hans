---
keywords: Experience Platform;home;popular topics; analytics;classifications
description: 本教程提供了在UI中创建Adobe Analytics分类数据连接器以将分类数据引入Adobe Experience Platform的步骤。
solution: Experience Platform
title: 在UI中创建Adobe Analytics分类数据连接器
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 2%

---


# 在UI中创建Adobe Analytics分类数据连接器

本教程提供了在UI中创建Adobe Analytics分类数据连接器以将分类数据引入Adobe Experience Platform的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [[!DNL沙箱]](../../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

## 选择您的分类

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择“源”以访问源工作区。 “目 **[!UICONTROL 录]** ”屏幕显示可用源，用于创建入站连接。 每个源卡都显示一个选项，用于配置新帐户或向现有帐户添加数据。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在Adobe **[!UICONTROL 应用程序]** 类别下，选择 **[!UICONTROL Adobe Analytics卡]** ，然后选择 **[!UICONTROL 将数据添加]** 到使用Analytics分类数据的开始。

![](../../../../images/tutorials/create/classifications/catalog.png)

将显 **[!UICONTROL 示分析源添加数据]** 步骤。 从顶 **[!UICONTROL 部标题]** 中选择“分类”以查看数据集的 [!DNL Classifications] 列表，包括有关其DimensionID、 **[!UICONTROL 报表包名称]**、报表包 ******** ID和的信息。

每页最多显示十个可 [!DNL Classifications] 供选择的不同数据集。 选 **[!UICONTROL 择页]** 面底部的“下一步”以浏览更多选项。 右侧的面板显示您选择的 [!DNL Classifications] 数据集总数及其名称。 此面板还允许您删除可能因错 [!DNL Classifications] 误而选择的任何数据集，或通过一个操作清除所有选择。

您最多可以选择30个不 [!DNL Classifications] 同的数据集 [!DNL Platform]。

选择数据集 [!DNL Classifications] 后， **[!UICONTROL 选择]** 页面右上方的“下一步”。

![](../../../../images/tutorials/create/classifications/add-data.png)

## 查看分类

此时 **[!UICONTROL 会显示]** “审阅”步骤，允许您在创建选定 [!DNL Classifications] 的数据集之前查看它。 详细信息按以下类别分组：

* **[!UICONTROL 连接]**:显示源平台和连接状态。
* **[!UICONTROL 数据类型]**:显示选定的数量 [!DNL Classifications]。
* **[!UICONTROL 计划]**:显示数据的同步 [!DNL Classifications] 频率。

查看数据流后，单击 **[!UICONTROL 完成]** ，并允许一段时间创建数据流。

![](../../../../images/tutorials/create/classifications/review.png)

## 监视分类数据流

创建数据流后，您可以监视通过它摄取的数据。 从“目 **[!UICONTROL 录]** ”屏幕中，选 **[!UICONTROL 择“数据流]** ”以视图与您的帐户关联的已建立流 [!DNL Classifications] 列表。

![](../../../../images/tutorials/create/classifications/dataflows.png)

出现 **[!UICONTROL “数据]** 流”屏幕。 本页是数据流的列表，包括有关其名称、源数据和数据流运行状态的信息。 右侧是包含与 **[!UICONTROL 数据流]** 相关的元数据的“属性 [!DNL Classifications] ”面板。

选择要 **[!UICONTROL 访问的目标]** 数据集。

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

“数 **[!UICONTROL 据集活动]** ”页显示有关您选择的目标数据集的信息，包括有关其批处理状态、数据集ID和模式的详细信息。

>[!IMPORTANT]
>
>虽然其他源连接器可以删除数据集，但Analytics Classifications Data Connector当前不支持此功能。 如果您误删除了数据集，请与Adobe客户服务部联系。

![](../../../../images/tutorials/create/classifications/dataset.png)


## 后续步骤

通过遵循本教程，您创建了一个将数据引入其中的Analytics Classifications [!DNL Classifications] 数据连接器 [!DNL Platform]。 有关更多信息和数据，请参阅以 [!DNL Analytics] 下文档 [!DNL Classifications] 信息：

* [Analytics数据连接器概述](../../../../connectors/adobe-applications/analytics.md)
* [在UI中创建Analytics数据连接器](./analytics.md)
* [关于分类](https://docs.adobe.com/content/help/zh-Hans/analytics/components/classifications/c-classifications.html#)