---
keywords: Marketo Munchkin;marketo munchkin;Marketo Munchkin扩展；marketo Munchkin扩展；marketo munchkin扩展；marketo;marketo
title: Marketo Munchkin 扩展
seo-title: Marketo Munchkin 扩展
description: Marketo Munchkin扩展是Adobe Experience Platform的个性化目的地。 有关扩展功能的详细信息，请参阅AdobeExchange上的扩展页。
seo-description: Marketo Munchkin扩展是Adobe Experience Platform的个性化目的地。 有关扩展功能的详细信息，请参阅AdobeExchange上的扩展页。
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 7%

---


# [!DNL Marketo Munchkin] 扩展 {#marketo-munchkin-extension}

## 概述 {#overview}

从销售线索管理到基于帐户的营销，[!DNL Marketo Engagement Platform]可简化您在客户体验的每个阶段规划、编排和衡量与客户和潜在客户的互动。

[!DNL Marketo’s Munchkin][!DNL Marketo] JavaScript 允许跟踪最终用户对 登陆页面和外部网页的访问次数和点击次数。

[!DNL Marketo Munchkin] 是Adobe Experience Platform的电子邮件分机。有关扩展功能的详细信息，请参见[AdobeExchange](https://exchange.adobe.com/experiencecloud.details.101054.marketo-munchkin.html)上的扩展页。

这个目的地是Adobe Experience Platform Launch。 有关Platform Launch扩展在Platform中的工作方式的详细信息，请参阅[Adobe Experience Platform Launch扩展概述](../launch-extensions/overview.md)。

![Marketo Munchkin 扩展](../../assets/catalog/email/marketo-munchkin/catalog.png)

## 先决条件 {#prerequisites}

此扩展位于[!DNL Destinations]目录中，可供所有已购买平台的客户使用。

要使用此扩展，您需要访问Adobe Experience Platform Launch。 Platform Launch作为一项附带的增值功能提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对Platform Launch的访问权限，并要求他们授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您可以安装扩展。

## 安装扩展{#install-extension}

安装[!DNL Marketo Munchkin]扩展：

在[平台接口](http://platform.adobe.com/)中，转至&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**。

从目录中选择扩展或使用搜索栏。

单击目标以突出显示它，然后在右边栏中选择&#x200B;**[!UICONTROL 配置]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控件灰显，则您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限。 请参阅[先决条件](#prerequisites)。

在&#x200B;**[!UICONTROL 选择可用的平台启动属性]**&#x200B;窗口中，选择要在其中安装扩展的平台启动属性。 您还可以选择在Platform Launch中创建新属性。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解平台启动文档的[属性页面部分](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page)中的属性。

该工作流将带您到Platform Launch以完成安装。

有关扩展配置选项和安装支持的信息，请参见AdobeExchange](https://exchange.adobe.com/experiencecloud.details.101054.marketo-munchkin.html)上的[Marketo Munchkin页。

您还可以直接在[Adobe Experience Platform Launch接口](https://launch.adobe.com/)中安装扩展。 请参阅平台启动文档中的[添加新扩展](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension)。

## 如何使用扩展{#how-to-use}

安装扩展后，您可以直接在Platform Launch中开始为其设置规则。

在Platform Launch中，您可以为已安装的扩展设置规则，以便仅在某些情况下将事件数据发送到扩展目标。 有关为扩展设置规则的详细信息，请参阅[规则文档](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)。

## 配置、升级和删除扩展{#configure-upgrade-delete}

您可以在平台启动界面中配置、升级和删除扩展。

>[!TIP]
>
>如果某个属性上已安装该扩展，平台UI仍显示该扩展的&#x200B;**[!UICONTROL 安装]**。 启动安装工作流程（如[安装扩展](#install-extension)中所述），以转到平台启动并配置或删除您的扩展。

要升级您的扩展，请参阅平台启动文档中的[扩展升级](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html)。