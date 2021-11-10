---
keywords: Experience Platform；用户指南；客户AI；热门主题；配置实例；创建实例；
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: 配置Customer AI实例
topic-legacy: Instance creation
description: Intelligent Services将Customer AI作为一项简单易用的Adobe Sensei服务提供，该服务可针对不同用例进行配置。 以下部分提供了配置Customer AI实例的步骤。
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
source-git-commit: 52ab1527d3021500d934afe56cfc751116f784a4
workflow-type: tm+mt
source-wordcount: '2299'
ht-degree: 0%

---

# 配置Customer AI实例

Customer AI作为Intelligent Services的一部分，使您能够生成自定义倾向得分，而无需担心机器学习问题。

Intelligent Services将Customer AI作为一项简单易用的Adobe Sensei服务提供，该服务可针对不同用例进行配置。 以下部分提供了配置Customer AI实例的步骤。

## 设置实例 {#set-up-your-instance}

在平台UI中，选择 **[!UICONTROL 服务]** 中。 的 **[!UICONTROL 服务]** 浏览器会显示并显示您可使用的所有可用服务。 在Customer AI的容器中，选择 **[!UICONTROL 打开]**.

![](../images/user-guide/navigate-to-service.png)

的 **客户人工智能** 此时会显示UI，并显示您的所有服务实例。

- 您可以在 **[!UICONTROL 得分的用户档案总数]** 位于 **[!UICONTROL 创建实例]** 容器。 此量度跟踪Customer AI在当前日历年内对包括所有沙盒环境和任何已删除服务实例在内的用户档案进行评分的总数。

![](../images/user-guide/total-profiles.png)

可以使用UI右侧的控件来编辑、克隆和删除服务实例。 要显示这些控件，请从现有的 **[!UICONTROL 服务实例]**. 这些控件包含以下内容：

- **[!UICONTROL 编辑]**:选择 **[!UICONTROL 编辑]** 用于修改现有服务实例。 您可以编辑实例的名称、描述和评分频率。
- **[!UICONTROL 克隆]**:选择 **[!UICONTROL 克隆]** 复制当前选定的服务实例设置。 然后，您可以修改工作流以进行细微调整，并将其重命名为新实例。
- **[!UICONTROL 删除]**:您可以删除包含任何历史运行的服务实例。
- **[!UICONTROL 数据源]**:指向此实例使用的数据集的链接。 如果使用多个数据集，则选择超链接文本会打开数据集预览弹出窗口。
- **[!UICONTROL 上次运行详细信息]**:仅当运行失败时，才会显示该设置。 此处显示有关运行失败原因的信息，如错误代码。
- **[!UICONTROL 得分定义]**:您为此实例配置的目标的快速概述。

![](../images/user-guide/service-instance-panel.png)

要创建新实例，请选择 **[!UICONTROL 创建实例]**.

![](../images/user-guide/dashboard.png)

## 设置

此时将显示实例创建工作流，从 **[!UICONTROL 设置]** 中。

以下是关于必须向实例提供的值的重要信息：

- **[!UICONTROL 名称]:** 在显示Customer AI得分的所有位置中，都会使用实例的名称。 因此，名称应描述预测分数表示的内容。 例如，“取消杂志订阅的可能性”。

- **[!UICONTROL 描述]:** 说明您尝试预测的内容的描述。

