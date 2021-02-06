---
keywords: Experience Platform；用户指南；用户ai；热门主题；配置实例；创建实例；
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 配置客户AI实例
topic: Instance creation
description: 智能服务将客户人工智能作为简单易用的Adobe Sensei服务提供，该服务可针对不同的用例进行配置。 以下各节提供了配置客户人工智能实例的步骤。
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 0%

---


# 配置客户AI实例

作为智能服务的一部分，客户人工智能使您能够生成自定义倾向得分，而不必担心机器学习。

智能服务将客户人工智能作为简单易用的Adobe Sensei服务提供，该服务可针对不同的用例进行配置。 以下各节提供了配置客户人工智能实例的步骤。

## 设置实例{#set-up-your-instance}

在平台UI中，在左侧导航中选择&#x200B;**[!UICONTROL 服务]**。 将显示&#x200B;**[!UICONTROL 服务]**&#x200B;浏览器，并显示您可以使用的所有可用服务。 在客户AI的容器中，选择&#x200B;**[!UICONTROL 打开]**。

![](../images/user-guide/navigate-to-service.png)

出现&#x200B;**客户AI** UI并显示您的所有服务实例。

- 您可以在&#x200B;**[!UICONTROL 创建实例]**&#x200B;用户档案的右下侧找到得分&#x200B;]**的**[!UICONTROL &#x200B;容器总数。 此度量跟踪当前日历年度由客户AI评分的用户档案总数，包括所有沙箱环境和所有已删除的服务实例。

![](../images/user-guide/total-profiles.png)

使用UI右侧的控件可以编辑、克隆和删除服务实例。 要显示这些控件，请从现有&#x200B;**[!UICONTROL 服务实例]**&#x200B;中选择一个实例。 这些控件包含以下内容：

- **[!UICONTROL 编辑]**:选择 **** 编辑允许您修改现有服务实例。您可以编辑实例的名称、说明和评分频率。
- **[!UICONTROL 克隆]**:选择 **** 克隆操作当前选择的服务实例设置。然后，您可以修改工作流以进行细微调整，并将其重命名为新实例。
- **[!UICONTROL 删除]**:您可以删除包含任何历史运行的服务实例。
- **[!UICONTROL 数据源]**:此实例使用的数据集的链接。
- **[!UICONTROL 上次运行详细信息]**:仅当运行失败时，才显示此选项。此处显示有关运行失败原因的信息，如错误代码。
- **[!UICONTROL 得分定义]**:您为此实例配置的目标的快速概述。

![](../images/user-guide/service-instance-panel.png)

要创建新实例，请选择&#x200B;**[!UICONTROL 创建实例]**。

![](../images/user-guide/dashboard.png)

出现实例创建工作流，从&#x200B;**[!UICONTROL 设置]**&#x200B;步骤开始。

以下是关于必须向实例提供的值的重要信息：

- 在显示客户AI分数的所有位置都使用实例的名称。 因此，名称应描述预测分数所代表的内容，例如“取消杂志订阅的可能性”。

- 倾向类型确定得分和度量极性的目的。 您可以选择&#x200B;**[!UICONTROL Churn]**&#x200B;或&#x200B;**[!UICONTROL Conversion]**。 有关倾向类型如何影响您的实例的详细信息，请参阅发现洞察文档中[评分摘要](./discover-insights.md#scoring-summary)下的注释。

- 数据源是数据所在的位置。 数据集是用于预测得分的输入数据集。 根据设计，客户人工智能使用消费者体验事件数据来计算倾向得分。 从下拉选择器中选择数据集时，只列出与客户AI兼容的数据集。

- 默认情况下，将为所有用户档案生成倾向得分，除非指定符合条件的人口。 您可以通过定义条件来指定合格的人口，以根据用户档案包含或排除事件。

提供所需的值，然后选择&#x200B;**[!UICONTROL Next]**。

![](../images/user-guide/setup.png)

### 定义目标{#define-a-goal}

将出现&#x200B;**[!UICONTROL 定义目标]**&#x200B;步骤，它为您提供交互式环境，以可视化地定义预测目标。 目标由一个或多个事件组成，其中每个事件的发生基于其所持条件。 客户人工智能实例的目标是确定在给定时间范围内实现其目标的可能性。

要创建目标，请选择&#x200B;**[!UICONTROL 输入字段名称]**&#x200B;并从下拉列表中选择一个字段。 选择第二个输入，为事件的条件选择一个子句，然后提供目标值以完成事件。 可通过选择&#x200B;**[!UICONTROL 添加事件]**&#x200B;配置其他事件。 最后，通过应用以天数表示的预测时间帧来完成目标，然后选择&#x200B;**[!UICONTROL Next]**。

