---
keywords: Awin广告商转换标签扩展；转换标签；Awin;awin;AWIN
title: Awin广告商转换标签扩展
description: Awin广告商转换标签扩展是Adobe Experience Platform中的广告目的地。 有关扩展功能的详细信息，请参阅Adobe Exchange上的扩展页。
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---


# Awin广告商转换标签扩展{#awin-conversiontag-extension}

## 概述 {#overview}

“转换标签”是AWIN.Tracking.Sale JavaScript对象的声明，该对象在确认页面上完成，以指示Mastertag已进行转换。 随后，它将执行必要的跟踪请求。

Awin广告商转化标签是Adobe Experience Platform中的广告扩展。 有关扩展功能的详细信息，请参阅[AdobeExchange](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html)上的扩展页。

此目标是[!DNL Adobe Experience Platform Launch]扩展。 有关[!DNL Platform Launch]扩展在平台中的工作方式的详细信息，请参阅[Experience Platform Launch扩展概述](../launch-extensions/overview.md)。

![UI中的Awin广告商转换标签扩展](../../assets/catalog/advertising/awin-conversion-tag/catalog.png)

## 先决条件 {#prerequisites}

此扩展可在“目标”目录中找到所有已购买平台的客户。

要使用此扩展，您需要访问[!DNL Experience Platform Launch]。 [!DNL Experience Platform Launch] 作为附带的增值功能提供给Adobe Experience Cloud客户。请联系您的组织管理员获取对[!DNL Launch]的访问权限并要求他们授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您可以安装扩展。

## 安装扩展{#install-extension}

安装[!DNL Awin Advertiser Conversion Tag]扩展：

在[平台接口](http://platform.adobe.com/)中，转到&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**。

从目录中选择扩展或使用搜索栏。

单击目标以突出显示它，然后在右边栏中选择&#x200B;**[!UICONTROL Configure]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控件灰显，则您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限。 请参阅[先决条件](#prerequisites)。

在&#x200B;**[!UICONTROL Select available Platform Launch property]**&#x200B;窗口中，选择要安装扩展的[!DNL Platform Launch]属性。 您还可以选择在[!DNL Platform Launch]中创建新属性。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解[!DNL Launch]文档的[属性页面部分](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page)中的属性。

该工作流将引导您完成[!DNL Platform Launch]安装。

有关扩展配置选项和安装支持的信息，请参阅Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html)上的[ Awin Advertiser转换标签页。

您还可以直接在[Adobe Experience Platform Launch接口](https://launch.adobe.com/)中安装扩展。 请参阅[!DNL Platform Launch]文档中的[添加新扩展](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension)。


## 如何使用扩展{#how-to-use}

安装扩展后，可以直接在[!DNL Platform Launch]中开始为它设置规则。

在[!DNL Platform Launch]中，您可以设置已安装扩展的规则，以便仅在某些情况下才将事件数据发送到扩展目标。 有关设置扩展规则的详细信息，请参阅[规则文档](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)。

## 配置、升级和删除扩展{#configure-upgrade-delete}

您可以在[!DNL Platform Launch]接口中配置、升级和删除扩展。

>[!TIP]
>
>如果某个属性上已安装该扩展，则平台UI仍会显示该扩展的&#x200B;**[!UICONTROL Install]**。 启动安装工作流，如[安装扩展](#install-extension)中所述，以访问[!DNL Platform Launch]并配置或删除您的扩展。

要升级您的扩展，请参阅[!DNL Platform Launch]文档中的[扩展升级](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html)。
