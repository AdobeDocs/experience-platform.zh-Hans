---
title: 将受众数据激活到流目标
type: Tutorial
description: 了解如何通过在Adobe Experience Platform中将现有受众映射到流目标来激活这些受众。
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: 30ad6c32d8ae8a2a68dfafd78f306209ce49b6d5
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 6%

---


# 将受众激活到流目标

>[!IMPORTANT]
> 
> * 激活受众并启用 [映射步骤](#mapping) 的工作流中，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions).
> * 要激活受众，请不通过 [映射步骤](#mapping) 的工作流中，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活没有映射的区段]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions).
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}
> 
> 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

## 概述 {#overview}

本文介绍了在Adobe Experience Platform流目标中激活受众所需的工作流。

## 先决条件 {#prerequisites}

要将受众激活到目标，您必须已成功完成 [已连接到目标](./connect-destination.md). 如果您尚未这样做，请转到 [目标目录](../catalog/overview.md)，浏览支持的目标，并配置要使用的目标。

## 选择您的目标 {#select-destination}

1. 转到 **[!UICONTROL “连接”>“目标”]**，然后选择 **[!UICONTROL 目录]** 选项卡。

   ![显示各种流目标的“目标目录”选项卡。](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 选择 **[!UICONTROL 激活受众]** ，，如下图所示。

   ![激活目标目录中突出显示的控件。](../assets/ui/activate-segment-streaming-destinations/activate-audiences-button.png)

1. 选择要用于激活受众的目标连接，然后选择 **[!UICONTROL 下一个]**.

   ![在选择目标步骤中高亮显示的目标连接。](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. 移到下一节至 [选择您的受众](#select-audiences).

## 选择您的受众 {#select-audiences}

要选择要激活到目标的受众，请选中受众名称左侧的复选框，然后选择 **[!UICONTROL 下一个]**.

您可以从多种类型的受众中进行选择，具体取决于其来源：

* **[!UICONTROL 分段服务]**：分段服务在Experience Platform中生成的受众。 请参阅 [分段文档](../../segmentation/ui/overview.md) 以了解更多详细信息。
* **[!UICONTROL 自定义上传]**：在Experience Platform之外生成的受众，以CSV文件形式上传到Platform。 要了解有关外部受众的更多信息，请参阅关于以下内容的文档： [导入受众](../../segmentation/ui/overview.md#import-audience).
* 其他类型的受众，源自其他Adobe解决方案，例如 [!DNL Audience Manager].

![在选择受众步骤中突出显示的多个受众。](../assets/ui/activate-segment-streaming-destinations/select-audiences.png)

## 映射属性和身份 {#mapping}

>[!IMPORTANT]
>
>此步骤仅适用于某些受众流目标。 如果您的目标没有 **[!UICONTROL 映射]** 步骤，跳至 [受众调度](#scheduling).
>
>将受众激活到流目标时，您还必须映射 *至少一个目标身份命名空间*，以及目标配置文件属性。 否则，受众将不会激活到目标平台。
> ![显示强制标识命名空间映射的映射步骤图像。](../assets/ui/activate-segment-streaming-destinations/identity-mapping-mandatory.png) {zoomable="yes"}


某些受众流目标要求您选择源属性或身份命名空间以映射为目标中的目标身份。

1. 在 **[!UICONTROL 映射]** 页面，选择 **[!UICONTROL 添加新映射]**.

   ![添加突出显示的新映射控件。](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. 选择右侧的箭头 **[!UICONTROL 源字段]** 进入。

   ![选择高亮显示的源字段控件。](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. 在 **[!UICONTROL 选择源字段]** 页面，使用 **[!UICONTROL 选择属性]** 或 **[!UICONTROL 选择身份命名空间]** 用于在这两种可用源字段之间切换的选项。 从可用的 [!DNL XDM] 配置文件属性和身份命名空间，选择要映射到目标的配置文件属性和身份命名空间，然后选择 **[!UICONTROL 选择]**.

   使用 **[!UICONTROL 仅显示包含数据的字段]** 切换以仅显示使用值填充的架构字段。 默认情况下，仅显示填充的架构字段。

   ![显示多个可用源字段的“选择源字段”页。](../assets/ui/activate-segment-streaming-destinations/select-source-field-modal.png)

1. 选择右侧的按钮 **[!UICONTROL 目标字段]** 进入。

   ![选择突出显示的目标字段。](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. 在 **[!UICONTROL 选择目标字段]** 页中，选择要将源字段映射到的目标身份命名空间，然后选择 **[!UICONTROL 选择]**.

   ![选择目标字段页面，其中显示了目标字段映射的可用选项。](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. 要添加更多映射，请重复步骤1至5。

### 应用转换 {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="应用转换"
>abstract="使用未进行哈希处理的源字段时选中此选项，让 Adobe Experience Platform 在激活时自动对它们进行哈希处理。"

将未经过哈希处理的源属性映射到目标期望进行哈希处理的目标属性时(例如： `email_lc_sha256` 或 `phone_sha256`)，检查 **应用转换** 用于使Adobe Experience Platform在激活时自动哈希源属性的选项。

![应用在“身份映射”步骤中突出显示的转换控件。](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## 计划受众导出 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="结束日期"
>abstract="无法添加受众计划的结束日期。"

默认情况下， **[!UICONTROL 受众计划]** 页面仅显示您在当前激活流中选择的新选定受众。

要查看激活到目标的所有受众，请使用筛选选项并禁用 **[!UICONTROL 仅显示新受众]** 筛选。

![所有受众](../assets/ui/activate-segment-streaming-destinations/all-audiences.png)

1. 在 **[!UICONTROL 受众计划]** 页面上，选择每个受众，然后使用 **[!UICONTROL 开始日期]** 和 **[!UICONTROL 结束日期]** 选择器，用于配置向目标发送数据的时间间隔。

   ![受众计划过滤器突出显示。](../assets/ui/activate-segment-streaming-destinations/audience-schedule.png)

   * 某些目标要求您选择 **[!UICONTROL 受众来源]** 对于每个受众，使用日历选择器下的下拉菜单。 如果您的目标不包含此选择器，请跳过此步骤。

     ![突出显示了映射ID下拉列表。](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * 某些目标要求您手动映射 [!DNL Platform] 受众与其在目标中的对应受众。 为此，请选择每个受众，然后在中输入目标平台中相应的受众ID **[!UICONTROL 映射Id]** 字段。 如果您的目标不包含此字段，请跳过此步骤。

     ![突出显示的“受众来源”下拉列表。](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * 某些目标要求您输入 **[!UICONTROL 应用程序ID]** 激活时 [!DNL IDFA] 或 [!DNL GAID] 受众。 如果您的目标不包含此字段，请跳过此步骤。

     ![应用程序ID下拉列表突出显示。](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. 选择 **[!UICONTROL 下一个]** 以转到 [!UICONTROL 审核] 页面。

## 审查 {#review}

在 **[!UICONTROL 审核]** 页面上，您可以看到选择的摘要。 选择 **[!UICONTROL 取消]** 来打破气流， **[!UICONTROL 返回]** 以修改设置，或者 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

![审核步骤中的选择摘要。](../assets/ui/activate-segment-streaming-destinations/review.png)

### 同意策略评估 {#consent-policy-evaluation}

如果您的组织购买了 **Adobe Healthcare Shield** 或 **Adobe Privacy &amp; Security Shield**，请选择&#x200B;**[!UICONTROL 查看适用的同意策略]**&#x200B;以查看应用了哪些同意策略以及作为其结果包含在激活中的配置文件数量。阅读关于 [同意政策评估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 以了解更多信息。

### 数据使用策略检查 {#data-usage-policy-checks}

在 **[!UICONTROL 审核]** 步骤，Experience Platform还会检查是否存在任何数据使用策略违规。 下面显示了一个违反策略的示例。 在解决该违规之前，您无法完成受众激活工作流。 有关如何解决策略违规的信息，请参阅 [数据使用策略违规](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) 数据管理文档一节中。

![激活工作流中显示的数据策略违规示例。](../assets/common/data-policy-violation.png)

### 筛选受众 {#filter-audiences}

此外，在此步骤中，您可以使用页面上的可用过滤器仅显示其计划或映射作为此工作流的一部分而更新的受众。 您还可以切换要查看的表列。

![显示审核步骤中可用的受众过滤器的屏幕录制。](../assets/ui/activate-segment-streaming-destinations/filter-audiences-review-step.gif)

如果您对您的选择感到满意，并且未检测到任何违反策略的情况，请选择 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

## 验证受众激活 {#verify}

查看 [目标监视文档](../../dataflows/ui/monitor-destinations.md) ，了解有关如何监控流向您目标的数据流的详细信息。

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Audience membership in the audience would be added and removed as users are qualified or disqualified for the activated audiences.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical audience qualifications are sent to [!DNL Facebook] when you activate the audiences to the destination.
-->
