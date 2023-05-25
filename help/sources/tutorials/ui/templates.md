---
description: 了解如何在Adobe Experience Platform UI中使用模板来加速B2B数据的数据摄取过程。
title: 使用UI中的模板创建源数据流
badge1: "Beta"
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: 91d6832231d75c9dd23e91a5f1152eac61558fc5
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 9%

---

# 使用UI中的模板创建源数据流

>[!IMPORTANT]
>
>模板为测试版，受以下源支持：
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>文档和功能可能会发生更改。

Adobe Experience Platform提供了预配置的模板，您可以使用这些模板加快数据摄取过程。 模板包括自动生成的资源，例如架构、数据集、身份、映射规则、身份命名空间和数据流，在将数据从源引入到Experience Platform时可使用这些资源。

使用模板，您可以：

* 通过加快模板化资产的创建，缩短引入的价值实现时间。
* 最大程度地减少手动数据摄取过程中可能发生的错误。
* 随时更新自动生成的资源以符合您的用例。

以下教程提供了有关如何在Platform UI中使用模板的步骤。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [源](../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
* [沙盒](../../../sandboxes/home.md)：Experience Platform提供可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

## 在Platform UI中使用模板 {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="选择业务类型"
>abstract="为您的用例选择适当的业务类型。您的访问权限可能因 Real-Time Customer Data Platform 订阅帐户而异。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=zh-Hans" text="Real-Time CDP 概述"

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 并查看Experience Platform中可用的源目录。

使用 *[!UICONTROL 类别]* 菜单，用于按类别筛选源。 或者，在搜索栏中输入源名称，以从目录查找特定源。

转到 [!UICONTROL Adobe应用程序] 类别以查看 [!DNL Marketo Engage] 源卡，然后选择 [!UICONTROL 添加数据] 开始。

![突出显示Marketo Engage源的源工作区的目录。](../../images/tutorials/templates/catalog.png)

此时会显示一个弹出窗口，为您提供浏览模板或使用现有架构和数据集的选项。

* **浏览模板**：源模板可为您自动创建包含映射规则的架构、身份、数据集和数据流。 您可以根据需要自定义这些资源。
* **使用我的现有资源**：使用您创建的现有数据集和架构摄取数据。 如果需要，您还可以创建新数据集和架构。

要使用自动生成的资源，请选择 **[!UICONTROL 浏览模板]** 然后选择 **[!UICONTROL 选择]**.

![一个弹出窗口，其中包含浏览模板或使用现有资源的选项。](../../images/tutorials/templates/browse-templates.png)

### 身份验证

此时将显示身份验证步骤，提示您创建新帐户或使用现有帐户。

>[!BEGINTABS]

>[!TAB 使用现有帐户]

要使用现有帐户，请选择 [!UICONTROL 现有帐户] 然后从显示的列表中选择要使用的帐户。

![现有帐户的选择页面，其中包含您可以访问的现有帐户列表。](../../images/tutorials/templates/existing-account.png)

>[!TAB 创建新帐户]

要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后提供源连接详细信息和帐户身份验证凭据。 完成后，选择 **[!UICONTROL 连接到源]** 并留出一些时间来建立新连接。

![具有源连接详细信息和帐户身份验证凭据的新帐户的身份验证页面。](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### 选择模板

根据您选择的业务类型，将显示模板列表。 选择预览图标 ![预览图标](../../images/tutorials/templates/preview-icon.png) 位于模板名称旁边，用于预览模板中的示例数据。

![突出显示预览图标的模板列表。](../../images/tutorials/templates/templates.png)

此时将显示预览窗口，允许您浏览和检查模板中的示例数据。 完成后，选择 **[!UICONTROL 知道了]**.

![预览示例数据窗口。](../../images/tutorials/templates/preview-sample-data.png)

接下来，从列表中选择要使用的模板。 您可以选择多个模板并一次创建多个数据流。 但是，每个帐户只能使用一次模板。 选择模板后，选择 **[!UICONTROL 完成]** 并留出一些时间以便生成资源。

如果从可用模板列表中选择一个或多个项目，则仍会生成所有B2B架构和身份命名空间，以确保正确配置架构之间的B2B关系。

>[!NOTE]
>
>已使用的模板将从选择中禁用。

![已选择机会联系人角色模板的模板列表。](../../images/tutorials/templates/select-template.png)

### 设置计划

此 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce] 两个源都支持计划数据流。

使用计划界面为数据流配置摄取计划。 将摄取频率设置为 **一次** 创建一次性摄取。

![Dynamics和Salesforce模板的计划界面。](../../images/tutorials/templates/schedule.png)

或者，您也可以将摄取频率设置为 **分钟**， **小时**， **日**，或 **周**. 如果计划数据流以进行多次摄取，则必须设置间隔以在每次摄取之间建立一个时间范围。 例如，摄取频率设置为 **小时** 并且间隔设置为 **15** 意味着您的数据流计划每隔 **15小时**.

在此步骤中，您还可以启用 **回填** 和定义用于增量摄取数据的列。 回填用于摄取历史数据，而您为增量摄取定义的列允许将新数据与现有数据区分开。

配置完摄取计划后，选择 **[!UICONTROL 完成]**.

![已启用回填的Dynamics和Salesforce模板的计划界面。](../../images/tutorials/templates/backfill.png)

### 查看资产 {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="查看自动生成的资产"
>abstract="生成所有资产最多需要五分钟时间。如果您选择离开页面，在生成完资产后，将向您发送通知以返回页面。您可以在资产生成后查看资产，并随时对数据流进行其他配置。"

此 [!UICONTROL 审核模板资产] 页面显示作为模板的一部分自动生成的资产。 在此页中，可以查看与源连接关联的自动生成的架构、数据集、身份命名空间和数据流。 生成所有资产最多需要五分钟时间。如果您选择离开页面，在生成完资产后，将向您发送通知以返回页面。您可以在资产生成后查看资产，并随时对数据流进行其他配置。

默认情况下，自动生成的数据流设置为草稿状态，以允许对配置进行进一步自定义，如映射规则或计划频率。 选择省略号(`...`)，然后选择 **[!UICONTROL 预览映射]** 查看为草稿数据流创建的映射集。

![已选择预览映射选项的下拉窗口。](../../images/tutorials/templates/preview.png)

此时将显示一个预览页面，允许您检查源数据字段与目标架构字段之间的映射关系。 查看数据流的映射后。 选择 **[!UICONTROL 知道了。]**

![映射预览窗口。](../../images/tutorials/templates/preview-mappings.png)

可在执行后随时更新数据流。 选择省略号(`...`)，然后选择 **[!UICONTROL 更新数据流]**. 您将转到源工作流页面，可以在其中更新数据流详细信息，包括部分摄取、错误诊断和警报通知的设置以及数据流的映射。

您可以使用架构编辑器视图对自动生成的架构进行更新。 请访问指南，网址为 [使用架构编辑器](../../../xdm/tutorials/create-schema-ui.md) 了解更多信息。

![已选择更新数据流选项的下拉窗口。](../../images/tutorials/templates/update.png)

>[!TIP]
>
>您可以通过以下方式访问草稿数据流 [!UICONTROL 数据流] “源”工作区中的“目录”页面。 选择 **[!UICONTROL 数据流]** 从顶部标题中，然后从列表中选择要更新的数据流。
>
>![源工作区的数据流目录中的现有数据流列表。](../../images/tutorials/templates/dataflows.png)

### 发布数据流

通过浏览源工作流开始发布过程。 选择后 [!UICONTROL 更新数据流]，您会被带到 *[!UICONTROL 添加数据]* 工作流的步骤。 选择 **[!UICONTROL 下一个]** 以继续。

![为草稿数据流添加数据步骤](../../images/tutorials/templates/continue-draft.png)

接下来，确认数据流详细信息并配置错误诊断、部分摄取和警报通知的设置。 完成后，选择 **[!UICONTROL 下一个]**.

![草稿数据流的数据流详细信息步骤。](../../images/tutorials/templates/dataflow-detail.png)

>[!NOTE]
>
>您可以选择 **[!UICONTROL 另存为草稿]** 随时停止并保存您对数据流的更改。

此时将显示映射步骤。 在此步骤中，您可以重新配置数据流的映射配置。 有关用于映射的数据准备功能的全面指南，请访问 [数据准备UI指南](../../../data-prep/ui/mapping.md).

![草稿数据流的映射步骤。](../../images/tutorials/templates/mapping.png)

最后，查看数据流的详细信息，然后选择 **[!UICONTROL 保存并摄取]** 以发布草稿。

![草稿数据流的审核步骤。](../../images/tutorials/templates/review.png)

## 后续步骤

通过学习本教程，您现在已使用模板创建了数据流以及架构、数据集和身份命名空间等资产。 欲了解信息源的一般信息，请访问 [源概述](../../home.md).

## 警报和通知 {#alerts-and-notifications}

Adobe Experience Platform警报支持模板，您可以使用通知面板接收资产状态的更新，并导航回审核页面。

选择Platform UI顶部标题的通知图标，然后选择状态警报以查看要审阅的资产。

![Platform UI中的通知面板（带有对失败数据流发出警报的通知）突出显示。](../../images/tutorials/templates/notifications.png)

您可以更新模板的警报设置，以接收有关数据流状态的电子邮件和平台内通知。 有关配置警报的更多信息，请阅读以下指南： [如何订阅源数据流的警报](../ui/alerts.md).