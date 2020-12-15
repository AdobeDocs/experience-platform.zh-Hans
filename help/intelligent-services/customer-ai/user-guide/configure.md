---
keywords: Experience Platform;user guide;customer ai;popular topics;configure instance;create instance;
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 配置客户AI实例
topic: Instance creation
description: 智能服务将客户人工智能作为简单易用的Adobe Sensei服务提供，该服务可针对不同的用例进行配置。 以下各节提供了配置客户人工智能实例的步骤。
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 0%

---


# 配置客户AI实例

作为智能服务的一部分，客户人工智能使您能够生成自定义倾向得分，而不必担心机器学习。

智能服务将客户人工智能作为简单易用的Adobe Sensei服务提供，该服务可针对不同的用例进行配置。 以下各节提供了配置客户人工智能实例的步骤。

## 设置实例 {#set-up-your-instance}

在平台UI中，选择左 **[!UICONTROL 侧导]** 航中的“服务”。 将显 **[!UICONTROL 示服务]** 浏览器，并显示您可使用的所有可用服务。 在客户AI的容器中，选择 **[!UICONTROL 打开]**。

![](../images/user-guide/navigate-to-service.png)

将显 **示客户** AI UI，并显示您的所有服务实例。

- 您可以在创 **[!UICONTROL 建实例]** 容器的右下侧找到Total **[!UICONTROL 用户档案计分量度]** 。 此度量跟踪当前日历年度由客户AI评分的用户档案总数，包括所有沙箱环境和所有已删除的服务实例。

![](../images/user-guide/total-profiles.png)

使用UI右侧的控件可以编辑、克隆和删除服务实例。 要显示这些控件，请从现有服务实例中选 **[!UICONTROL 择一个实例]**。 这些控件包含以下内容：

- **[!UICONTROL 编辑]**:选择 **[!UICONTROL “编辑]** ”允许您修改现有服务实例。 您可以编辑实例的名称、说明和评分频率。
- **[!UICONTROL 克隆]**:选择 **[!UICONTROL 克隆]** ，将复制当前选定的服务实例设置。 然后，您可以修改工作流以进行细微调整，并将其重命名为新实例。
- **[!UICONTROL 删除]**:您可以删除包含任何历史运行的服务实例。
- **[!UICONTROL 数据源]**:此实例使用的数据集的链接。
- **[!UICONTROL 上次运行详细信息]**:仅当运行失败时，才显示此选项。 此处显示有关运行失败原因的信息，如错误代码。
- **[!UICONTROL 得分定义]**:您为此实例配置的目标的快速概述。

![](../images/user-guide/service-instance-panel.png)

要创建新实例，请选择“创 **[!UICONTROL 建实例”]**。

![](../images/user-guide/dashboard.png)

将出现实例创建工作流，从“设置” **[!UICONTROL 步骤]** 开始。

以下是关于必须向实例提供的值的重要信息：

- 在显示客户AI分数的所有位置都使用实例的名称。 因此，名称应描述预测分数所代表的内容，例如“取消杂志订阅的可能性”。

