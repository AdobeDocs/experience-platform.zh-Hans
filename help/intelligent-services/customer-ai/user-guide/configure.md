---
keywords: Experience Platform；用户指南；客户AI；热门主题；配置实例；创建实例；
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 配置Customer AI实例
topic-legacy: Instance creation
description: Intelligent Services将Customer AI作为一项简单易用的Adobe Sensei服务提供，该服务可针对不同用例进行配置。 以下部分提供了配置Customer AI实例的步骤。
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
source-git-commit: b6fff24d6298bad968e16516f2e555927c3a4a12
workflow-type: tm+mt
source-wordcount: '1549'
ht-degree: 0%

---

# 配置Customer AI实例

Customer AI作为Intelligent Services的一部分，使您能够生成自定义倾向得分，而无需担心机器学习问题。

Intelligent Services将Customer AI作为一项简单易用的Adobe Sensei服务提供，该服务可针对不同用例进行配置。 以下部分提供了配置Customer AI实例的步骤。

## 设置实例 {#set-up-your-instance}

在Platform UI的左侧导航中，选择&#x200B;**[!UICONTROL 服务]**。 出现&#x200B;**[!UICONTROL Services]**&#x200B;浏览器，它显示您可以使用的所有可用服务。 在Customer AI的容器中，选择&#x200B;**[!UICONTROL Open]**。

![](../images/user-guide/navigate-to-service.png)

将显示&#x200B;**Customer AI** UI并显示您的所有服务实例。

- 您可以在&#x200B;**[!UICONTROL 创建实例]**&#x200B;容器右下方找到&#x200B;**[!UICONTROL 打分的]**&#x200B;配置文件总数量度。 此量度跟踪Customer AI在当前日历年中得分的用户档案总数，包括所有沙盒环境和任何已删除的服务实例。

![](../images/user-guide/total-profiles.png)

可以使用UI右侧的控件来编辑、克隆和删除服务实例。 要显示这些控件，请从现有的&#x200B;**[!UICONTROL Service实例]**&#x200B;中选择一个实例。 这些控件包含以下内容：

- **[!UICONTROL 编辑]**:选择 **** 编辑允许您修改现有服务实例。您可以编辑实例的名称、描述和评分频率。
- **[!UICONTROL 克隆]**:选择 **** 克隆操作当前选定的服务实例设置。然后，您可以修改工作流以进行细微调整，并将其重命名为新实例。
- **[!UICONTROL 删除]**:您可以删除包含任何历史运行的服务实例。
- **[!UICONTROL 数据源]**:指向此实例使用的数据集的链接。
- **[!UICONTROL 上次运行详细信息]**:仅当运行失败时，才会显示该设置。此处显示有关运行失败原因的信息，如错误代码。
- **[!UICONTROL 得分定义]**:您为此实例配置的目标的快速概述。

![](../images/user-guide/service-instance-panel.png)

要创建新实例，请选择&#x200B;**[!UICONTROL 创建实例]**。

![](../images/user-guide/dashboard.png)

此时将显示实例创建工作流，从&#x200B;**[!UICONTROL 设置]**&#x200B;步骤开始。

以下是关于必须向实例提供的值的重要信息：

- 在显示Customer AI得分的所有位置中，都会使用实例的名称。 因此，名称应描述预测得分代表什么，例如“取消杂志订阅的可能性”。

- 倾向类型确定得分和量度极性的意图。 您可以选择&#x200B;**[!UICONTROL 流失率]**&#x200B;或&#x200B;**[!UICONTROL 转化]**。 有关倾向类型如何影响实例的更多信息，请参阅发现分析文档中[评分摘要](./discover-insights.md#scoring-summary)下的注释。

- 数据源是数据所在的位置。 数据集是用于预测得分的输入数据集。 Customer AI通过设计，使用消费者体验事件、Adobe Analytics和Adobe Audience Manager数据来计算倾向得分。 从下拉选择器中选择数据集时，只会列出与Customer AI兼容的数据集。

- 默认情况下，会为所有用户档案生成倾向得分，除非指定了符合条件的群体。 您可以通过定义条件以包含或排除基于事件的用户档案来指定符合条件的群体。

提供所需的值，然后选择&#x200B;**[!UICONTROL Next]**。

![](../images/user-guide/setup.png)

### 定义目标 {#define-a-goal}

此时会出现&#x200B;**[!UICONTROL 定义目标]**&#x200B;步骤，该步骤提供了一个交互环境，供您直观地定义预测目标。 目标由一个或多个事件组成，其中每个事件的发生取决于其保留的条件。 Customer AI实例的目标是确定在给定时间范围内实现其目标的可能性。

要创建目标，请选择&#x200B;**[!UICONTROL 输入字段名称]**，然后从下拉列表中选择一个字段。 选择第二个输入并为事件条件选择子句，然后提供目标值以完成事件。 可通过选择&#x200B;**[!UICONTROL Add event]**&#x200B;来配置其他事件。 最后，通过应用以天为单位的预测时间范围来完成目标，然后选择&#x200B;**[!UICONTROL Next]**。

![](../images/user-guide/goal.png)

#### 将发生且不发生

在定义目标时，您可以选择&#x200B;**[!UICONTROL 将发生]**&#x200B;或&#x200B;**[!UICONTROL 将不发生]**。 选择&#x200B;**[!UICONTROL 将发生]**&#x200B;表示需要满足您定义的事件条件，才能将客户的事件数据包含在分析UI中。

