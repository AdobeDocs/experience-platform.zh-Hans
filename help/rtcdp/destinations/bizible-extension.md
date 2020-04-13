---
title: 可变延伸
seo-title: 可变延伸
description: The Bizible扩展是Adobe实时客户数据平台中的电子邮件目标。 有关扩展功能的详细信息，请参阅Adobe Exchange上的扩展页面。
seo-description: Bizible扩展是Adobe实时客户数据平台中的电子邮件目标。 有关扩展功能的详细信息，请参阅Adobe Exchange上的扩展页面。
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# Bizible Extension {#bizible-extension}

## 概述 {#overview}

Bizbile是行业领先的B2B归因解决方案，它使您能够无法并行地查看数据，从而能够做出可促进增长的明智决策。

Bizbile是Adobe实时客户数据平台中的电子邮件扩展。 有关扩展功能的详细信息，请参阅 [Adobe Exchange上的扩展页](https://exchange.adobe.com/experiencecloud.details.101055.bizible-analytics.html)。

此目标是Experience Platform Launch扩展。 有关Launch扩展在Adobe实时CDP中的工作方式的更多信息，请参阅 [Experience Platform Launch扩展概述](/help/rtcdp/destinations/experience-platform-launch-extensions.md)。

## 先决条件 {#prerequisites}

此扩展位于“目标”目录中，可供所有已购买Adobe实时CDP的客户使用。

要使用此扩展，您需要访问Experience Platform Launch。 Experience Platform Launch作为附带的增值功能提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对Launch的访问权限，并要求他们授予您权限， **[!UICONTROL manage_properties]** 以便您可以安装扩展。

## 安装扩展 {#install-extension}

安装Bizible扩展：

1. 在 [Adobe实时CDP界面中](http://platform.adobe.com/)，转到 **[!UICONTROL Destinations > Catalog]**。
2. 从目录中选择扩展或使用搜索栏。
3. 单击目标以高亮显示它，然后在右 **[!UICONTROL Install Extension]** 边栏中选择。 如果控 **[!UICONTROL Install Extension]** 件灰显，则表示您缺少该权 **[!UICONTROL manage_properties]** 限。 请参阅 [先决条件](#prerequisites)。
4. 在窗 **[!UICONTROL Select available Launch property]** 口中，选择要在其中安装扩展的启动项属性。 您还可以选择在启动项中创建新属性。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解启动文档的“ [属性”页面部分](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) 中的属性。
5. 该工作流将引导您进入Launch以完成安装。

有关扩展配置选项和安装支持的信息，请参 [阅Adobe Exchange上的“可见”页](https://exchange.adobe.com/experiencecloud.details.101055.bizible-analytics.html)。

您还可以直接在 [Experience Platform Launch界面中安装扩展](https://launch.adobe.com/)。 请参 [阅启动文档中的](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) “添加新扩展”。

## 如何使用扩展 {#how-to-use}

安装扩展后，您可以在Launch中直接开始为其设置规则。

在Launch中，您可以为已安装的扩展设置规则，以便仅在某些情况下才将事件数据发送到扩展目标。 有关为扩展设置规则的详细信息，请参阅规 [则文档](https://docs.adobe.com/help/zh-Hans/launch/using/reference/manage-resources/rules.html)。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在启动界面中配置、升级和删除扩展。

>[!TIP]
>
>如果某个属性上已安装该扩展，则仍会显示该扩展的Adobe实时CDP **[!UICONTROL Install]** 用户界面。 启动安装工作流程(如安装扩 [展中所述](#install-extension) )，以转到启动并配置或删除您的扩展。

要升级您的扩展，请参阅 [Launch文档中的](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) “扩展升级”。