- 倾向类型确定得分和度量极性的目的。 您可以选择“ **[!UICONTROL 客户流]** 失” **[!UICONTROL 或“转化]**”。 有关倾向类型如何影 [响实例](./discover-insights.md#scoring-summary) ，请参阅发现洞察文档中评分摘要下的注释。

- 数据源是数据所在的位置。 数据集是用于预测得分的输入数据集。 根据设计，客户人工智能使用消费者体验事件数据来计算倾向得分。 从下拉选择器中选择数据集时，只列出与客户AI兼容的数据集。

- 默认情况下，将为所有用户档案生成倾向得分，除非指定符合条件的人口。 您可以通过定义条件来指定合格的人口，以根据用户档案包含或排除事件。

提供所需的值，然后选择“下 **[!UICONTROL 一步]**”。

![](../images/user-guide/setup.png)

### 定义目标 {#define-a-goal}

此时 **[!UICONTROL 将显示]** “定义目标”步骤，它提供一个交互式环境，供您以可视方式定义预测目标。 目标由一个或多个事件组成，其中每个事件的发生基于其所持条件。 客户人工智能实例的目标是确定在给定时间范围内实现其目标的可能性。

要创建目标，请选 **[!UICONTROL 择“输入字段名]** ”，然后从下拉列表中选择一个字段。 选择第二个输入，为事件的条件选择一个子句，然后提供目标值以完成事件。 可以通过选择添加事件来配 **[!UICONTROL 置其他事件]**。 最后，通过应用天数预测时间帧来完成目标，然后选择“下 **[!UICONTROL 一步”]**。

![](../images/user-guide/goal.png)

#### 将发生且不会发生

定义目标时，您可以选择“将 **[!UICONTROL 发生]** ” **[!UICONTROL 或“不发生”]**。 选 **[!UICONTROL 择将发]** 生意味着您定义的事件条件需要满足，才能将客户事件数据包含在洞察UI中。

例如，如果您要设置应用程序以预测客户是否进行购买，则可以选 **[!UICONTROL 择]** Will **[!UICONTROL occur]** , **后跟All of** ，然后输入 **commerce.purchases.id** ，并作为运营商。

![将发生](../images/user-guide/occur.png)

但是，有时您可能希望预测某些事件是否在特定时间段内不会发生。 要使用此选项配置目标，请 **[!UICONTROL 从顶级下拉]** 菜单中选择“不会发生”。

例如，如果您希望预测哪些客户参与度降低，请不要在下个月访问您的帐户登录页面。 选 **[!UICONTROL 择Will]** not Will by **[!UICONTROL All]** ，然后输 **入web.webInteraction.URL，并将等于** 作为 ******** 的的值，该值为帐户登录名。

![不会发生](../images/user-guide/not-occur.png)

#### 所有和任何

在某些情况下，您可能想要预测事件组合是否会发生，而在其他情况下，您可能想要预测来自预定义集的任何事件的发生。 要预测客户是否将具有事件组合，请从“定义 **[!UICONTROL 目标]** ”页的“二级”下拉菜单中选择“全部 **[!UICONTROL ”选项]** 。

例如，您可能想要预测客户是否购买特定产品。 该预测目标由两个条件定义：a `commerce.order.purchaseID` 存 **在** ，且 `productListItems.SKU` 等 **于某** 些特定值。

![所有示例](../images/user-guide/all-of.png)

为了预测客户是否将拥有来自给定集合的任何事件，您可以使用“任 **[!UICONTROL 意”选项]** 。

例如，您可能想要预测客户是访问某个URL还是访问具有特定名称的网页。 该预测目标由两个条件定义： `web.webPageDetails.URL` **具有特定** 值的开始和 `web.webPageDetails.name` 具 **有特定值** 的开始。

![任何示例](../images/user-guide/any-of.png)

### 配置计划 *（可选）* {#configure-a-schedule}

将出 **[!UICONTROL 现]** “高级”步骤。 此可选步骤允许您配置计划以自动执行预测运行，定义预测排除以过滤某些事件，或 **[!UICONTROL 选择]** “完成”（如果不需要）。

通过配置评分频率设置 **[!UICONTROL 评分计划]**。 可以计划每周或每月运行自动预测运行。

![](../images/user-guide/schedule.png)

在计划配置下，您可以定义预测排除，以防止在生成得分时评估满足特定条件的事件。 此功能可用于过滤掉不相关的数据输入。

要排除某些事件 **** ，请选择“添加排除”，并以与定义目标相同的方式定义事件。 要删除排除，请选择事件&#x200B;**[!UICONTROL 容器右上方的省略号(]**...)，然后选择 **[!UICONTROL 删除容器]**。

![](../images/user-guide/exclusion.png)

根据需要排除事件，然 **[!UICONTROL 后选]** 择完成以创建实例。

![](../images/user-guide/advanced.png)

如果实例创建成功，将立即触发预测运行，并根据您定义的计划执行后续运行。

>[!NOTE]
>
>根据输入数据的大小，预测运行可能需要24小时才能完成。

按照本节所述，您已配置了客户AI的实例，并执行了预测运行。 在运行成功完成后，得分洞察会自动用预测得分填充用户档案。 请等待24小时，然后继续阅读本教程的下一节。

## 后续步骤 {#next-steps}

通过遵循本教程，您成功地配置了客户AI的实例并生成了倾向得分。 您现在可以选择使用细分构建器创建具 [有预测得分的客户细分](./create-segment.md) ，或 [通过客户人工智能发掘洞察](./discover-insights.md)。

## Journey Orchestration

以下视频旨在支持您对客户AI配置工作流程的理解。 此外，还提供了最佳实践和用例示例。

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)

