---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 创建用于导出受众段的数据集
topic: tutorial
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea

---


# 创建用于导出受众段的数据集

Adobe Experience Platform允许您根据特定属性将客户用户档案轻松细分为受众。 创建区段后，您可以将该受众导出到数据集，在该数据集中可以访问并执行操作。 要成功导出，必须正确配置数据集。

本教程将逐步介绍创建可用于使用Experience Platform UI导出受众区段的数据集所需的步骤。

本教程直接与本教程中概述的用于评估和访问 [区段结果的步骤相关](./evaluate-a-segment.md)。 评估区段教程提供了使用目录API创建数据集的步骤，而本教程则概述了使用Experience Platform UI创建数据集的步骤。

## 入门指南

要导出区段，数据集必须基于XDM单个用户档案合并模式。 合并模式是系统生成的只读模式，它聚合共享同一类的所有模式的字段，在本例中为XDM单个用户档案类。 有关合并视图模式的更多信息，请参 [阅模式注册开发人员指南的实时客户用户档案部分](../../xdm/schema/composition.md#union)。

要在UI中视图合并模式 **，请在左侧导航中单击** 用户档案 ** ，然后单击合并模式选项卡，如下所示。

![合并模式选项卡](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## 数据集工作区

Experience Platform UI中的数据集工作区允许您视图和管理IMS组织创建的所有数据集，并创建新数据集。

要视图数据集工作区，请单 **击左侧导航中的** “数据集”，然后单击“浏 *览* ”选项卡。 数据集包含数据集列表，包括显示 *Name*、 *Source**（日期和时间）、Source*（日期和时间）、 ****** Last Batch Status（最后批）的列，就像日期和创建的“上次更新”的“上次创建的”的“上次更新”的“上次模式”的时间一样。 根据每列的宽度，可能需要向左或向右滚动才能看到所有列。

>[!NOTE] 单击搜索栏旁边的筛选器图标，以使用筛选功能仅视图为“实时客户用户档案”启用的数据集。

![视图所有数据集](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## 创建数据集

要创建数据集，请单击“ **数据集** ”工作区右上角的“创建数据集”。

![单击创建数据集](../images/tutorials/segment-export-dataset/dataset-click-create.png)

在“创 *建数据集* ”屏幕上，单 **击“从模式创建数据集** ”以继续。

![选择数据源](../images/tutorials/segment-export-dataset/create-dataset.png)

## 选择XDM单个用户档案合并模式

要选择要在数据集中使用的XDM个人用户档案合并模式，请在“选择合并”屏幕上找到类型为“模式”的“XDM个人用户档案 ** ”模式。

选择了“ **XDM Individual用户档案”旁的单选按钮**，然后单 **击右上角的** “下一步”。

![选择模式](../images/tutorials/segment-export-dataset/select-schema.png)

## 配置数据集

在“配 **置数据集** ”屏幕上，您需要为数据集指定名称 *，并且可能还提供数据集的* 描述 ** 。

**数据集名称上的注释：**
- 数据集名称应简短且具有描述性，以便以后可以在库中轻松找到数据集。
- 数据集名称必须是唯一的，这意味着该名称也应足够具体，以便将来不会重用。
- 最好使用描述字段提供有关数据集的其他信息，因为这可能有助于其他用户将来区分不同的数据集。

数据集有名称和说明后，单击“完 **成”**。

![配置数据集](../images/tutorials/segment-export-dataset/configure-dataset.png)

## 数据集活动

现在已创建空数据集，并且您已返回到“数据集”工作区 *中的“数据集活动* ”选项卡。 您应当在工作区的左上角看到数据集的名称，并看到通知“尚未添加批次”。 由于您尚未向此数据集添加任何批，因此应该这样做。

在数据集的右侧，您将看到与新数据集相关的 **Info**************** AS、ADD、AD D和A D表名称、AD D模式名称、A D D源、A D流和A D等新工作区的标签信息。 “信息”选项卡还包含有关数据集创建时间及其上次修 *改* 日期 *的信息* 。

请记下数据集 **ID**，因为完成受众段导出工作流程需要此值。

![数据集活动](../images/tutorials/segment-export-dataset/dataset-activity.png)

## 后续步骤

现在，您已基于XDM个人用户档案合并模式创建了一个数据集，现在您可以使用数据集 **ID** ，继续 [评估和访问区段结果教程](./evaluate-a-segment.md) 。

此时，请返回评估区段结果教程，并从导出区段工作流的“为用户档案成员生成 [XDM单个受众](./evaluate-a-segment.md#generate-profiles-for-audience-members) ”步骤 [中学习](./evaluate-a-segment.md#export-a-segment) 。
