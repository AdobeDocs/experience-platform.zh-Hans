---
keywords: Google广告；Google广告；Google广告扩展；Google Ads扩展
title: Google Ads扩展
description: Google Ads扩展是Adobe Experience Platform中的一个广告目标。 有关扩展功能的更多信息，请参阅Exchange上的扩展页面Adobe。
exl-id: b563ce68-7b04-4cfb-b0c3-151f34ec7c1a
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 3%

---

# [!DNL Google Ads] 扩展

## 概述 {#overview}

此扩展跟踪点击[!DNL Google Ads]的用户的转化。 您还需要安装gtag.js扩展并将其添加到库中，因为[!DNL Google Ads]取决于该扩展。

[!DNL Google Ads] 是Adobe Experience Platform的一项广告扩展。有关扩展功能的更多信息，请参阅[AdobeExchange](https://www.adobeexchange.com/experiencecloud.details.101383.google-ads.html)上的扩展页面。

此目标是一个标记扩展。 有关标记扩展如何在Platform中工作的更多信息，请参阅[标记扩展概述](../launch-extensions/overview.md)。

![Google Ads扩展](../../assets/catalog/advertising/google-ads-extension/catalog.png)

## 先决条件 {#prerequisites}

目标目录中提供的这项扩展适用于已购买平台的所有客户。

要使用此扩展，您需要访问Adobe Experience Platform中的标记。 以内置增值功能的形式提供给Adobe Experience Cloud客户的标记。 请联系您的组织管理员以获取对标记的访问权限，并要求他们授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您可以安装扩展。 并要求他们授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

要安装[!DNL Google Ads]扩展，请执行以下操作：

在[Platform接口](http://platform.adobe.com/)中，转到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL Catalog]**。

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后选择右边栏中的&#x200B;**[!UICONTROL 配置]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控件呈灰显状态，则您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限。 请参阅[先决条件](#prerequisites)。

选择要在其中安装扩展的资产。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解标记文档的[属性页面部分](../../../tags/ui/administration/companies-and-properties.md#properties-page)中的属性。

工作流可指导您完成完成安装的步骤。

有关扩展配置选项和安装支持的信息，请参阅AdobeExchange](https://www.adobeexchange.com/experiencecloud.details.101383.google-ads.html)上的[Google Ads页面。

您还可以直接在[数据收集UI](https://experience.adobe.com/#/data-collection/)中安装扩展。 有关更多信息，请参阅标记文档中关于[添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)的部分。

## 如何使用扩展 {#how-to-use}

安装扩展后，您可以开始设置规则。

您可以为已安装的扩展设置规则，以便仅在某些情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅[标记文档](../../../tags/ui/managing-resources/rules.md)。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果您的某个资产上已安装扩展，则Platform UI仍会为该扩展显示&#x200B;**[!UICONTROL Install]**。 按照[Install extension](#install-extension)中所述启动安装工作流，以配置或删除您的扩展。

要升级扩展，请参阅标记文档中[扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)中的指南。
