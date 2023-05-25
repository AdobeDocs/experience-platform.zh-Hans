---
keywords: bing；bing ads事件跟踪；事件跟踪bing；UET；UET扩展
title: Bing Ads通用事件跟踪(UET)扩展
description: Bing Ads通用事件跟踪(UET)扩展是Adobe Experience Platform中的一个广告目标。 有关扩展功能的更多信息，请参阅Adobe交换上的扩展页面。
exl-id: f2fc4d1f-01b0-4813-902c-9a3c30a8fa78
source-git-commit: c8d6c156b3351324fe1be11144afeae91f7a2a59
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 4%

---

# [!DNL Bing Ads Universal Event Tracking] (UET)扩展 {#bing-ads-extension}

## 概述 {#overview}

此 [!DNL Bing Ads Universal Event Tracking] (UET)标记扩展是一种跟踪某人单击您的搜索广告后所发生情况的有用方法。 通过使用单个UET标记来记录客户在您的网站上的行为，您可以利用该数据，从而允许您使用再营销列表跟踪转化或目标受众。

[!DNL Bing Ads Universal Event Tracking] (UET)是Adobe Experience Platform中的一个广告扩展。 有关扩展功能的更多信息，请参阅上的扩展页面 [Adobe交换](https://exchange.adobe.com/experiencecloud.details.100154.html).

此目标是标记扩展。 有关标记扩展如何在Platform中工作的更多信息，请参阅 [标记扩展概述](../launch-extensions/overview.md).

![Bing Ads扩展](../../assets/catalog/advertising/bing-ads/catalog.png)

## 先决条件 {#prerequisites}

此扩展位于 [!DNL Destinations] 适用于已购买Platform的所有客户的目录。

要使用此扩展，您需要访问Adobe Experience Platform中的标记。 标记以内置增值功能的方式提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对标记的访问权限，并要求他们授予您 **[!UICONTROL manage_properties]** 权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

安装 [!DNL Bing Ads Universal Event Tracking] (UET)扩展：

在 [平台界面](https://platform.adobe.com/)，转到 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**.

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后选择 **[!UICONTROL 配置]** 在右边栏中。 如果 **[!UICONTROL 配置]** 控件呈灰显状态，您缺少的是 **[!UICONTROL manage_properties]** 许可。 参见 [先决条件](#prerequisites).

选择要在其中安装扩展的标记属性。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解中的属性 [标记文档](../../../tags/ui/administration/companies-and-properties.md).

该工作流会将您转到数据收集UI以完成安装。

有关扩展配置选项和安装支持的信息，请参阅 [“Adobe交换”上的“Bing Ads通用事件跟踪(UET)”页面](https://exchange.adobe.com/experiencecloud.details.100154.html).

您还可以直接在中安装扩展 [数据收集UI](https://experience.adobe.com/#/data-collection/). 请参阅指南，网址为 [添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 了解更多信息。


## 如何使用扩展 {#how-to-use}

安装扩展后，即可开始设置规则。 在数据收集UI中，您可以为已安装的扩展设置规则，以便仅在特定情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅 [规则](../../../tags/ui/managing-resources/rules.md) 标记文档中的。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果某个资产上已安装该扩展，则仍会显示UI **[!UICONTROL 安装]** 作为扩展。 启动安装工作流，如中所述 [安装扩展](#install-extension) 以配置或删除扩展。

要升级扩展，请参阅 [扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 标记文档中的。
