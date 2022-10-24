---
keywords: Experience Platform；主页；热门主题；
description: Adobe Experience Platform提供了预配置的模板，您可以使用这些模板来加快数据摄取流程。 模板包括自动生成的资产，例如架构、数据集、映射规则、身份命名空间和数据流，在将数据从源引入到Experience Platform时，可以使用这些资产。
title: (Alpha)使用UI中的模板创建源数据流
hide: true
hidefromtoc: true
source-git-commit: a0ca9cff43b6f8276268467fecf944c664992950
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 1%

---

# (Alpha)使用UI中的模板创建源数据流

>[!IMPORTANT]
>
>模板位于Alpha中，当前仅受 [[!DNL Marketo Engage] 来源](../../connectors/adobe-applications/marketo/marketo.md). 文档和功能可能会发生更改。

Adobe Experience Platform提供了预配置的模板，您可以使用这些模板来加快数据摄取流程。 模板包括自动生成的资产，例如架构、数据集、映射规则、身份命名空间和数据流，在将数据从源引入到Experience Platform时，可以使用这些资产。

使用模板，您可以：

* 通过加快基于ML的资产创建，可缩短摄取的时间和价值实现。
* 最大限度地减少在手动数据获取过程中可能发生的错误。
* 随时更新自动生成的资产，以适合您的用例。

以下教程提供了有关如何在Platform UI中使用模板的步骤 [[!DNL Marketo Engage] 来源](../../connectors/adobe-applications/marketo/marketo.md).

## 快速入门

本教程需要对Experience Platform的以下组件有一定的了解：

* [源](../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 在平台UI中使用模板 {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="选择业务类型"
>abstract="为您的用例选择适当的业务类型。 您的访问权限可能因您的Real-time Customer Data Platform订阅帐户而异。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=zh-Hans" text="Real-Time CDP概述"

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕显示可用于创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在 [!UICONTROL Adobe应用程序] 类别，选择 **[!UICONTROL Marketo Engage]** 然后选择 **[!UICONTROL 添加数据]**.

![突出显示源的源工作区目录。Marketo Engage源。](../../images/tutorials/templates/catalog.png)

此时会出现一个弹出窗口，向您提供浏览模板或使用现有架构和数据集的选项。 要使用自动生成的资产，请选择 **[!UICONTROL 浏览模板]** 然后选择 **[!UICONTROL 选择]**.

![一个弹出窗口，其中提供了用于浏览模板或使用现有资产的选项。](../../images/tutorials/templates/browse-templates.png)

### 身份验证

此时会显示身份验证步骤，提示您创建新帐户或使用现有帐户。

#### 现有帐户

要使用现有帐户，请选择 [!UICONTROL 现有帐户] 然后，从显示的列表中选择要使用的帐户。

![现有帐户的选择页面，其中包含您可以访问的现有帐户列表。](../../images/tutorials/templates/existing-account.png)

#### 新帐户

要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后提供源连接详细信息和帐户身份验证凭据。 完成后，选择 **[!UICONTROL 连接到源]** 并留出一些时间建立新连接。

![具有源连接详细信息和帐户身份验证凭据的新帐户的身份验证页面。](../../images/tutorials/templates/new-account.png)

### 选择模板

验证并选择帐户后，会显示模板列表。 选择模板名称旁边的预览图标，以预览模板中的示例数据。

![高亮显示预览图标的模板列表。](../../images/tutorials/templates/templates.png)

此时将显示预览窗口，用于浏览和检查模板中的示例数据。 完成后，选择 **[!UICONTROL 收到了]**.

![预览示例数据窗口。](../../images/tutorials/templates/preview-sample-data.png)

接下来，从列表中选择要使用的模板。 您可以选择多个模板并一次创建多个数据流。 但是，每个帐户只能使用一次模板。 选择模板后，选择 **[!UICONTROL 完成]** 并允许一些时间生成资产。

![选择了Opportunity Contact Role模板的模板列表。](../../images/tutorials/templates/select-template.png)

### 审核资产 {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="查看自动生成的资产"
>abstract="最多可能需要五分钟才能生成所有资产。 如果您选择离开页面，则会在资产完成后收到返回通知。 在生成资产后，您便可以查看资产，并随时为数据流进行其他配置。"

的 [!UICONTROL 审核模板资产] 页面会将自动生成的资产显示为模板的一部分。 在本页中，您可以查看与源连接关联的自动生成的架构、数据集、身份命名空间和数据流。

默认情况下，会启用自动生成的数据流。 选择省略号(`...`)，然后选择 **[!UICONTROL 预览映射]** 以查看为数据流创建的映射集。

![选择了预览映射选项的下拉窗口。](../../images/tutorials/templates/preview.png)

此时会显示预览页，用于检查源数据字段和目标架构字段之间的映射关系。 查看数据流的映射后。 选择 **[!UICONTROL 明白了。]**

![映射预览窗口。](../../images/tutorials/templates/preview-mappings.png)

您可以在执行后随时更新数据流。 选择省略号(`...`)，然后选择 **[!UICONTROL 更新数据流]**. 您将转到源工作流页面，在该页面中可以更新数据流详细信息，包括部分摄取、错误诊断和警报通知的设置，以及数据流的映射。

![选择了更新数据流选项的下拉窗口。](../../images/tutorials/templates/update.png)

## 后续步骤

在本教程之后，您现在已使用模板创建数据流以及模式、数据集和身份命名空间等资产。 有关来源的一般信息，请访问 [源概述](../../home.md).