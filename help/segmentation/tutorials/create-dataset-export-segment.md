---
keywords: Experience Platform；主页；热门主题；分段服务；分段；创建数据集；导出受众区段；导出区段；
solution: Experience Platform
title: 创建用于导出受众区段的数据集
type: Tutorial
description: 本教程将演示创建数据集所需的步骤，数据集可用于使用Experience PlatformUI导出受众区段。
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# 创建用于导出受众区段的数据集

[!DNL Adobe Experience Platform] 允许您根据特定属性将客户用户档案细分为受众。 创建区段后，您可以将该受众导出到可在其中访问并执行操作的数据集。 要成功导出，必须正确配置数据集。

本教程将逐步介绍创建数据集以用于使用 [!DNL Experience Platform] UI。

本教程直接与 [评估和访问区段结果](./evaluate-a-segment.md). 区段评估教程提供了使用创建数据集的步骤 [!DNL Catalog Service] API，而本教程则概述使用创建数据集的步骤 [!DNL Experience Platform] UI。

## 快速入门

要导出区段，数据集必须基于 [!DNL XDM Individual Profile Union Schema]. 并集架构是系统生成的只读架构，用于聚合共享同一类的所有架构的字段。 有关并集模式的更多信息，请参阅 [架构组合的基础知识](../../xdm/schema/composition.md#union).

要在UI中查看并集架构，请选择 **[!UICONTROL 用户档案]** 在左侧导航中，选择 **[!UICONTROL 并集架构]** 如下所示。

![并集架构选项卡会突出显示。](../images/tutorials/segment-export-dataset/union.png)

## 数据集工作区

的 [!UICONTROL 数据集] 工作区允许您查看和管理组织的所有数据集。

选择 **[!UICONTROL 数据集]** 在左侧导航中以访问工作区，然后选择 **[!UICONTROL 浏览]**. 此选项卡显示数据集列表及其详细信息。 根据每列的宽度，可能需要向左或向右滚动才能看到所有列。

>[!NOTE]
>
>选择搜索栏旁边的过滤器图标，以使用过滤功能仅查看为 [!DNL Real-Time Customer Profile].

![将显示数据集工作区。](../images/tutorials/segment-export-dataset/browse.png)

## 创建数据集

要创建数据集，请选择 **[!UICONTROL 创建数据集]**.

![“创建数据集”按钮将突出显示。](../images/tutorials/segment-export-dataset/create-dataset.png)

在下一个屏幕上，选择 **[!UICONTROL 从架构创建数据集]**.

![“从架构创建数据集”选项已突出显示。](../images/tutorials/segment-export-dataset/create-from-schema.png)

## 选择XDM单个配置文件合并架构

选择 [!DNL XDM Individual Profile Union Schema] 要在数据集中使用，请找到“[!UICONTROL XDM个人配置文件]“架构” **[!UICONTROL 选择架构]** 屏幕。 选择架构后，您可以确认它是否为下的并集架构 **[!UICONTROL API使用情况]** 中。 如果 [!UICONTROL 架构] 路径结束于 `_union`，这是一个联合模式。

>[!NOTE]
>
>尽管合并架构按照定义参与实时客户资料，但由于未以与传统架构相同的方式为资料启用，因此它们被列为“未启用”。

选择旁边的单选按钮 **[!UICONTROL XDM个人配置文件]**，然后选择 **[!UICONTROL 下一个]**.

![XDM个人用户档案架构将突出显示。](../images/tutorials/segment-export-dataset/select-schema.png)

## 配置数据集

在下一个屏幕中，您必须为数据集命名。 您还可以添加可选描述。

**有关数据集名称的注释：**

* 数据集名称应该简短且具有描述性，以便以后可以在库中轻松找到该数据集。
* 数据集名称必须是唯一的，这意味着它们还应具有足够的特定性，以便将来不会重复使用。
* 最佳做法是使用描述字段提供有关数据集的其他信息，因为这可能有助于其他用户将来区分不同的数据集。

在数据集具有名称和描述后，选择 **[!UICONTROL 完成]**.

![此时会显示“配置数据集”页面。 配置选项会突出显示。](../images/tutorials/segment-export-dataset/configure-dataset.png)

## 数据集活动

创建数据集后，您会打开该数据集的活动页面。 您应会在工作区的左上角看到数据集的名称，并收到“尚未添加任何批次”通知。 由于您尚未向此数据集添加任何批次，因此应该会出现这种情况。

右边栏包含与新数据集相关的信息，如数据集ID、名称、描述、架构等。 请注意 **[!UICONTROL 数据集ID]**，因为完成受众区段导出工作流需要此值。

![此时会显示数据集活动页面。 数据集ID会突出显示，因为在将来的步骤中需要注意此值。](../images/tutorials/segment-export-dataset/activity.png)

## 后续步骤

现在，您已基于 [!DNL XDM Individual Profile Union Schema]，则可以使用数据集ID继续 [评估和访问区段结果](./evaluate-a-segment.md) 教程。

此时，请返回到评估区段结果教程，并从 [为受众成员生成用户档案](./evaluate-a-segment.md#generate-profiles) 导出区段工作流的步骤。
