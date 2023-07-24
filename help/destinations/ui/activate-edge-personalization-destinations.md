---
title: 将受众激活到边缘个性化目标
description: 了解如何为同一页面和下一页面个性化用例将受众从Adobe Experience Platform激活到边缘个性化目标。
type: Tutorial
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 2%

---


# 将受众激活到边缘个性化目标

## 概述 {#overview}

Adobe Experience Platform使用 [边缘分割](../../segmentation/ui/edge-segmentation.md) 与Edge目标相结合，使客户能够实时大规模创建和定位受众。 此功能可帮助您配置同页和下一页个性化用例。

Edge目标的示例包括 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自定义个性化](../../destinations/catalog/personalization/custom-personalization.md) 连接。

>[!NOTE]
>
>时间 [配置Adobe Target连接](../catalog/personalization/adobe-target-connection.md) 如果不使用数据流ID，则不支持本文中描述的用例。 在没有数据流的情况下，仅支持下一会话个性化用例。

>[!IMPORTANT]
> 
> * 要激活数据并启用 [映射步骤](#mapping) 的工作流，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions).
> * 要激活数据，而不通过 [映射步骤](#mapping) 的工作流，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活没有映射的区段]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions).
> 
> 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

本文介绍了在Adobe Experience Platform Edge目标中激活受众所需的工作流。 当与一起使用时 [边缘分割](../../segmentation/ui/edge-segmentation.md) 和可选的 [配置文件属性映射](#mapping)，这些目标在您的Web和移动资产上启用同页和下一页个性化用例。

有关如何为Edge个性化配置Adobe Target连接的简短概述，请观看以下视频。

>[!NOTE]
>
>Experience Platform用户界面经常更新，自从录制此视频以来，可能已经更改。 有关最新信息，请参阅以下部分中描述的配置步骤。

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

有关如何将受众和配置文件属性共享到Adobe Target和自定义个性化目标的简短概述，请观看以下视频。

>[!VIDEO](https://video.tv.adobe.com/v/3419036/?quality=12&learn=on)

## 用例 {#use-cases}

Edge个性化目标使您能够使用Adobe个性化解决方案(如Adobe Target)或您自己的个性化合作伙伴平台(例如， [!DNL Optimizely]， [!DNL Pega])，以及专有系统（例如，内部CMS），以通过提供更深入的客户个性化体验 [自定义个性化](../catalog/personalization/custom-personalization.md) 目标。 所有这些功能的同时，还利用Experience Platform边缘网络数据收集和分段功能。

下面介绍的用例包括网站个性化和有针对性的网站广告。

要启用这些用例，客户需要一种快速、简化的方式，从Experience Platform中检索受众和配置文件属性信息，然后将此信息发送至 [Adobe Target](../catalog/personalization/adobe-target-connection.md) 或 [自定义个性化](../catalog/personalization/custom-personalization.md) Experience PlatformUI中的连接。

### 同一页面个性化 {#same-page}

用户访问您网站的页面。 客户可以使用当前页面访问信息（例如，引荐URL、浏览器语言、嵌入的产品信息）选择下一个操作/决策（例如，个性化），使用 [自定义个性化](../catalog/personalization/custom-personalization.md) 非Adobe平台的连接(例如， [!DNL Pega]， [!DNL Optimizely]、等)。

### 下一页面个性化 {#next-page}

用户访问您网站上的页面A。 基于此交互，用户已符合一组受众的资格。 然后，用户单击一个链接，该链接会将用户从页面A转到页面B。用户在上一次与页面A进行交互期间符合条件的受众，以及由当前网站访问决定的用户档案更新，将用于支持下一个操作/决策（例如，向访客显示哪个广告横幅，或者在A/B测试的情况下，显示哪个页面版本）。

### 下一个会话个性化 {#next-session}

用户访问您网站上的多个页面。 根据这些交互，用户已符合一组受众的资格。 然后，用户终止当前浏览会话。

第二天，用户返回到同一客户网站。 之前与所有访问过的网站页面交互时，他们符合条件的受众，加上当前网站访问决定的用户档案更新，将用于选择下一个操作/决策（例如，向访客显示哪个广告横幅，或者在A/B测试的情况下，显示哪个页面版本）。

### 个性化主页横幅 {#home-page-banner}

一家家庭租赁和销售公司希望根据Adobe Experience Platform中的受众资格条件，使用横幅来个性化其主页。 公司可以选择应该获得个性化体验的受众，并将这些受众发送到Adobe Target作为其Target选件的定位标准。

## 先决条件 {#prerequisites}

### 在数据收集UI中配置数据流 {#configure-datastream}

设置个性化目标的第一步是为Experience PlatformWeb SDK配置数据流。 此操作可在数据收集UI中完成。

配置数据流时，位于 **[!UICONTROL Adobe Experience Platform]** 确保两者 **[!UICONTROL 边缘分段]** 和 **[!UICONTROL 个性化目标]** 已选中。

![数据流配置](../assets/ui/activate-edge-personalization-destinations/datastream-config.png)

有关如何设置数据流的更多详细信息，请按照 [Platform Web SDK文档](../../datastreams/configure.md#aep).

### 创建 [!DNL Active-On-Edge] 合并策略 {#create-merge-policy}

创建目标连接后，必须创建 [!DNL Active-On-Edge] 合并策略。 此 [!DNL Active-On-Edge] 合并策略可确保不断评估受众 [在边缘](../../segmentation/ui/edge-segmentation.md) 和可用于实时和下一页个性化用例。

>[!IMPORTANT]
>
>目前，Edge目标仅支持激活使用 [Active-on-Edge合并策略](../../segmentation/ui/segment-builder.md#merge-policies) 设置为默认值。 如果将使用不同合并策略的受众映射到边缘目标，则不会评估这些受众。

按照上的说明操作 [创建合并策略](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)，并确保启用 **[!UICONTROL Active-On-Edge合并策略]** 切换。

### 在Platform中创建新受众 {#create-audience}

创建之后 [!DNL Active-On-Edge] ，您必须在Platform中创建新受众。

请遵循 [受众生成器](../../segmentation/ui/segment-builder.md) 指南，以创建新受众，并确保 [分配](../../segmentation/ui/segment-builder.md#merge-policies) 此 [!DNL Active-On-Edge] 您在步骤3中创建的合并策略。

### 创建目标连接 {#connect-destination}

配置数据流后，可以开始配置个性化目标。

请遵循 [目标连接创建教程](../ui/connect-destination.md) 以获取有关如何创建新目标连接的详细说明。

根据您配置的目标，请参阅以下文章，了解特定于目标的先决条件和相关信息：

* [Adobe Target连接](../catalog/personalization/adobe-target-connection.md#parameters)
* [自定义个性化连接](../catalog/personalization/custom-personalization.md##parameters)

## 选择您的目标 {#select-destination}

完成先决条件后，您现在可以选择用于同页和下一页个性化的边缘个性化目标。

1. 转到 **[!UICONTROL 连接>目标]**，并选择 **[!UICONTROL 目录]** 选项卡。

   ![“目标目录”选项卡](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. 选择 **[!UICONTROL 激活受众]** ，位于要激活受众的个性化目标对应的卡片上，如下图所示。

   ![激活按钮](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. 选择要用于激活受众的目标连接，然后选择 **[!UICONTROL 下一个]**.

   ![选择目标](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. 移到下一部分以 [选择您的受众](#select-audiences).

## 选择您的受众 {#select-audiences}

使用受众名称左侧的复选框选择要激活到目标的受众，然后选择 **[!UICONTROL 下一个]**.

要选择要激活到目标的受众，请选中受众名称左侧的复选框，然后选择 **[!UICONTROL 下一个]**.

您可以根据受众的来源，从多种类型的受众中进行选择：

* **[!UICONTROL 分段服务]**：分段服务在Experience Platform中生成的受众。 请参阅 [分段文档](../../segmentation/ui/overview.md) 了解更多详细信息。
* **[!UICONTROL 自定义上传]**：受众在Experience Platform之外生成，并以CSV文件形式上传到Platform。 要了解有关外部受众的更多信息，请参阅有关以下内容的文档 [导入受众](../../segmentation/ui/overview.md#import-audience).
* 其他类型的受众，源自其他Adobe解决方案，例如 [!DNL Audience Manager].

![选择受众](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

## 映射属性 {#mapping}

>[!IMPORTANT]
>
>配置文件属性可能包含敏感数据。 为了保护此数据， **[!UICONTROL 自定义个性化]** 目标要求您使用 [边缘网络服务器API](../../server-api/overview.md) 在为基于属性的个性化配置目标时。 所有服务器API调用必须在 [已验证的上下文](../../server-api/authentication.md).
>
><br>如果您已在使用Web SDK或Mobile SDK进行集成，则可以通过添加服务器端集成来通过服务器API检索属性。
>
><br>如果不遵循上述要求，则仅基于受众会员资格进行个性化。

选择要为用户启用个性化用例的属性。 这意味着，如果属性的值发生更改或将属性添加到用户档案，则该用户档案将成为受众的成员，并将激活到个性化目标。

添加属性是可选的，您仍然可以继续下一步并在不选择属性的情况下启用同页和下一页个性化。 如果您未在此步骤中添加任何属性，则仍会根据用户档案的受众成员资格和身份映射资格进行个性化。

![显示选择了属性的映射步骤的图像](../assets/ui/activate-edge-personalization-destinations/mapping-step.png)

### 选择源属性 {#select-source-attributes}

要添加源属性，请选择 **[!UICONTROL 添加新字段]** 控制 **[!UICONTROL 源字段]** 列并搜索或导航到所需的XDM属性字段，如下所示。

![显示如何在映射步骤中选择目标属性的屏幕录制](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

### 选择目标属性 {#select-target-attributes}

要添加目标属性，请选择 **[!UICONTROL 添加新字段]** 控制 **[!UICONTROL 目标字段]** 列并键入要映射源属性的自定义属性名称。

>[!NOTE]
>
>目标属性的选择仅适用于 [自定义个性化](../catalog/personalization/custom-personalization.md) 激活工作流，以便支持目标平台中的友好名称字段映射。

![显示如何在映射步骤中选择XDM属性的屏幕录制](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)

## 计划受众导出 {#scheduling}

默认情况下， [!UICONTROL 受众计划] 页面仅显示您在当前激活流程中选择的新选定受众。

要查看激活到目标的所有受众，请使用筛选选项并禁用 **[!UICONTROL 仅显示新受众]** 筛选条件。

![所有受众](../assets/ui/activate-edge-personalization-destinations/all-audiences.png)

在 **[!UICONTROL 受众计划]** 页面中，选择每个受众，然后使用 **[!UICONTROL 开始日期]** 和 **[!UICONTROL 结束日期]** 选择器，用于配置将数据发送到目标的时间间隔。

![受众计划](../assets/ui/activate-edge-personalization-destinations/audience-schedule.png)

选择 **[!UICONTROL 下一个]** 以转到 [!UICONTROL 审核] 页面。

## 请查看 {#review}

在 **[!UICONTROL 审核]** 页面时，您可以看到所选内容的摘要。 选择 **[!UICONTROL 取消]** 来打破气流， **[!UICONTROL 返回]** 修改设置，或者 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

![审核步骤中的选择摘要。](../assets/ui/activate-edge-personalization-destinations/review.png)

### 同意政策评估 {#consent-policy-evaluation}

如果您的组织购买了 **Adobe Healthcare Shield** 或 **Adobe Privacy &amp; Security Shield**，请选择&#x200B;**[!UICONTROL 查看适用的同意策略]**&#x200B;以查看应用了哪些同意策略以及作为其结果包含在激活中的配置文件数量。阅读关于 [同意政策评估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 了解更多信息。

### 数据使用策略检查 {#data-usage-policy-checks}

在 **[!UICONTROL 审核]** 步骤，Experience Platform还会检查是否存在任何数据使用策略违规。 下面显示了一个违反策略的示例。 在解决该违规之前，您无法完成受众激活工作流。 有关如何解决策略违规的信息，请参阅 [数据使用策略违规](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) 在数据治理文档部分中。

![数据策略违规](../assets/common/data-policy-violation.png)

### 筛选受众 {#filter-audiences}

在此步骤中，您可以使用页面上的可用过滤器仅显示其计划或映射已作为此工作流的一部分更新的受众。 您还可以切换要查看的表列。

![屏幕录制，其中显示审核步骤中的可用受众筛选器。](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)

如果您对您的选择感到满意，并且未检测到违反策略的情况，请选择 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify audience activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->
