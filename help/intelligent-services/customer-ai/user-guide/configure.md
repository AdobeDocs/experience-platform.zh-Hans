---
keywords: Experience Platform;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform
title: 配置客户AI实例
topic: Instance creation
translation-type: tm+mt
source-git-commit: ec0de4c8775367be9e6016529471254ad9f8f453

---


# 配置客户AI实例

作为智能服务的一部分，客户人工智能使您能够生成自定义倾向得分，而不必担心机器学习。

智能服务将客户人工智能作为简单易用的Adobe Sensei服务提供，该服务可针对不同用例进行配置。 以下各节提供配置客户人工智能实例的步骤。

## 设置实例 {#set-up-your-instance}

在平台UI中，单击 **[!UICONTROL Services]** 左侧导航。 将显 **[!UICONTROL Services]** 示浏览器，并显示您可以使用的所有可用服务。 在客户AI的容器中，单击 **[!UICONTROL Open]**。

![](../images/user-guide/navigate-to-service.png)

“客 *户AI* ”屏幕显示所有现有客户AI实例。 单击 **[!UICONTROL Create instance]**。

![](../images/user-guide/dashboard.png)

将出现实例创建工作流，从“设置” *步骤* 开始。

以下是关于必须向实例提供的值的重要信息：

* 在显示客户AI得分的所有位置都使用实例的名称。 因此，名称应描述预测分数所代表的内容，例如“取消杂志订阅的可能性”。

* 倾向类型确定得分和度量极性的目的。 您可以选择 **[!UICONTROL Churn]** 或 **[!UICONTROL Conversion]**。 有关倾向类型如何影 [响实例](./discover-insights.md#scoring-summary) ，请参阅发现洞察文档中评分摘要下的注释。

* 数据源是数据所在的位置。 数据集是用于预测得分的输入数据集。 根据设计，客户人工智能使用消费者体验事件数据来计算倾向得分。 从下拉选择器中选择数据集时，只列出与客户AI兼容的数据集。

* 默认情况下，将为所有用户档案生成倾向得分，除非指定符合条件的人口。 您可以通过定义条件来指定合格的人口，以根据用户档案包含或排除事件。

提供所需的值，然后单击 **[!UICONTROL Next]**。

![](../images/user-guide/setup.png)

### 定义目标 {#define-a-goal}

此时 *会显示* “定义目标”步骤，它提供一个交互式环境，供您以可视方式定义目标。 目标由一个或多个事件组成，其中每个事件的发生基于其所持条件。 客户人工智能实例的目标是确定在给定时间范围内实现其目标的可能性。

单 **[!UICONTROL Enter Field Name]** 击并从下拉列表中选择字段。 单击第二个输入，为事件的条件选择一个子句，然后提供目标值以完成事件。 可通过单击配置其他事件 **[!UICONTROL Add event]**。 最后，通过应用天数的预测时间范围，完成目标，然后单击 **[!UICONTROL Next]**。

![](../images/user-guide/goal.png)

### 配置计划 *（可选）* {#configure-a-schedule}

将显 *示高* 级步骤。 此可选步骤允许您配置计划以自动执行预测运行，定义预测排除以过滤某些事件，或 **[!UICONTROL Finish]** 者单击（如果不需要）。

通过配置评分频率设置 *评分计划*。 可以计划每周或每月运行自动预测运行。

![](../images/user-guide/schedule.png)

在计划配置下，您可以定义预测排除，以防止在生成得分时评估满足特定条件的事件。 此功能可用于过滤掉不相关的数据输入。

要排除某些事件，请 **[!UICONTROL Add exclusion]** 单击并以与定义目标方式相同的方式定义事件。 要删除排除，请单击事件&#x200B;**[!UICONTROL ...]**&#x200B;容器右上方的省略号()，然后单击 **[!UICONTROL Remove Container]**。

![](../images/user-guide/exclusion.png)

根据需要排除事件，然 **[!UICONTROL Finish]** 后单击以创建实例。

![](../images/user-guide/advanced.png)

如果实例创建成功，将立即触发预测运行，并根据您定义的计划执行后续运行。

>[!NOTE] 根据输入数据的大小，预测运行可能需要24小时才能完成。

按照本节所述，您已配置了客户AI的实例，并执行了预测运行。 在运行成功完成后，得分洞察会自动用预测得分填充用户档案。 请等待24小时，然后继续阅读本教程的下一节。

## 后续步骤 {#next-steps}

通过遵循本教程，您成功地配置了客户AI的实例并生成了倾向得分。 您现在可以选择使用细分构建器创建具 [有预测得分的客户细分](./create-segment.md) ，或 [通过客户人工智能发掘洞察](./discover-insights.md)。

## Journey Orchestration

以下视频旨在支持您对客户AI配置工作流程的理解。 此外，还提供了最佳实践和用例示例。

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)

