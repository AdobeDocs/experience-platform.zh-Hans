---
title: Adform扩展
seo-title: Adform扩展
description: Adform扩展是Adobe实时客户数据平台中的一个分析目标。 有关扩展功能的详细信息，请参阅Adobe Exchange上的扩展页。
seo-description: Adform扩展是Adobe实时客户数据平台中的一个分析目标。 有关扩展功能的详细信息，请参阅Adobe Exchange上的扩展页。
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 5%

---


# Adform扩展 {#adform-extension}

## 概述 {#overview}

Adform网站跟踪扩展使广告商能够使用该平台在其网站上轻松实施Adform跟踪 [!DNL Experience Platform Launch] 点。

[!DNL Adform] 是Adobe实时客户数据平台中的分析扩展。 有关扩展功能的详细信息，请参阅Adobe Exchange上的扩 [展页面](https://exchange.adobe.com/experiencecloud.details.103195.adform-website-tracking.html)

此目标是扩 [!DNL Experience Platform Launch] 展。 有关扩展在Adobe [!DNL Launch] 实时CDP中的工作方式的更多信息，请参阅 [Experience Platform Launch扩展概述](/help/rtcdp/destinations/experience-platform-launch-extensions.md)。

![Adform扩展](/help/rtcdp/destinations/assets/adform-extension.png)

## 先决条件 {#prerequisites}

此扩展可在目录 [!DNL Destinations] 中找到已购买Adobe实时CDP的所有客户。

要使用此扩展，您需要访问 [!DNL Experience Platform Launch]。 [!DNL Experience Platform Launch] 作为附带的增值功能提供给Adobe Experience Cloud客户。 请与您的组织管理员联系以 [!DNL Launch] 获取访问权限，并要求他们授予 **[!UICONTROL 您manage_properties]** 权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

安装Adform扩展：

1. 在Adobe [实时CDP界面中](http://platform.adobe.com/)，转到“目 **[!UICONTROL 标”>“目录”]**。
2. 从目录中选择扩展或使用搜索栏。
3. 单击目标以选中它，然后在右边 **[!UICONTROL 栏中选择]** “安装扩展”。 如果“安 **[!UICONTROL 装扩展]** ”控件灰显，则您缺少 **[!UICONTROL manage_properties]** 权限。 请参 [阅先决条件](#prerequisites)。
4. 在“选 **[!UICONTROL 择可用的启动项]** ”属性窗口中， [!DNL Launch] 选择要安装扩展的属性。 您还可以在启动项中选择创建新属性。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解文档的“属 [性”页面部分](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) 中的 [!DNL Launch] 属性。
5. 该工作流将帮 [!DNL Launch] 您完成安装。

有关扩展配置选项和安装支持的信息，请参 [阅Adobe Exchange的Adform页](https://exchange.adobe.com/experiencecloud.details.103195.adform-website-tracking.html)。

您还可以直接在Experience Platform Launch界面中安 [装扩展](https://launch.adobe.com/)。 请参 [阅在文档中添加](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) 新的 [!DNL Launch] 扩展。


## 如何使用扩展 {#how-to-use}

安装扩展后，您可以直接在中开始为它设置规则 [!DNL Launch]。

在中 [!DNL Launch]，您可以为已安装的扩展设置规则，以便仅在某些情况下才将事件数据发送到扩展目标。 有关为扩展设置规则的详细信息，请参阅规 [则文档](https://docs.adobe.com/help/zh-Hans/launch/using/reference/manage-resources/rules.html)。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在界面中配置、升级和删除扩 [!DNL Launch] 展。

>[!TIP]
>
>如果某个属性上已安装该扩展，Adobe实时CDP UI仍会显示该 **[!UICONTROL 扩展]** 的安装。 按照安装扩展中的说明启 [动安装](#install-extension) 工作流 [!DNL Launch] 程，以获取并配置或删除扩展。

要升级您的扩展，请参 [阅文档](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) 中的扩 [!DNL Launch] 展升级。



