---
keywords: Marketo Munchkin;marketo munchkin;Marketo Munchkin extension;marketo munchkin extension;marketo;Marketo
title: Marketo Munchkin 扩展
seo-title: Marketo Munchkin 扩展
description: Marketo Munchkin扩展是实时客户数据平台中的个性化目标。 有关扩展功能的详细信息，请参阅AdobeExchange上的扩展页。
seo-description: Marketo Munchkin扩展是实时客户数据平台中的个性化目标。 有关扩展功能的详细信息，请参阅AdobeExchange上的扩展页。
translation-type: tm+mt
source-git-commit: 80db19822551883da272787affb6f7dc9dc3a745
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 7%

---


# [!DNL Marketo Munchkin] 扩展 {#marketo-munchkin-extension}

## 概述 {#overview}

从销售线索管理到基于帐户的营销 [!DNL Marketo Engagement Platform] ，您可以简化在客户和潜在客户体验的每个阶段规划、编排和衡量客户与客户的互动。

[!DNL Marketo’s Munchkin][!DNL Marketo] JavaScript 允许跟踪最终用户对 登陆页面和外部网页的访问次数和点击次数。

[!DNL Marketo Munchkin] 是实时客户数据平台中的电子邮件扩展。 有关扩展功能的详细信息，请参阅Adobe交换上的扩 [展页](https://exchange.adobe.com/experiencecloud.details.101054.marketo-munchkin.html)。

这个目的地是Adobe Experience Platform Launch。 有关Platform Launch扩展如何在实时CDP中工作的更多信息，请参阅 [Adobe Experience Platform Launch扩展概述](../launch-extensions/overview.md)。

![Marketo Munchkin 扩展](../../assets/catalog/email/marketo-munchkin/catalog.png)

## 先决条件 {#prerequisites}

此扩展位于目录 [!DNL Destinations] 中，供所有已购买实时CDP的客户使用。

要使用此扩展，您需要访问Adobe Experience Platform Launch。 Platform Launch作为一项附带的增值功能提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对Platform Launch的访问权限，并要求他们授予您 **[!UICONTROL manage_properties]** （管理属性）权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

安装扩 [!DNL Marketo Munchkin] 展：

在实 [时CDP界面中](http://platform.adobe.com/)，转到“目 **[!UICONTROL 标]** ” **[!UICONTROL >“]**&#x200B;目录”。

从目录中选择扩展或使用搜索栏。

单击目标以突出显示它，然后在右 **[!UICONTROL 边栏中]** 选择配置。 如果“ **[!UICONTROL 配置]** ”控件灰显，则您缺少 **[!UICONTROL manage_properties权限]** 。 请参 [阅先决条件](#prerequisites)。

在“选 **[!UICONTROL 择可用的平台启动项属性]** ”窗口中，选择要在其中安装扩展的平台启动项属性。 您还可以选择在Platform Launch中创建新属性。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解Platform Launch文档 [的“属性](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) ”页面部分中的属性。

该工作流将带您到Platform Launch以完成安装。

有关扩展配置选项和安装支持的信息，请参 [阅AdobeExchange的Marketo Munchkin页](https://exchange.adobe.com/experiencecloud.details.101054.marketo-munchkin.html)。

您还可以直接在Adobe Experience Platform Launch界面中安 [装扩展](https://launch.adobe.com/)。 请参 [阅平台启动文档](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) 中的添加新扩展。

## 如何使用扩展 {#how-to-use}

安装扩展后，您可以直接在Platform Launch中开始为其设置规则。

在Platform Launch中，您可以为已安装的扩展设置规则，以便仅在某些情况下将事件数据发送到扩展目标。 有关为扩展设置规则的详细信息，请参阅规 [则文档](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在平台启动界面中配置、升级和删除扩展。

>[!TIP]
>
>如果某个属性上已安装该扩展，则实时CDP UI仍会显示该 **[!UICONTROL 扩展]** 的安装。 启动安装工作流程(如安装扩 [展中所述](#install-extension) )，以获取平台启动并配置或删除您的扩展。

要升级您的扩展，请参 [阅Platform Launch文档](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) 中的扩展升级。