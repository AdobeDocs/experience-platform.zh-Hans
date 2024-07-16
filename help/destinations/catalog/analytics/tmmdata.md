---
keywords: TMMData；TMM数据；TMMDATA；TMM数据
title: TMMData扩展
description: TMMData扩展是Adobe Experience Platform中的分析目标。 有关扩展功能的更多信息，请参阅Adobe Exchange上的扩展页面。
exl-id: 9f4ad50e-d964-41b0-b58e-71611bff3ead
source-git-commit: b4e869f9bc29122db4fc66ccda752a50c7db729f
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 3%

---

# [!DNL TMMData] 扩展 {#tmmdata-extension}

## 概述 {#overview}

[!DNL TMMData's] Foundation Platform for Adobe Marketing Cloud为营销团队提供了工具，使其能够访问和混合所有关键数据源（包括内部/外部和在线/离线数据），以实现有信心、全面的跨渠道分析，同时还可以自动设置营销活动并直接导入到Adobe及其他分析和BI工具。

[!DNL TMMData]是Adobe Experience Platform中的Analytics扩展。 有关扩展功能的详细信息，请参阅[Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100148.tmmdata-foundation-platform.html)上的扩展页面。

此目标是标记扩展。 有关标记扩展如何在Platform中工作的更多信息，请参阅[标记扩展概述](../launch-extensions/overview.md)。

![TMMData扩展](../../assets/catalog/analytics/tmmdata/catalog.png)

## 先决条件 {#prerequisites}

此扩展在[!DNL Destinations]目录中提供，适用于已购买Platform的所有客户。

要使用此扩展，您需要具有对Adobe Experience Platform中标记的访问权限。 标记以内置增值功能的方式提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对标记的访问权限，并要求他们授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您能够安装扩展。

## 安装扩展 {#install-extension}

要安装[!DNL TMMData]扩展，请执行以下操作：

在[平台接口](https://platform.adobe.com/)中，转到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**。

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后在右边栏中选择&#x200B;**[!UICONTROL 配置]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控件呈灰显状态，则表示您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限。 请参阅[先决条件](#prerequisites)。

选择要安装扩展的资产。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。在标记文档的[属性页面](../../../tags/ui/administration/companies-and-properties.md#properties-page)部分中了解属性。

该工作流将指导您完成安装步骤。

有关扩展配置选项和安装支持的信息，请参阅Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100148.tmmdata-foundation-platform.html)上的[TMMData页。

您还可以直接在[数据收集UI](https://experience.adobe.com/#/data-collection/)中安装该扩展。 有关详细信息，请参阅标记文档中有关[添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)的部分。

## 如何使用扩展 {#how-to-use}

安装扩展后，您可以开始设置规则。

您可以为已安装的扩展设置规则，以便仅在特定情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅[标记文档](../../../tags/ui/managing-resources/rules.md)。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果扩展已安装在您的某个资产上，则平台UI仍会显示该扩展的&#x200B;**[!UICONTROL Install]**。 按照[安装扩展](#install-extension)中的说明启动安装工作流，以配置或删除您的扩展。

要升级扩展，请参阅标记文档中的[扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)指南。
