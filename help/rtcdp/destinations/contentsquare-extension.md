---
keywords: contentsquare extension;contentsquare destination;contentsquare
title: Contentsquare扩展
seo-title: Contentsquare扩展
description: Contentsquare扩展是实时客户数据平台中的一个分析目标。 有关扩展功能的详细信息，请参阅AdobeExchange上的扩展页。
seo-description: Contentsquare扩展是实时客户数据平台中的一个分析目标。 有关扩展功能的详细信息，请参阅AdobeExchange上的扩展页。
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 6%

---


# [!DNL Contentsquare] 扩展 {#contentsquare-extension}

## 概述 {#overview}

可视化页面内行为，了解客户放弃的原因以及您可以如何改进。 将收入归因于每个Analytics区段和目标测试的UX和内容元素。 安装标 [!DNL Contentsquare] 签、设置自定义变量和事件。 开始只需单击几下，即可收集UX分析的数据。

[!DNL Contentsquare] 是实时客户数据平台中的分析扩展。 有关扩展功能的详细信息，请参阅Adobe交换上的扩 [展页](https://exchange.adobe.com/experiencecloud.details.100364.html)。

这个目的地是Adobe Experience Platform Launch。 有关Platform Launch扩展如何在Adobe实时CDP中工作的更多信息，请参阅 [Adobe Experience Platform Launch扩展概述](/help/rtcdp/destinations/experience-platform-launch-extensions.md)。

![Contentsquare扩展](assets/contentsquare-extension.png)


## 先决条件 {#prerequisites}

此扩展位于目录 [!DNL Destinations] 中，面向所有已购买Adobe实时CDP的客户。

要使用此扩展，您需要访问Adobe Experience Platform Launch。 Platform Launch作为一项附带的增值功能提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对Platform Launch的访问权限，并要求他们授予您 **[!UICONTROL manage_properties]** （管理属性）权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

安装扩 [!DNL Contentsquare] 展：

1. 在Adobe [实时CDP界面中](http://platform.adobe.com/)，转到“目 **[!UICONTROL 标]** ”> **[!UICONTROL “目录]**”。
2. 从目录中选择扩展或使用搜索栏。
3. 单击目标以突出显示它，然后在右 **[!UICONTROL 边栏中]** 选择配置。 如果“ **[!UICONTROL 配置]** ”控件灰显，则您缺少 **[!UICONTROL manage_properties权限]** 。 请参 [阅先决条件](#prerequisites)。
4. 在“选 **[!UICONTROL 择可用的平台启动项属性]** ”窗口中，选择要在其中安装扩展的平台启动项属性。 您还可以选择在Platform Launch中创建新属性。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解Platform Launch文档 [的“属性](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) ”页面部分中的属性。
5. 该工作流将带您到Platform Launch以完成安装。

有关扩展配置选项的信息，请参 [阅Adobe交换上的](https://exchange.adobe.com/experiencecloud.details.100364.html) Contentsquare扩展页。

您还可以直接在Adobe Experience Platform Launch界面中安 [装扩展](https://launch.adobe.com/)。 请参 [阅平台启动文档](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) 中的添加新扩展。


## 如何使用扩展 {#how-to-use}

安装扩展后，您可以直接在Platform Launch中开始为其设置规则。

在Platform Launch中，您可以为已安装的扩展设置规则，以便仅在某些情况下将事件数据发送到扩展目标。 有关为扩展设置规则的详细信息，请参阅规 [则文档](https://docs.adobe.com/help/zh-Hans/launch/using/reference/manage-resources/rules.html)。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在平台启动界面中配置、升级和删除扩展。

>[!TIP]
>
>如果某个属性上已安装该扩展，Adobe实时CDP UI仍会显 **[!UICONTROL 示]** 该扩展的安装。 启动安装工作流程(如安装扩 [展中所述](#install-extension) )，以获取平台启动并配置或删除您的扩展。

要升级您的扩展，请参 [阅Platform Launch文档](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) 中的扩展升级。



