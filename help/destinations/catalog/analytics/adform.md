---
keywords: adform extension;adform
title: Adform扩展
seo-title: Adform扩展
description: Adform扩展是Adobe Experience Platform的一个分析目标。 有关扩展功能的详细信息，请参阅AdobeExchange上的扩展页。
seo-description: Adform扩展是Adobe Experience Platform的一个分析目标。 有关扩展功能的详细信息，请参阅AdobeExchange上的扩展页。
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---


# Adform扩展{#adform-extension}

## 概述 {#overview}

Adform网站跟踪扩展使广告商能够使用[!DNL Experience Platform Launch]平台在他们的网站上毫不费力地实施Adform跟踪点。

[!DNL Adform] 是Adobe Experience Platform的分析扩展。有关扩展功能的详细信息，请参见[AdobeExchange](https://exchange.adobe.com/experiencecloud.details.103195.adform-website-tracking.html)上的扩展页

此目标是[!DNL Adobe Experience Platform Launch]扩展。 有关[!DNL Platform Launch]扩展在平台中的工作方式的详细信息，请参阅[Experience Platform Launch扩展概述](../launch-extensions/overview.md)。

![Adform扩展](../../assets/catalog/analytics/adform/catalog.png)

## 先决条件 {#prerequisites}

此扩展位于[!DNL Destinations]目录中，可供所有已购买平台的客户使用。

要使用此扩展，您需要访问[!DNL Adobe Experience Platform Launch]。 [!DNL Platform Launch] 作为附带的增值功能提供给Adobe Experience Cloud客户。请与您的组织管理员联系以获取对[!DNL Platform Launch]的访问权限，并要求他们授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您可以安装扩展。

## 安装扩展{#install-extension}

安装Adform扩展：

在[平台接口](http://platform.adobe.com/)中，转至&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**。

从目录中选择扩展或使用搜索栏。

单击目标以突出显示它，然后在右边栏中选择&#x200B;**[!UICONTROL 配置]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控件灰显，则您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限。 请参阅[先决条件](#prerequisites)。

在&#x200B;**[!UICONTROL 选择可用的启动属性]**&#x200B;窗口中，选择要安装扩展的[!DNL Launch]属性。 您还可以在启动项中选择创建新属性。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解[!DNL Launch]文档的[属性页面部分](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page)中的属性。

该工作流将引导您完成[!DNL Launch]安装。

有关扩展配置选项和安装支持的信息，请参见AdobeExchange](https://exchange.adobe.com/experiencecloud.details.103195.adform-website-tracking.html)上的[Adform页。

您还可以直接在[Adobe Experience Platform Launch接口](https://launch.adobe.com/)中安装扩展。 请参阅[!DNL Platform Launch]文档中的[添加新扩展](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension)。

## 如何使用扩展{#how-to-use}

安装扩展后，您可以直接在[!DNL Platform Launch]中开始为其设置规则。

在[!DNL Platform Launch]中，您可以为已安装的扩展设置规则，以便仅在某些情况下将事件数据发送到扩展目标。 有关为扩展设置规则的详细信息，请参阅[规则文档](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)。

## 配置、升级和删除扩展{#configure-upgrade-delete}

您可以在[!DNL Platform Launch]接口中配置、升级和删除扩展。

>[!TIP]
>
>如果某个属性上已安装该扩展，平台UI仍显示该扩展的&#x200B;**[!UICONTROL 安装]**。 启动安装工作流程（如[安装扩展](#install-extension)中所述），以访问[!DNL Platform Launch]并配置或删除您的扩展。

要升级您的扩展，请参阅[!DNL Platform Launch]文档中的[扩展升级](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html)。