![](../images/user-guide/goal.png)

#### 将发生且不会发生

在定义目标时，您可以选择&#x200B;**[!UICONTROL 将发生]**&#x200B;或&#x200B;**[!UICONTROL 不发生]**。 选择&#x200B;**[!UICONTROL 将发生]**&#x200B;意味着您定义的事件条件需要满足，才能将客户事件数据包含在洞察UI中。

例如，如果要设置应用程序以预测客户是否进行购买，可以选择&#x200B;**[!UICONTROL Will occur]**，后跟&#x200B;**[!UICONTROL All of]**，然后输入&#x200B;**commerce.purchases.id**，并且&#x200B;**exists**&#x200B;作为运算符。

![将发生](../images/user-guide/occur.png)

但是，有时您可能希望预测某些事件是否在特定时间段内不会发生。 要使用此选项配置目标，请从顶级下拉菜单中选择&#x200B;**[!UICONTROL 不会发生]**。

例如，如果您希望预测哪些客户参与度降低，请不要在下个月访问您的帐户登录页面。 选择&#x200B;**[!UICONTROL 不发生]**，后跟&#x200B;**[!UICONTROL 所有]**，然后输入&#x200B;**web.webInteraction.URL**&#x200B;和&#x200B;**[!UICONTROL 等于]**&#x200B;作为以&#x200B;**account-login**&#x200B;作为值的运算符。

![不会发生](../images/user-guide/not-occur.png)

#### 所有和任何

在某些情况下，您可能想要预测事件组合是否会发生，而在其他情况下，您可能想要预测来自预定义集的任何事件的发生。 为了预测客户是否将具有事件组合，请从&#x200B;**[!UICONTROL 定义目标]**&#x200B;页的第二级下拉列表中选择&#x200B;**[!UICONTROL 所有]**&#x200B;选项。

例如，您可能想要预测客户是否购买特定产品。 该预测目标由两个条件定义：a `commerce.order.purchaseID` **存在**&#x200B;且`productListItems.SKU` **等于**&#x200B;某个特定值。

![所有示例](../images/user-guide/all-of.png)

为了预测客户是否具有给定集的任何事件，您可以使用&#x200B;**[!UICONTROL 任何]**&#x200B;选项。

例如，您可能想要预测客户是访问某个URL还是访问具有特定名称的网页。 该预测目标由两个条件定义：`web.webPageDetails.URL`**具有特定值的开始和具有特定值的`web.webPageDetails.name`**&#x200B;开始。****

![任何示例](../images/user-guide/any-of.png)

### 配置计划&#x200B;*（可选）* {#configure-a-schedule}

出现&#x200B;**[!UICONTROL 高级]**&#x200B;步骤。 此可选步骤允许您配置计划以自动执行预测运行，定义预测排除以过滤某些事件，或选择&#x200B;**[!UICONTROL 完成]**（如果不需要）。

通过配置&#x200B;**[!UICONTROL 评分频率]**&#x200B;设置评分计划。 可以计划每周或每月运行自动预测运行。

![](../images/user-guide/schedule.png)

在计划配置下，您可以定义预测排除，以防止在生成得分时评估满足特定条件的事件。 此功能可用于过滤掉不相关的数据输入。

要排除某些事件，请选择&#x200B;**[!UICONTROL 添加排除]**，并以与定义目标相同的方式定义事件。 要删除排除，请选择省略号(**[!UICONTROL ...]**)，然后选择&#x200B;**[!UICONTROL 删除事件]**。

![](../images/user-guide/exclusion.png)

根据需要排除事件，然后选择&#x200B;**[!UICONTROL 完成]**&#x200B;以创建实例。

![](../images/user-guide/advanced.png)

如果实例创建成功，将立即触发预测运行，并根据您定义的计划执行后续运行。

>[!NOTE]
>
>根据输入数据的大小，预测运行可能需要24小时才能完成。

按照本节所述，您已配置了客户AI的实例，并执行了预测运行。 在运行成功完成后，得分洞察会自动用预测得分填充用户档案。 请等待24小时，然后继续阅读本教程的下一节。

## 后续步骤 {#next-steps}

通过遵循本教程，您成功地配置了客户AI的实例并生成了倾向得分。 您现在可以选择使用细分构建器[使用预测分数](./create-segment.md)或[通过客户AI](./discover-insights.md)发掘洞察来创建客户细分。

## Journey Orchestration

以下视频旨在支持您对客户AI配置工作流程的理解。 此外，还提供了最佳实践和用例示例。

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)

