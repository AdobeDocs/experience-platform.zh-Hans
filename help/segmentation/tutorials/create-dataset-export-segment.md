---
solution: Experience Platform
title: 创建用于导出受众的数据集
type: Tutorial
description: 了解如何使用Experience PlatformUI创建可用于导出受众的数据集。
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 1%

---

# 创建用于导出受众的数据集

[!DNL Adobe Experience Platform]允许您根据特定属性将客户配置文件划分为受众。 创建区段定义后，您可以将生成的受众导出到可在其中进行访问和操作的数据集。 为了成功导出，必须正确配置数据集。

本教程将介绍创建数据集所需的步骤，该数据集可用于使用[!DNL Experience Platform] UI导出受众。

本教程与教程中有关[评估和访问分段结果](./evaluate-a-segment.md)的步骤直接相关。 区段定义评估教程提供了使用[!DNL Catalog Service] API创建数据集的步骤，而本教程则概述了使用[!DNL Experience Platform] UI创建数据集的步骤。

## 快速入门

要导出受众，数据集必须基于[!DNL XDM Individual Profile Union Schema]。 合并架构是系统生成的只读架构，它聚合了共享同一类的所有架构的字段。 有关合并架构的详细信息，请参阅[架构组合基础知识](../../xdm/schema/composition.md#union)指南。

要在UI中查看合并架构，请在左侧导航中选择&#x200B;**[!UICONTROL 配置文件]**，然后选择&#x200B;**[!UICONTROL 合并架构]**，如下所示。

![联合架构选项卡已突出显示。](../images/tutorials/segment-export-dataset/union.png)

## 数据集工作区

[!UICONTROL 数据集]工作区允许您查看和管理组织的所有数据集。

在左侧导航中选择&#x200B;**[!UICONTROL 数据集]**&#x200B;以访问工作区，然后选择&#x200B;**[!UICONTROL 浏览]**。 此选项卡显示数据集及其详细信息的列表。 根据每列的宽度，您可能需要向左或向右滚动才能查看所有列。

>[!NOTE]
>
>选择搜索栏旁的筛选器图标以使用筛选功能仅查看那些为[!DNL Real-Time Customer Profile]启用的数据集。

![将显示数据集工作区。](../images/tutorials/segment-export-dataset/browse.png)

## 创建数据集

要创建数据集，请选择&#x200B;**[!UICONTROL 创建数据集]**。

![已突出显示“创建数据集”按钮。](../images/tutorials/segment-export-dataset/create-dataset.png)

在下一个屏幕上，选择&#x200B;**[!UICONTROL 从架构创建数据集]**。

![从架构创建数据集选项突出显示。](../images/tutorials/segment-export-dataset/create-from-schema.png)

## 选择XDM Individual Profile Union架构

要选择要在数据集中使用的[!DNL XDM Individual Profile Union Schema]，请在&#x200B;**[!UICONTROL 选择架构]**&#x200B;屏幕上找到“[!UICONTROL XDM个人配置文件]”架构。 选择架构后，您可以确认它是否是右边栏中&#x200B;**[!UICONTROL API使用情况]**&#x200B;下的合并架构。 如果[!UICONTROL 架构]路径以`_union`结尾，则它是一个合并架构。

>[!NOTE]
>
>尽管联合架构按定义参与实时客户档案，但由于与传统架构相同的方式未针对档案启用它们，因此它们被列为“未启用”。

选择&#x200B;**[!UICONTROL XDM Individual Profile]**&#x200B;旁边的单选按钮，然后选择&#x200B;**[!UICONTROL 下一步]**。

![已突出显示XDM个人资料架构。](../images/tutorials/segment-export-dataset/select-schema.png)

## 配置数据集

在下一个屏幕上，必须为数据集提供一个名称。 您还可以添加可选描述。

**有关数据集名称的注释：**

* 数据集名称应简短且具有描述性，以便之后能够在库中轻松找到数据集。
* 数据集名称必须是唯一的，这意味着它们还应该足够具体，以便将来不会重复使用。
* 您应使用描述字段提供有关数据集的附加信息，因为它可能有助于其他用户将来区分数据集。

在数据集具有名称和描述后，选择&#x200B;**[!UICONTROL 完成]**。

![将显示“配置数据集”页面。 配置选项突出显示。](../images/tutorials/segment-export-dataset/configure-dataset.png)

## 数据集活动

创建数据集后，您将获得该数据集的活动页面。 您应该会在工作区的左上角看到数据集的名称，同时还会看到“未添加任何批次”的通知。 这是正常情况，因为您尚未将任何批次添加到此数据集。

右边栏包含与新数据集相关的信息，例如数据集ID、名称、描述、架构等。 请记下&#x200B;**[!UICONTROL 数据集ID]**，因为此值是完成受众导出工作流所必需的。

![将显示数据集活动页面。 数据集ID已突出显示，因为未来步骤需要记录此值。](../images/tutorials/segment-export-dataset/activity.png)

## 后续步骤

现在您已经基于[!DNL XDM Individual Profile Union Schema]创建了一个数据集，您可以使用该数据集ID来继续[评估和访问区段定义结果](./evaluate-a-segment.md)教程。

此时，请返回到“评估区段定义结果”教程，并从导出受众工作流的[为受众成员生成配置文件](./evaluate-a-segment.md#generate-profiles)步骤中选取。
