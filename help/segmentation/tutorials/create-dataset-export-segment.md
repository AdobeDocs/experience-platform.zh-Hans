---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 创建用于导出受众段的数据集
topic: tutorial
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---


# 创建用于导出受众段的数据集

[!DNL Adobe Experience Platform] 使您能够根据特定属性轻松地将客户用户档案细分为受众。 创建受众后，您可以将该数据导出到数据集，在数据集中对其进行访问和操作。 要成功导出，必须正确配置数据集。

本教程将逐步介绍创建可用于使用UI导出受众段的数据集所需的 [!DNL Experience Platform] 步骤。

本教程直接与教程中概述的用于评估和访 [问区段结果的步骤相关](./evaluate-a-segment.md)。 评估区段教程提供了使用API创建数据集的步 [!DNL Catalog Service] 骤，而本教程则概括介绍使用UI创建数据集的 [!DNL Experience Platform] 步骤。

## 入门指南

要导出区段，数据集必须基于 [!DNL XDM Individual Profile Union Schema]。 合并模式是系统生成的只读模式，它聚合共享同一类的所有模式的字段，在本例中为类 [!DNL XDM Individual Profile] 。 有关合并视图模式的更多信息，请参 [阅模式注册开发人员指南的实时客户用户档案部分](../../xdm/schema/composition.md#union)。

要在UI中视图合并模式 **[!UICONTROL ，请单击左侧导航中的]** 用户档案 **[!UICONTROL ，然后单击合并模式]** 选项卡，如下所示。

![合并模式选项卡在Experience PlatformUI中](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## 数据集工作区

UI中的数据集工 [!DNL Experience Platform] 作区允许您视图和管理IMS组织创建的所有数据集，并创建新数据集。

要视图数据集工作区，请单 **[!UICONTROL 击左侧导]** 航中的“数据集 **[!UICONTROL ”，然后单击“浏览”]** 选项卡。 数据集工作区包含数据集列表，包 **[!UICONTROL 括显示]** Name、Source **[!UICONTROL (date and time)、Source]** 、SourceBatch和 **************** Last Batch Status的列，如数据集的日期和上次创建模式更新的时间。 根据每列的宽度，可能需要向左或向右滚动才能看到所有列。

>[!NOTE]
>
>单击搜索栏旁边的筛选器图标，以使用筛选功能仅视图那些启用的数据集 [!DNL Real-time Customer Profile]。

![视图所有数据集](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## 创建数据集

要创建数据集，请单 **[!UICONTROL 击“数据集]** ”工作区右上角的“创 [!UICONTROL 建数据集] ”。

![单击创建数据集](../images/tutorials/segment-export-dataset/dataset-click-create.png)

在“创 **[!UICONTROL 建数据集]** ”屏幕上，单 **[!UICONTROL 击“从模式创建数据集]** ”以继续。

![选择数据源](../images/tutorials/segment-export-dataset/create-dataset.png)

## 选择XDM单独用户档案合并模式

要选择要 [!DNL XDM Individual Profile Union Schema] 在数据集中使用的用户档案，请在“选[!UICONTROL 择模式”屏幕上查找类型为“]合并[!UICONTROL ”的“XDM]Individual Signidual **** ”模式。

选择了“XDM Individual Adobile **[!UICONTROL 用户档案”旁边的单选按钮]**，然后 **[!UICONTROL 单击右]** 上角的“下一步”。

![选择模式](../images/tutorials/segment-export-dataset/select-schema.png)

## 配置数据集

在“配 **[!UICONTROL 置数据集]** ”屏幕上，您将需要为数据集 **[!UICONTROL 指定名称]** ，并且还可 **[!UICONTROL 能提供]** 数据集的“描述”。

**数据集名称的注释：**
- 数据集名称应简短且具有描述性，以便以后可以在库中轻松找到该数据集。
- 数据集名称必须唯一，这意味着它也应足够具体，以便将来不再重用。
- 最好使用描述字段提供有关数据集的其他信息，因为这可能有助于其他用户将来区分不同数据集。

数据集有名称和说明后，单击“完 **[!UICONTROL 成”]**。

![配置数据集](../images/tutorials/segment-export-dataset/configure-dataset.png)

## 数据集活动

现在已创建空数据集，您已返回到“数据集 **[!UICONTROL ”工作区]** 的“数据集 [!UICONTROL 活动] ”选项卡。 您应当在工作区的左上角看到数据集的名称，并显示通知“尚未添加批次”。 由于尚未向此数据集添加任何批，因此应该设置此值。

在数据集的右侧，您将看到与新数据集 **[!UICONTROL 相关的]** Info标签信息，如 **[!UICONTROL Info]**&#x200B;标签、Info Tab和新数据集，如 ************************ ID、AD、TableId名称、模式名、、和源。 “信 [!UICONTROL 息] ”选项卡还包含有关数据集创建时间及其上次修 **[!UICONTROL 改]** 日期 **[!UICONTROL 的信息]** 。

请记下数据集 **[!UICONTROL ID]**，因为完成受众段导出工作流时需要此值。

![数据集活动](../images/tutorials/segment-export-dataset/dataset-activity.png)

## 后续步骤

现在，您已基于创建了数据集 [!DNL XDM Individual Profile Union Schema]，可以使用 **[!UICONTROL 数据集ID]** 继续 [评估和访问区段结果教程](./evaluate-a-segment.md) 。

此时，请返回评估区段结果教程，并从导出区段工作流 [的用户档案成员生成受众](./evaluate-a-segment.md#generate-profiles) ，步骤中进行选择。
