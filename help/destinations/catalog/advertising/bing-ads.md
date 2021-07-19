---
keywords: bing;bing ads事件跟踪；事件跟踪bing;UET;UET扩展
title: Bing Ads通用事件跟踪(UET)扩展
description: Bing Ads通用事件跟踪(UET)扩展是Adobe Experience Platform中的一个广告目标。 有关扩展功能的更多信息，请参阅Exchange上的扩展页面Adobe。
exl-id: f2fc4d1f-01b0-4813-902c-9a3c30a8fa78
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 5%

---

# [!DNL Bing Ads Universal Event Tracking] (UET)扩展 {#bing-ads-extension}

## 概述 {#overview}

[!DNL Bing Ads Universal Event Tracking] (UET)for是 [!DNL Experience Platform Launch] 一种有用的方法，用于跟踪用户点击您的搜索广告后所发生的情况。通过使用单个UET标记记录客户在您网站上的行为，您可以利用该数据，从而使用再营销列表跟踪转化或定位受众。

[!DNL Bing Ads Universal Event Tracking] (UET)是Adobe Experience Platform的一项广告扩展。有关扩展功能的更多信息，请参阅[AdobeExchange](https://exchange.adobe.com/experiencecloud.details.100154.html)上的扩展页面。

此目标是[!DNL Adobe Experience Platform Launch]扩展。 有关[!DNL Platform Launch]扩展如何在Platform中工作的更多信息，请参阅[Experience Platform Launch扩展概述](../launch-extensions/overview.md)。

![Bing Ads扩展](../../assets/catalog/advertising/bing-ads/catalog.png)

## 先决条件 {#prerequisites}

[!DNL Destinations]目录中提供了此扩展，可供已购买Platform的所有客户使用。

要使用此扩展，您需要访问[!DNL Adobe Experience Platform Launch]。 [!DNL Platform Launch] 以内置增值功能的形式提供给Adobe Experience Cloud客户。请联系您的组织管理员以获取[!DNL Platform Launch]的访问权限，并要求他们授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

要安装[!DNL Bing Ads Universal Event Tracking](UET)扩展，请执行以下操作：

在[Platform接口](http://platform.adobe.com/)中，转到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL Catalog]**。

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后选择右边栏中的&#x200B;**[!UICONTROL 配置]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控件呈灰显状态，则您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限。 请参阅[先决条件](#prerequisites)。

在&#x200B;**[!UICONTROL 选择可用的Platform launch属性]**&#x200B;窗口中，选择要在其中安装扩展的[!DNL Platform Launch]属性。 您还可以选择在[!DNL Platform Launch]中创建新属性。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解[!DNL Launch]文档的[属性页面部分](../../../tags/ui/administration/companies-and-properties.md#properties-page)中的属性。

工作流会引导您完成[!DNL Platform Launch]安装。

有关扩展配置选项和安装支持的信息，请参阅AdobeExchange](https://exchange.adobe.com/experiencecloud.details.100154.html)上的[Bing Ads通用事件跟踪(UET)页面。

您还可以直接在[Adobe Experience Platform Launch界面](https://launch.adobe.com/)中安装该扩展。 请参阅[!DNL Platform Launch]文档中的[添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 。


## 如何使用扩展 {#how-to-use}

安装该扩展后，便可以直接在[!DNL Platform Launch]中为其设置规则。

在[!DNL Platform Launch]中，您可以为已安装的扩展设置规则，以便仅在某些情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅[规则文档](../../../tags/ui/managing-resources/rules.md)。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在[!DNL Platform Launch]界面中配置、升级和删除扩展。

>[!TIP]
>
>如果您的某个资产上已安装扩展，则Platform UI仍会为该扩展显示&#x200B;**[!UICONTROL Install]**。 按照[Install extension](#install-extension)中所述启动安装工作流，以转到[!DNL Platform Launch]并配置或删除您的扩展。

要升级扩展，请参阅[!DNL Platform Launch]文档中的[扩展升级](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 。