例如，如果要设置应用程序以预测客户是否会购买产品，则可以选择&#x200B;**[!UICONTROL Will occur]**，后跟&#x200B;**[!UICONTROL All of]**，然后输入&#x200B;**commerce.purchases.id**&#x200B;和&#x200B;**exists**&#x200B;作为运算符。

![将发生](../images/user-guide/occur.png)

但是，在某些情况下，您可能希望预测某个事件是否会在特定时间范围内发生。 要使用此选项配置目标，请从顶级下拉菜单中选择&#x200B;**[!UICONTROL 将不发生]**。

例如，如果您有兴趣预测哪些客户的参与度会降低，并且不会在下个月访问您的帐户登录页面。 选择&#x200B;**[!UICONTROL 将不出现]**，后跟&#x200B;**[!UICONTROL 所有]**，然后输入&#x200B;**web.webInteraction.URL**&#x200B;和&#x200B;**[!UICONTROL 等于]**&#x200B;作为运算符，并将&#x200B;**account-login**&#x200B;作为值。

![不会发生](../images/user-guide/not-occur.png)

#### 所有及任何

在某些情况下，您可能想要预测事件的组合是否会发生，而在其他情况下，您可能想要预测预定义集中的任何事件的发生。 要预测客户是否将具有事件组合，请从&#x200B;**[!UICONTROL 定义目标]**&#x200B;页面的二级下拉菜单中选择&#x200B;**[!UICONTROL 所有]**&#x200B;选项。

例如，您可能想要预测客户是否购买了特定产品。 此预测目标由两个条件定义：a `commerce.order.purchaseID` **存在**，且`productListItems.SKU` **等于某些特定值。**

![所有示例](../images/user-guide/all-of.png)

为了预测客户是否将拥有给定集中的任何事件，您可以使用&#x200B;**[!UICONTROL 任意]**&#x200B;选项。

例如，您可能想要预测客户是访问某个特定URL，还是访问具有特定名称的网页。 此预测目标由两个条件定义：`web.webPageDetails.URL` **以**&#x200B;开头，`web.webPageDetails.name` **以**&#x200B;特定值开头。

![任何示例](../images/user-guide/any-of.png)

### 自定义事件（*可选*）{#custom-events}

除了Customer AI用于生成倾向得分的[标准事件字段](../input-output.md#standard-events)之外，如果您还有其他信息，则会提供自定义事件选项。 如果您选择的数据集包含在架构中定义的自定义事件，则可以将它们添加到实例中。

![事件功能](../images/user-guide/event-feature.png)

要添加自定义事件，请选择&#x200B;**[!UICONTROL Add custom event]**。 接下来，输入自定义事件名称，然后将其映射到架构中的事件字段。 在查看影响因素和其他分析时，会显示自定义事件名称来代替字段值。 这表示用户ID、保留ID、设备信息和其他自定义值将以自定义事件名称列出，而不是以事件的ID/值列出。 Customer AI使用这些其他自定义事件来提高模型质量并提供更准确的结果。

![“自定义事件”字段](../images/user-guide/custom-event.png)

接下来，从可用的运算符下拉列表中选择您希望使用的运算符。 只列出与事件兼容的运算符。

![自定义事件运算符](../images/user-guide/custom-operator.png)

最后，如果所选运算符需要一个字段值，请输入该字段值。 在本例中，我们只需要查看酒店或餐厅是否存在预订。 但是，如果我们想要更精确，可以使用等于运算符，并在值提示符中输入精确值。

![自定义事件字段值](../images/user-guide/custom-value.png)

完成后，选择右上方的&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

### 配置计划&#x200B;*（可选）* {#configure-a-schedule}

出现&#x200B;**[!UICONTROL 高级]**&#x200B;步骤。 此可选步骤允许您配置计划以自动执行预测运行，定义预测排除以过滤某些事件，或者选择&#x200B;**[!UICONTROL 完成]**（如果不需要）。

通过配置&#x200B;**[!UICONTROL 评分频率]**&#x200B;来设置评分计划。 可以计划每周或每月运行自动预测运行。

![](../images/user-guide/schedule.png)

### 预测排除

如果您的数据集包含作为测试数据添加的任何列，则可以将该列或事件添加到排除列表中，方法是选择&#x200B;**添加排除项**，然后输入要排除的字段。 这样可防止在生成得分时评估满足特定条件的事件。 此功能可用于过滤掉不相关的数据输入或某些促销活动。

要排除事件，请选择&#x200B;**[!UICONTROL 添加排除项]**&#x200B;并定义事件。 要删除排除项，请选择省略号(**[!UICONTROL ...]**)，然后选择&#x200B;**[!UICONTROL 删除容器]**。

![](../images/user-guide/exclusion.png)

根据需要排除事件，然后选择&#x200B;**[!UICONTROL 完成]**&#x200B;以创建实例。

![](../images/user-guide/advanced.png)

如果成功创建实例，则会立即触发预测运行，并根据您定义的计划执行后续运行。

>[!NOTE]
>
>根据输入数据的大小，预测运行可能需要长达24小时才能完成。

通过执行本节，您配置了Customer AI的实例，并执行了预测运行。 在运行成功完成后，得分分析会自动用预测的得分填充用户档案。 请最多等待24小时，然后再继续阅读本教程的下一部分。

## 后续步骤 {#next-steps}

通过阅读本教程，您成功配置了Customer AI的实例并生成了倾向得分。 现在，您可以选择使用区段生成器来[创建具有预测得分](./create-segment.md)或[的客户区段，以通过Customer AI](./discover-insights.md)发现洞察。

## 其他资源

以下视频旨在支持您了解Customer AI的配置工作流。 此外，还提供了最佳实践和用例示例。

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)
