---
keywords: Awin Advertiser mastertag extension;mastertag tag;Awin;awin;AWIN
title: Awin Advertiser Mastertag扩展
seo-title: Awin Advertiser Mastertag扩展
description: Awin Advertiser Mastertag扩展是Adobe实时客户数据平台中的一个广告目的地。 有关扩展功能的详细信息，请参阅AdobeExchange上的扩展页。
seo-description: Awin Advertiser Mastertag扩展是Adobe实时客户数据平台中的一个广告目的地。 有关扩展功能的详细信息，请参阅AdobeExchange上的扩展页。
translation-type: tm+mt
source-git-commit: 164c51e543d5eba11e4756723f3fecd84ec48f59
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 5%

---


# [!DNL Awin Advertiser Mastertag] 扩展 {#awin-mastertag-extension}

## 概述 {#overview}

它是 [!DNL MasterTag] 一个JavaScript库，包含Awin跟踪解决方案所需的所有功能，应无条件地附加到网站的每个页面（包括确认页面），但不包括显示或处理付款信息的任何页面。

[!DNL Awin Advertiser Mastertag] 是Adobe实时客户数据平台中的广告扩展。 有关扩展功能的详细信息，请参阅Adobe交换上的扩 [展页](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html)。

此目标是扩 [!DNL Experience Platform Launch] 展。 有关Launch扩展如何在Adobe实时CDP中工作的更多信息，请参阅 [Experience Platform Launch扩展概述](/help/rtcdp/destinations/experience-platform-launch-extensions.md)。

![UI中的Awin广告商Mastertag扩展](/help/rtcdp/destinations/assets/awin-mastertag-extension.png)

## 先决条件 {#prerequisites}

此扩展位于目录 [!DNL Destinations] 中，面向所有已购买Adobe实时CDP的客户。

要使用此扩展，您需要访问 [!DNL Experience Platform Launch]。 [!DNL Experience Platform Launch] 作为附带的增值功能提供给Adobe Experience Cloud客户。 请与您的组织管理员联系以 [!DNL Launch] 获取访问权限，并要求他们授予 **[!UICONTROL 您manage_properties]** 权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

安装扩 [!DNL Awin Advertiser Mastertag] 展：

1. 在Adobe [实时CDP界面中](http://platform.adobe.com/)，转到“目 **[!UICONTROL 标]** ”> **[!UICONTROL “目录]**”。
2. 从目录中选择扩展或使用搜索栏。
3. 单击目标以突出显示它，然后在右 **[!UICONTROL 边栏中]** 选择配置。 如果“ **[!UICONTROL 配置]** ”控件灰显，则您缺少 **[!UICONTROL manage_properties权限]** 。 请参 [阅先决条件](#prerequisites)。
4. 在“选 **[!UICONTROL 择可用的启动项]** ”属性窗口中， [!DNL Launch] 选择要安装扩展的属性。 您还可以在中选择创建新属性 [!DNL Launch]。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解文档的“属 [性”页面部分](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) 中的 [!DNL Launch] 属性。
5. 该工作流将帮 [!DNL Launch] 您完成安装。

有关扩展配置选项和安装支持的信息，请参 [阅AdobeExchange上的Awin Advertiser Mastertag页](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html)。

您还可以直接在Experience Platform Launch界面中安 [装扩展](https://launch.adobe.com/)。 请参 [阅在文档中添加](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) 新的 [!DNL Launch] 扩展。


## 如何使用扩展 {#how-to-use}

安装扩展后，您可以直接在中开始为它设置规则 [!DNL Launch]。

在中 [!DNL Launch]，您可以为已安装的扩展设置规则，以便仅在某些情况下才将事件数据发送到扩展目标。 有关为扩展设置规则的详细信息，请参阅规 [则文档](https://docs.adobe.com/help/zh-Hans/launch/using/reference/manage-resources/rules.html)。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在界面中配置、升级和删除扩 [!DNL Launch] 展。

>[!TIP]
>
>如果某个属性上已安装该扩展，Adobe实时CDP UI仍会显 **[!UICONTROL 示]** 该扩展的安装。 按照安装扩展中的说明启 [动安装](#install-extension) 工作流 [!DNL Launch] 程，以获取并配置或删除扩展。

要升级您的扩展，请参 [阅文档](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) 中的扩 [!DNL Launch] 展升级。
