---
keywords: Experience Platform;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform
title: 配置客户AI实例
topic: Instance creation
translation-type: tm+mt
source-git-commit: f7c59ef097c00073fbf9f6522b6e70ed24cc8bf1

---


# 配置客户AI实例

作为智能服务的一部分，客户人工智能使您能够生成自定义倾向得分，而不必担心机器学习。

智能服务将客户人工智能作为一种简单易用的Adobe Sensei服务提供，该服务可针对不同的用例进行配置。 以下各节提供了配置客户AI实例的步骤。

## 设置实例 {#set-up-your-instance}

在平台UI中，单击 **[!UICONTROL Services]** 左侧导航中的。 随后 **[!UICONTROL Services]** 将显示浏览器，并显示您可以使用的所有可用服务。 在客户AI的容器中，单击 **[!UICONTROL Open]**。

![](../images/user-guide/navigate-to-service.png)

“客 *户AI* ”屏幕显示所有现有客户AI实例。 单击 **[!UICONTROL Create instance]**。

![](../images/user-guide/dashboard.png)

将出现实例创建工作流，从“设置”( *Setup* )步骤开始。

以下是关于必须为实例提供的值的重要信息：

* 实例的名称将用于显示客户AI得分的所有位置。 因此，名称应描述预测得分代表什么，例如“取消杂志订阅的可能性”。

* 倾向类型决定得分和度量极性的目的。 您可以选择 **[!UICONTROL Churn]** 或 **[!UICONTROL Conversion]**。 有关倾向类型如何影 [响实例的更多信息](./discover-insights.md#scoring-summary) ，请参阅发现洞察文档中评分摘要下的注释。

* 数据源是数据所在的位置。 数据集是用于预测得分的输入数据集。 根据设计，客户人工智能使用消费者体验事件数据来计算倾向得分。 从下拉选择器中选择数据集时，仅列出与客户AI兼容的数据集。

* 默认情况下，将为所有用户档案生成倾向得分，除非指定符合条件的人群。 您可以通过定义条件来指定符合条件的人口，以包括或排除基于用户档案的事件。

提供所需的值，然后单击 **[!UICONTROL Next]**。

![](../images/user-guide/setup.png)

### 定义目标 {#define-a-goal}

将显 *示定义目标步骤* ，该步骤为您提供了一个交互式环境，以便以可视方式定义目标。 目标由一个或多个事件组成，其中每个事件的发生基于其保持的条件。 客户人工智能实例的目标是确定在给定时间范围内实现其目标的可能性。

单 **[!UICONTROL Enter Field Name]** 击并从下拉框列表中选择字段。 单击第二个输入，为事件的条件选择一个子句，然后提供目标值以完成事件。 可通过单击配置其他事件 **[!UICONTROL Add event]**。 最后，通过应用以天为单位的预测时间帧，完成目标，然后单击 **[!UICONTROL Next]**。

![](../images/user-guide/goal.png)

### 配置计划 *（可选）*{#configure-a-schedule}

将显 *示高级* 步骤。 此可选步骤允许您配置计划以自动执行预测运行，定义预测排除以过滤某些事件，或者单击( **[!UICONTROL Finish]** 如果不需要)。

通过配置评分频率设置 *评分计划*。 可以计划每周或每月运行自动预测运行。

![](../images/user-guide/schedule.png)

在计划配置下，您可以定义预测排除，以防止在生成得分时评估满足特定条件的事件。 此功能可用于过滤掉不相关的数据输入。

要排除某些事件，请 **[!UICONTROL Add exclusion]** 单击并定义事件，其方式与定义目标的方式相同。 要删除排除，请单击事件容器右上方的省略号(**[!UICONTROL ...]**)，然后单击 **[!UICONTROL Remove Container]**。

![](../images/user-guide/exclusion.png)

根据需要排除事件，然后 **[!UICONTROL Finish]** 单击以创建实例。

![](../images/user-guide/advanced.png)

如果实例创建成功，将立即触发预测运行，并根据您定义的计划执行后续运行。

>[!NOTE] 根据输入数据的大小，预测运行最长可能需要24小时。

按照本节所述，您配置了客户AI的实例，并执行了预测运行。 在运行成功完成后，得分的洞察会自动用预测得分填充用户档案。 请等待24小时，然后继续本教程的下一节。

## 后续步骤 {#next-steps}

通过遵循本教程，您成功地配置了客户AI的实例并生成了倾向得分。 您现在可以选择使用细分构建器创建具有预 [测得分的客户细分](./create-segment.md) ，或 [通过客户人工智能发掘洞察](./discover-insights.md)。

