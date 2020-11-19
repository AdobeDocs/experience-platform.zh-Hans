---
keywords: Confirmit Digital Feedback;confirmit extension;confirmit
title: 确认数字反馈扩展
seo-title: 确认数字反馈扩展
description: 确认数字反馈扩展是实时客户数据平台中客户目标的声音。 有关扩展功能的详细信息，请参阅AdobeExchange上的扩展页。
seo-description: 确认数字反馈扩展是实时客户数据平台中客户目标的声音。 有关扩展功能的详细信息，请参阅AdobeExchange上的扩展页。
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 4%

---


# [!DNL Confirmit Digital Feedback] 扩展

## 概述 {#overview}

[!DNL Confirmit Digital Feedback] 解决方案可帮助您将网站流量转化为实时洞察。 有了 [!DNL Confirmit]不显眼且目标明确的调查，您就可以根据您的要求显示，鼓励访客提供反馈，例如：

* 网站反馈
* 交易满意度
* 退出意图原因
* 购物车废弃信息
* 整体客户满意度
* 等等

[!DNL Confirmit] 数字反馈是实时客户数据平台中客户扩展的声音。 有关扩展功能的详细信息，请参阅Adobe交换上的扩 [展页](https://exchange.adobe.com/experiencecloud.details.103247.confirmit-digital-feedback-for-adobe-launch.html)。

这个目的地是Adobe Experience Platform Launch。 有关Platform Launch扩展如何在Adobe实时CDP中工作的更多信息，请参阅 [Adobe Experience Platform Launch扩展概述](/help/rtcdp/destinations/experience-platform-launch-extensions.md)。


![确认数字反馈扩展](assets/confirmit-digital-feedback-extension.png)

## 先决条件 {#prerequisites}

此扩展位于目录 [!DNL Destinations] 中，面向所有已购买Adobe实时CDP的客户。

要使用此扩展，您需要访问Adobe Experience Platform Launch。 Platform Launch作为一项附带的增值功能提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对Platform Launch的访问权限，并要求他们授予您 **[!UICONTROL manage_properties]** （管理属性）权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

安装数字 [!DNL Confirmit] 反馈扩展：

1. 在Adobe [实时CDP界面中](http://platform.adobe.com/)，转到“目 **[!UICONTROL 标]** ”> **[!UICONTROL “目录]**”。
2. 从目录中选择扩展或使用搜索栏。
3. 单击目标以突出显示它，然后在右 **[!UICONTROL 边栏中]** 选择配置。 如果“ **[!UICONTROL 配置]** ”控件灰显，则您缺少 **[!UICONTROL manage_properties权限]** 。 请参 [阅先决条件](#prerequisites)。
4. 在“选 **[!UICONTROL 择可用的平台启动项属性]** ”窗口中，选择要在其中安装扩展的平台启动项属性。 您还可以选择在Platform Launch中创建新属性。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解Platform Launch文档 [的“属性](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) ”页面部分中的属性。
5. 该工作流将带您到Platform Launch以完成安装。

有关扩展配置选项和安装支持的信息，请参阅 [ExchangeAdobe的“确认数字反馈”页](https://exchange.adobe.com/experiencecloud.details.103247.confirmit-digital-feedback-for-adobe-launch.html)。

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