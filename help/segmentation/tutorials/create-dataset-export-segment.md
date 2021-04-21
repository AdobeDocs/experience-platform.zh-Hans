---
keywords: Experience Platform；主页；热门主题；分段服务；分段；分段；创建数据集；导出受众段；导出段；
solution: Experience Platform
title: 创建用于导出受众区段的数据集
topic-legacy: tutorial
type: Tutorial
description: 本教程将逐步介绍创建可用于使用受众 UI导出Experience Platform区段的数据集所需的步骤。
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 1%

---

# 创建用于导出受众段的数据集

[!DNL Adobe Experience Platform] 使您能够根据特定属性轻松地将客户用户档案细分为受众。创建区段后，您可以将该受众导出到数据集，以便在该数据集中访问和执行操作。 要成功导出，必须正确配置数据集。

本教程将介绍创建可用于使用[!DNL Experience Platform] UI导出受众段的数据集所需的步骤。

本教程直接与教程中概述的用于[评估和访问区段结果](./evaluate-a-segment.md)的步骤相关。 评估区段教程提供了使用[!DNL Catalog Service] API创建数据集的步骤，而本教程则概述了使用[!DNL Experience Platform] UI创建数据集的步骤。

## 入门指南

要导出区段，数据集必须基于[!DNL XDM Individual Profile Union Schema]。 合并模式是系统生成的只读模式，它聚合共享同一类的所有模式的字段，在本例中为[!DNL XDM Individual Profile]类。 有关合并视图模式的详细信息，请参阅模式注册开发人员指南](../../xdm/schema/composition.md#union)的[实时客户用户档案部分。

要在UI中视图合并模式，请单击左侧导航中的&#x200B;**[!UICONTROL Profiles]**，然后单击&#x200B;**[!UICONTROL Union schema]**&#x200B;选项卡，如下所示。

![合并模式选项卡](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## 数据集工作区

[!DNL Experience Platform] UI中的数据集工作区允许您视图和管理IMS组织创建的所有数据集，并创建新数据集。

要视图数据集工作区，请单击左侧导航中的&#x200B;**[!UICONTROL Datasets]**，然后单击&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡。 数据集工作区包含数据集的列表，包括显示名称、创建（日期和时间）、源、模式和上次批处理状态的列，以及上次更新数据集的日期和时间。 根据每列的宽度，可能需要向左或向右滚动才能看到所有列。

>[!NOTE]
>
>单击搜索栏旁边的筛选器图标，以使用筛选功能仅视图那些为[!DNL Real-time Customer Profile]启用的数据集。

![视图所有数据集](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## 创建数据集

要创建数据集，请单击&#x200B;**[!UICONTROL Datasets]**&#x200B;工作区右上角的&#x200B;**[!UICONTROL Create Dataset]**。

![单击创建数据集](../images/tutorials/segment-export-dataset/dataset-click-create.png)

在&#x200B;**[!UICONTROL Create Dataset]**&#x200B;屏幕上，单击&#x200B;**[!UICONTROL Create Dataset from Schema]**&#x200B;继续。

![选择数据源](../images/tutorials/segment-export-dataset/create-dataset.png)

## 选择XDM单个用户档案合并模式

要选择[!DNL XDM Individual Profile Union Schema]以在数据集中使用，请在&#x200B;**[!UICONTROL Select Schema]**&#x200B;屏幕上找到类型为“[!UICONTROL Union]”的“[!UICONTROL XDM Individual Profile]”模式。

选择了&#x200B;**[!UICONTROL XDM Individual Profile]**&#x200B;旁边的单选按钮，然后单击右上角的&#x200B;**[!UICONTROL Next]**。

![选择模式](../images/tutorials/segment-export-dataset/select-schema.png)

## 配置数据集

在&#x200B;**[!UICONTROL Configure Dataset]**&#x200B;屏幕上，您将需要为数据集指定名称，并可能提供数据集的说明。

**数据集名称上的注释：**
- 数据集名称应简短且描述性，以便以后可以在库中轻松找到数据集。
- 数据集名称必须唯一，这意味着它也应足够具体，以便将来不会重用。
- 最好使用描述字段提供有关数据集的其他信息，因为这可能有助于其他用户将来区分不同数据集。

数据集有名称和说明后，单击&#x200B;**[!UICONTROL Finish]**。

![配置数据集](../images/tutorials/segment-export-dataset/configure-dataset.png)

## 数据集活动

现在已创建空数据集，您已返回到&#x200B;**[!UICONTROL Datasets]**&#x200B;工作区中的&#x200B;**[!UICONTROL Dataset Activity]**&#x200B;选项卡。 您应在工作区的左上角看到数据集的名称，并显示“尚未添加任何批次”通知。 由于您尚未向此数据集添加任何批，因此应该这样做。

在“数据集”工作区的右侧，您将看到&#x200B;**[!UICONTROL Info]**&#x200B;选项卡，其中包含与新数据集相关的信息，如数据集ID、名称、描述、表名、模式、流和源。 **[!UICONTROL Info]**&#x200B;选项卡还包含有关数据集创建时间及其上次修改日期的信息。

请注意&#x200B;**[!UICONTROL Dataset ID]**，因为完成受众段导出工作流需要此值。

![数据集活动](../images/tutorials/segment-export-dataset/dataset-activity.png)

## 后续步骤

现在，您已基于[!DNL XDM Individual Profile Union Schema]创建了数据集，可以使用数据集ID继续[评估和访问区段结果](./evaluate-a-segment.md)教程。

此时，请返回评估区段结果教程，并从导出区段工作流的[为受众成员生成用户档案](./evaluate-a-segment.md#generate-profiles)步骤中进行学习。
