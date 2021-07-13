---
keywords: Experience Platform；主页；热门主题；分段服务；分段；创建数据集；导出受众区段；导出区段；
solution: Experience Platform
title: 创建用于导出受众区段的数据集
topic-legacy: tutorial
type: Tutorial
description: 本教程将演示创建数据集所需的步骤，数据集可用于使用Experience PlatformUI导出受众区段。
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: 44d7e11e79ed0e6041ff2e4438ddb7141ae3532d
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 1%

---

# 创建用于导出受众区段的数据集

[!DNL Adobe Experience Platform] 允许您根据特定属性将客户用户档案细分为受众。创建区段后，您可以将该受众导出到可在其中访问并执行操作的数据集。 要成功导出，必须正确配置数据集。

本教程将介绍创建数据集以用于使用[!DNL Experience Platform] UI导出受众区段所需的步骤。

本教程与本教程中介绍的有关[评估和访问区段结果](./evaluate-a-segment.md)的步骤直接相关。 区段评估教程提供了使用[!DNL Catalog Service] API创建数据集的步骤，而本教程则概述了使用[!DNL Experience Platform] UI创建数据集的步骤。

## 快速入门

要导出区段，数据集必须基于[!DNL XDM Individual Profile Union Schema]。 并集架构是系统生成的只读架构，用于聚合共享同一类的所有架构的字段。 有关并集架构的更多信息，请参阅[架构组合基础知识指南](../../xdm/schema/composition.md#union)。

要在UI中查看并集架构，请在左侧导航中选择&#x200B;**[!UICONTROL Profiles]**，然后选择&#x200B;**[!UICONTROL 并集架构]**，如下所示。

![Experience PlatformUI中的并集架构选项卡](../images/tutorials/segment-export-dataset/union.png)


## 数据集工作区

[!UICONTROL Datasets]工作区允许您查看和管理组织的所有数据集。

在左侧导航中选择&#x200B;**[!UICONTROL 数据集]**&#x200B;以访问工作区，然后选择&#x200B;**[!UICONTROL 浏览]**。 此选项卡显示数据集列表及其详细信息。 根据每列的宽度，可能需要向左或向右滚动才能看到所有列。

>[!NOTE]
>
>选择搜索栏旁边的过滤器图标，以使用过滤功能仅查看为[!DNL Real-time Customer Profile]启用的数据集。

![查看数据集](../images/tutorials/segment-export-dataset/browse.png)

## 创建数据集

要创建数据集，请选择&#x200B;**[!UICONTROL 创建数据集]**。

![选择创建数据集](../images/tutorials/segment-export-dataset/create-dataset.png)

在下一个屏幕中，选择&#x200B;**[!UICONTROL 从架构创建数据集]**。

![选择数据源](../images/tutorials/segment-export-dataset/create-from-schema.png)

## 选择XDM单个配置文件合并架构

要选择[!DNL XDM Individual Profile Union Schema]以在数据集中使用，请在&#x200B;**[!UICONTROL 选择架构]**&#x200B;屏幕上找到“[!UICONTROL XDM Indivial Profile]”架构。 选择架构后，您可以确认它是否为右边栏中&#x200B;**[!UICONTROL API使用]**&#x200B;下的并集架构。 如果[!UICONTROL Schema]路径以`_union`结尾，则它是并集架构。

>[!NOTE]
>
>尽管合并架构按照定义参与实时客户资料，但由于未以与传统架构相同的方式为资料启用，因此它们被列为“未启用”。

选择&#x200B;**[!UICONTROL XDM Indivial Profile]**&#x200B;旁边的单选按钮，然后选择&#x200B;**[!UICONTROL Next]**。

![选择架构](../images/tutorials/segment-export-dataset/select-schema.png)

## 配置数据集

在下一个屏幕中，您必须为数据集命名。 您还可以添加可选描述。

**有关数据集名称的注释：**
* 数据集名称应该简短且具有描述性，以便以后可以在库中轻松找到该数据集。
* 数据集名称必须是唯一的，这意味着它们还应具有足够的特定性，以便将来不会重复使用。
* 最佳做法是使用描述字段提供有关数据集的其他信息，因为这可能有助于其他用户将来区分不同的数据集。

在数据集具有名称和描述后，选择&#x200B;**[!UICONTROL 完成]**。

![配置数据集](../images/tutorials/segment-export-dataset/configure-dataset.png)

## 数据集活动

创建数据集后，您会打开该数据集的活动页面。 您应会在工作区的左上角看到数据集的名称，并收到“尚未添加任何批次”通知。 由于您尚未向此数据集添加任何批次，因此应该会出现这种情况。

右边栏包含与新数据集相关的信息，如数据集ID、名称、描述、架构等。 请注意&#x200B;**[!UICONTROL 数据集ID]**，因为完成受众区段导出工作流需要此值。

![数据集活动](../images/tutorials/segment-export-dataset/activity.png)

## 后续步骤

现在，您已基于[!DNL XDM Individual Profile Union Schema]创建数据集，接下来可以使用数据集ID继续执行[评估和访问区段结果](./evaluate-a-segment.md)教程。

此时，请返回到评估区段结果教程，并从导出区段工作流的[为受众成员生成配置文件](./evaluate-a-segment.md#generate-profiles)步骤中进行选择。
