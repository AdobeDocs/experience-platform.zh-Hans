---
keywords: 激活区段流目标；激活区段流目标；激活数据
title: 将受众数据激活到流区段导出目标
type: Tutorial
seo-title: 将受众数据激活到流区段导出目标
description: 了解如何通过将区段映射到区段流目标，来激活您在Adobe Experience Platform中拥有的受众数据。
seo-description: 了解如何通过将区段映射到区段流目标，来激活您在Adobe Experience Platform中拥有的受众数据。
source-git-commit: c3e273c66ffe0542258e5418104e0bcf154f5235
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---


# 将受众数据激活到流区段导出目标

## 概述 {#overview}

本文介绍了在Adobe Experience Platform区段流目标中激活受众数据所需的工作流。

## 先决条件 {#prerequisites}

要将数据激活到目标，您必须已成功地[连接到目标](./connect-destination.md)。 如果您尚未执行此操作，请转到[目标目录](../catalog/overview.md)，浏览支持的目标，并配置要使用的目标。

## 选择您的目标 {#select-destination}

1. 转到&#x200B;**[!UICONTROL 连接>目标]**，然后选择&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡。

   ![“目标浏览”选项卡](../assets/ui/activate-segment-streaming-destinations/browse-tab.png)

1. 选择与要激活区段的目标对应的&#x200B;**[!UICONTROL 添加区段]**&#x200B;按钮，如下图所示。

   ![激活按钮](../assets/ui/activate-segment-streaming-destinations/activate-buttons-browse.png)

1. 移到下一部分，选择[区段](#select-segments)。

## 选择您的区段 {#select-segments}

使用区段名称左侧的复选框选择要激活到目标的区段，然后选择&#x200B;**[!UICONTROL Next]**。

![选择区段](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## 映射属性和标识 {#mapping}

>[!IMPORTANT]
>
>此步骤仅适用于某些区段流目标。 如果您的目标没有&#x200B;**[!UICONTROL 映射]**&#x200B;步骤，请跳到[计划区段导出](#scheduling)。

某些区段流目标要求您选择源属性或身份命名空间以映射为目标标识。

1. 在&#x200B;**[!UICONTROL 映射]**&#x200B;页面中，选择&#x200B;**[!UICONTROL 添加新映射]**。

   ![添加新映射](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. 选择&#x200B;**[!UICONTROL 源字段]**&#x200B;条目右侧的箭头。

   ![选择源字段](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. 在&#x200B;**[!UICONTROL 选择源字段]**&#x200B;页中，使用&#x200B;**[!UICONTROL 选择属性]**&#x200B;或&#x200B;**[!UICONTROL 选择标识命名空间]**&#x200B;选项在两类可用源字段之间切换。 从可用的[!DNL XDM]配置文件属性和身份命名空间中，选择要映射到目标的属性和命名空间，然后选择&#x200B;**[!UICONTROL 选择]**。

   ![“选择源字段”页](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. 选择&#x200B;**[!UICONTROL 目标字段]**&#x200B;条目右侧的按钮。

   ![选择目标字段](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. 在&#x200B;**[!UICONTROL 选择目标字段]**&#x200B;页面中，选择要将源字段映射到的目标标识命名空间，然后选择&#x200B;**[!UICONTROL 选择]**。

   ![“选择目标字段”页](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. 要添加更多映射，请重复步骤1至5。

### 应用转换 {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="应用转换"
>abstract="使用未哈希源字段时，请勾选此选项，以使Adobe Experience Platform在激活时自动对它们进行哈希处理。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#apply-transformation" text="在文档中了解更多信息"

当您将未哈希化的源属性映射到目标预期经过哈希化的目标属性时(例如：`email_lc_sha256`或`phone_sha256`)，选中&#x200B;**Apply transformation**&#x200B;选项，让Adobe Experience Platform在激活时自动对源属性进行哈希处理。

![身份映射](/help/destinations/assets/ui/activate-segment-streaming-destinations/mapping-summary.png)


## 计划区段导出 {#scheduling}

1. 在&#x200B;**[!UICONTROL 区段计划]**&#x200B;页面上，选择每个区段，然后使用&#x200B;**[!UICONTROL 开始日期]**&#x200B;和&#x200B;**[!UICONTROL 结束日期]**&#x200B;选择器来配置向目标发送数据的时间间隔。

   ![区段计划](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * 某些目标要求您使用日历选择器下方的下拉菜单，为每个区段选择&#x200B;**[!UICONTROL 受众的来源]**。 如果您的目标不包含此选择器，请跳过此步骤。

      ![映射ID](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * 某些目标要求您手动将[!DNL Platform]区段映射到目标目标中的相应区段。 要执行此操作，请选择每个区段，然后在&#x200B;**[!UICONTROL 映射ID]**&#x200B;字段中从目标平台输入相应的区段ID。 如果您的目标不包含此字段，请跳过此步骤。

      ![映射ID](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * 在激活[!DNL IDFA]或[!DNL GAID]区段时，某些目标要求您输入&#x200B;**[!UICONTROL 应用程序ID]**。 如果您的目标不包含此字段，请跳过此步骤。

      ![应用程序 ID](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. 选择&#x200B;**[!UICONTROL Next]**&#x200B;以转到[!UICONTROL Review]页面。

## 审阅 {#review}

在&#x200B;**[!UICONTROL Review]**&#x200B;页面上，您可以看到您选择的摘要。 选择&#x200B;**[!UICONTROL 取消]**&#x200B;以划分流程，选择&#x200B;**[!UICONTROL 返回]**&#x200B;以修改设置，或选择&#x200B;**[!UICONTROL 完成]**&#x200B;以确认您的选择并开始向目标发送数据。

>[!IMPORTANT]
>
>在此步骤中，Adobe Experience Platform会检查是否存在数据使用策略违规。 下面显示了违反策略的示例。 在解决违规之前，无法完成区段激活工作流。 有关如何解决策略违规的信息，请参阅数据管理文档一节中的[策略执行](../../rtcdp/privacy/data-governance-overview.md#enforcement)。

![数据策略违规](../assets/common/data-policy-violation.png)

如果未检测到任何违反策略的情况，请选择&#x200B;**[!UICONTROL 完成]**&#x200B;以确认您的选择并开始向目标发送数据。

![审阅](../assets/ui/activate-segment-streaming-destinations/review.png)

## 验证区段激活 {#verify}

检查您的目标帐户。 如果激活成功，则目标平台中会填充受众。

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