- **[!UICONTROL 倾向类型]:** 倾向类型确定得分和量度极性的意图。 您可以选择 **[!UICONTROL 流失率]** 或 **[!UICONTROL 转化]**. 请参阅 [评分摘要](./discover-insights.md#scoring-summary) （位于“发现分析”文档中），以了解有关倾向类型如何影响实例的更多信息。

![设置屏幕](../images/user-guide/create-instance.png)

提供所需的值，然后选择 **[!UICONTROL 下一个]** 继续。

## 选择数据 {#select-data}

通过设计， Customer AI使用Adobe Analytics、Adobe Audience Manager、体验事件和消费者体验事件数据来计算倾向得分。 选择数据集时，只会列出与Customer AI兼容的数据集。 要选择数据集，请选择&#x200B;**+**)符号或选中复选框以一次添加多个数据集。 使用搜索选项可快速查找您感兴趣的数据集。

![选择和搜索数据集](../images/user-guide/configure-dataset-page.png)

选择要使用的数据集后，选择 **[!UICONTROL 添加]** 按钮将数据集添加到数据集预览窗格。

![选择数据集](../images/user-guide/select-datasets.png)

选择信息图标 ![信息图标](../images/user-guide/info-icon.png) 数据集旁边会打开数据集预览弹出窗口。

![选择和搜索数据集](../images/user-guide/dataset-info-2.png)

数据集预览包含数据，如上次更新时间、源架构以及前十列的预览。

### 数据集完整性 {#dataset-completeness}

数据集预览中有一个数据集完整性百分比值。 此值提供数据集中有多少列为空/空的快照。 如果一个数据集包含大量缺失值，并且这些值在其他位置被捕获，则强烈建议您包含包含缺失值的数据集。 在此示例中，人员ID为空，但是，人员ID是在可包含的单独数据集中捕获的。

>[!NOTE]
>
>使用Customer AI的最大培训窗口（一年）计算数据集完整性。 这意味着在显示数据集完整性值时，不会考虑一年以上的数据。
<!-- training dataset completness needs to change -->
![数据集完整性](../images/user-guide/dataset-info.png)

### 选择标识 {#identity}

为了使多个数据集彼此连接，您必须选择身份类型（也称为“身份命名空间”）和该命名空间中的身份值。 如果您在同一命名空间下为架构内的多个字段分配了身份，则所有分配的身份值都会显示在由命名空间前面的身份下拉菜单中，例如 `EMAIL (personalEmail.address)` 或 `EMAIL (workEmail.address)`.

>[!IMPORTANT]
>
>必须为您选择的每个数据集使用相同的身份类型（命名空间）。 标识列中的标识类型旁边会显示一个绿色复选标记，指示数据集兼容。 例如，使用电话命名空间和 `mobilePhone.number` 作为标识符，其余数据集的所有标识符必须包含并使用Phone命名空间。

要选择身份，请选择位于身份列中的带下划线的值。 此时会出现选择标识弹出窗口。

![选择相同的命名空间](../images/user-guide/identity-type.png)

如果命名空间中有多个标识可用，请确保为用例选择正确的标识字段。 例如，电子邮件命名空间中提供了两个电子邮件标识，即工作电子邮件和个人电子邮件。 根据用例的不同，个人电子邮件更有可能被填写，并且在单个预测中更有用。 这意味着 `EMAIL (personalEmail.address)` 将被选作身份。

![未选择数据集键值](../images/user-guide/select-identity.png)

>[!NOTE]
>
> 如果数据集不存在有效的标识类型（命名空间），则必须设置主标识，并使用 [架构编辑器](../../../xdm/schema/composition.md#identity). 要了解有关命名空间和身份的更多信息，请访问 [身份服务命名空间](../../../identity-service/namespaces.md) 文档。

## 定义目标 {#define-a-goal}

<!-- https://www.adobe.com/go/cai-define-a-goal -->

的 **[!UICONTROL 定义目标]** 步骤，它为您提供了一个交互式环境，以便您直观地定义预测目标。 目标由一个或多个事件组成，其中每个事件的发生取决于其保留的条件。 Customer AI实例的目标是确定在给定时间范围内实现其目标的可能性。

要创建目标，请选择 **[!UICONTROL 输入字段名称]** ，然后下拉列表中的字段。 选择第二个输入，即事件条件的子句，然后选择提供目标值以完成事件。 通过选择 **[!UICONTROL 添加事件]**. 最后，通过应用以天为单位的预测时间范围来完成目标，然后选择 **[!UICONTROL 下一个]**.

![](../images/user-guide/define-a-goal.png)

### 将发生且不发生

在定义目标时，您可以选择 **[!UICONTROL 将发生]** 或 **[!UICONTROL 不会发生]**. 选择 **[!UICONTROL 将发生]** 意味着需要满足您定义的事件条件，才能将客户的事件数据包含在分析UI中。

例如，如果您想设置应用程序来预测客户是否会购买产品，则可以选择 **[!UICONTROL 将发生]** 后跟 **[!UICONTROL 全部]** 然后输入 **commerce.purchases.id** （或类似字段）和 **[!UICONTROL 存在]** 作为运算符。

![将发生](../images/user-guide/occur.png)

但是，在某些情况下，您可能希望预测某个事件是否会在特定时间范围内发生。 要使用此选项配置目标，请选择 **[!UICONTROL 不会发生]** 从顶级下拉菜单中。

例如，如果您有兴趣预测哪些客户的参与度会降低，并且不会在下个月访问您的帐户登录页面。 选择 **[!UICONTROL 不会发生]** 后跟 **[!UICONTROL 全部]** 然后输入 **web.webInteraction.URL** （或类似字段）和 **[!UICONTROL 等于]** 作为 **account-login** 作为值。

![不会发生](../images/user-guide/not-occur.png)

### 所有及任何

在某些情况下，您可能想要预测事件的组合是否会发生，而在其他情况下，您可能想要预测预定义集中的任何事件的发生。 要预测客户是否将具有事件组合，请选择 **[!UICONTROL 全部]** 选项 **[!UICONTROL 定义目标]** 页面。

例如，您可能想要预测客户是否购买了特定产品。 此预测目标由两个条件定义：a `commerce.order.purchaseID` **存在** 和 `productListItems.SKU` **等于** 一些特定值。

![所有示例](../images/user-guide/all-of.png)

为了预测客户是否将拥有给定集中的任何事件，您可以使用 **[!UICONTROL 任意]** 选项。

例如，您可能想要预测客户是访问某个特定URL，还是访问具有特定名称的网页。 此预测目标由两个条件定义： `web.webPageDetails.URL` **开头** 特定值和 `web.webPageDetails.name` **开头** 特定值。

![任何示例](../images/user-guide/any-of.png)

### 合格人口 *（可选）*

默认情况下，会为所有用户档案生成倾向得分，除非指定了符合条件的群体。 您可以通过定义条件以根据事件包含或排除用户档案来指定符合条件的群体。

![合格人口](../images/user-guide/eligible-population.png)

### 自定义事件(*可选*) {#custom-events}

除 [标准事件字段](../input-output.md#standard-events) Customer AI用于生成倾向得分，提供了自定义事件选项。 使用此选项可添加您认为具有影响力的其他事件，这可能会提高模型的质量并有助于提供更准确的结果。 如果您选择的数据集包含在架构中定义的自定义事件，则可以将它们添加到实例中。

![事件功能](../images/user-guide/event-feature.png)

要添加自定义事件，请选择 **[!UICONTROL 添加自定义事件]**. 接下来，输入自定义事件名称，然后将其映射到架构中的事件字段。 在查看影响因素和其他分析时，会显示自定义事件名称来代替字段值。 这表示用户ID、保留ID、设备信息和其他自定义值将以自定义事件名称列出，而不是以事件的ID/值列出。 Customer AI使用这些其他自定义事件来提高模型质量并提供更准确的结果。

![“自定义事件”字段](../images/user-guide/custom-event.png)

接下来，从可用的运算符下拉列表中选择您希望使用的运算符。 只列出与事件兼容的运算符。

![自定义事件运算符](../images/user-guide/custom-operator.png)

最后，如果所选运算符需要一个字段值，请输入该字段值。 在本例中，我们只需要查看酒店或餐厅是否存在预订。 但是，如果我们想要更精确，可以使用等于运算符，并在值提示符中输入精确值。

![自定义事件字段值](../images/user-guide/custom-value.png)

完成后，选择 **[!UICONTROL 下一个]** 来继续。

### 自定义配置文件属性(*可选*)

除了 [标准事件字段](../input-output.md#standard-events) Customer AI用于生成倾向得分。 通过使用此选项，您可以添加其他您认为具有影响力的配置文件属性，这些属性可能会提高模型质量并提供更准确的结果。 此外，通过添加自定义用户档案属性，Customer AI可以更好地展示特定用户档案是如何在倾向存储段中结束的。

>[!NOTE]
>
>添加自定义配置文件属性的工作流程与添加自定义事件的工作流程相同。

![添加自定义配置文件属性](../images/user-guide/profile-attributes.png)

### 配置计划 *（可选）* {#configure-a-schedule}

的 **[!UICONTROL 高级]** 中。 此可选步骤允许您配置计划以自动执行预测运行、定义预测排除以过滤某些事件或选择 **[!UICONTROL 完成]** 无需执行任何操作。

通过配置 **[!UICONTROL 评分频度]**. 可以计划每周或每月运行自动预测运行。

![](../images/user-guide/schedule.png)

### 预测排除

如果您的数据集包含作为测试数据添加的任何列，则可以通过选择 **添加排除项** 然后输入要排除的字段。 这样可防止在生成得分时评估满足特定条件的事件。 此功能可用于过滤掉不相关的数据输入或某些促销活动。

要排除事件，请选择 **[!UICONTROL 添加排除项]** 并定义事件。 要删除排除项，请选择省略号(**[!UICONTROL ...]**)，然后选择 **[!UICONTROL 删除容器]**.

![](../images/user-guide/exclusion.png)

### 配置文件切换

“用户档案”切换开关允许Customer AI将评分结果导出到“实时客户资料”。 禁用此切换开关会阻止将模型评分结果添加到用户档案。 禁用此功能后，仍可使用客户AI评分结果。

首次使用Customer AI时，应关闭此功能，直到您对模型输出结果感到满意。 这样可防止在微调模型时将多个评分数据集上传到实时客户资料。

![配置文件切换](../images/user-guide/advanced-workflow.png)

设置评分计划、包含预测排除项以及在您希望的位置切换用户档案后，选择 **[!UICONTROL 完成]** ，以创建Customer AI实例。

如果成功创建实例，则会立即触发预测运行，并根据您定义的计划执行后续运行。

>[!NOTE]
>
>根据输入数据的大小，预测运行可能需要长达24小时才能完成。

通过执行本节，您配置了Customer AI的实例并执行了预测运行。 成功完成运行后，如果启用了用户档案切换，则得分分析会自动使用预测的得分填充用户档案。 请最多等待24小时，然后再继续阅读本教程的下一部分。

## 后续步骤 {#next-steps}

通过阅读本教程，您成功配置了Customer AI的实例并生成了倾向得分。 现在，您可以选择使用区段生成器来 [创建预测分数的客户区段](./create-segment.md) 或 [通过Customer AI发现洞察](./discover-insights.md).

## 其他资源

以下视频旨在支持您了解Customer AI的配置工作流。 此外，还提供了最佳实践和用例示例。

>[!IMPORTANT]
>
> 以下视频已过期。 有关最新信息，请参阅此文档。

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)
