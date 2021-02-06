---
keywords: Nielsen BSDK;nielsen bsdk;Nielsen BSDK
title: Nielsen BSDK扩展目标
description: Nielsen BSDK扩展是Adobe Experience Platform的一个分析目的地。 有关扩展功能的详细信息，请参阅AdobeExchange上的扩展页。
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 4%

---


# [!DNL Nielsen BSDK] 扩展 {#nielsen-bsdk-extension}

[!DNL Nielsen Digital SDK] 通过以下数字测量产品启动扩展优惠受众测量：

DCR:提供对非线性数字内容（包括带有广告的内容）进行日常测量的测量解决方案可全面视图桌面、移动设备、平板电脑和连接设备上的数字内容受众消费。

DTVR:这说明参加节目源在桌面和移动设备上进行的线性电视观看。 这是MRC为在计算机和移动设备上观看的节目而对电视受众衡量做出贡献的第一个获得认证的解决方案。

[!DNL Nielsen BSDK] 是Adobe Experience Platform的分析扩展。有关扩展功能的详细信息，请参见[AdobeExchange](https://exchange.adobe.com/experiencecloud.details.101361.html)上的扩展页。

这个目的地是Adobe Experience Platform Launch。 有关Platform Launch扩展在Platform中的工作方式的详细信息，请参阅[Adobe Experience Platform Launch扩展概述](../launch-extensions/overview.md)。

![Nielsen BSDK扩展](../../assets/catalog/analytics/nielsen-bsdk/catalog.png)

## 先决条件 {#prerequisites}

此扩展位于[!DNL Destinations]目录中，可供所有已购买平台的客户使用。

要使用此扩展，您需要访问Adobe Experience Platform Launch。 Platform Launch作为一项附带的增值功能提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对Platform Launch的访问权限，并要求他们授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您可以安装扩展。

## 安装扩展{#install-extension}

安装[!DNL Nielsen BSDK]扩展：

在[平台接口](http://platform.adobe.com/)中，转至&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**。

从目录中选择扩展或使用搜索栏。

单击目标以突出显示它，然后在右边栏中选择&#x200B;**[!UICONTROL 配置]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控件灰显，则您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限。 请参阅[先决条件](#prerequisites)。

在&#x200B;**[!UICONTROL 选择可用的平台启动属性]**&#x200B;窗口中，选择要在其中安装扩展的平台启动属性。 您还可以选择在Platform Launch中创建新属性。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解平台启动文档的[属性页面部分](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page)中的属性。

该工作流将带您到Platform Launch以完成安装。

有关扩展配置选项和安装支持的信息，请参阅AdobeExchange](https://exchange.adobe.com/experiencecloud.details.101361.html)上的[Nielsen BSDK页。

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