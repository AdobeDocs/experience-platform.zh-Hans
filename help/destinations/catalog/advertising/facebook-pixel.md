---
keywords: facebook像素扩展；facebook像素扩展；facebook像素目标；facebook像素
title: Facebook Pixel扩展
description: facebook Pixel扩展是Adobe Experience Platform的一个广告目的地。 有关扩展功能的更多信息，请参阅Exchange上的扩展页面Adobe。
exl-id: 6a2c661f-1ad0-4d96-b1bb-bf8c158c8521
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 4%

---

# [!DNL Facebook Pixel] 扩展 {#facebook-pixel-extension}

## 概述 {#overview}

[!DNL Facebook Pixel]是一个分析工具，它允许您通过了解用户在您的网站上采取的操作来衡量广告的有效性。

[!DNL Facebook Pixel] 是Adobe Experience Platform的一项广告扩展。有关扩展功能的更多信息，请参阅[Facebook Pixel网站](https://developers.facebook.com/docs/facebook-pixel/)。

此目标是Adobe Experience Platform Launch扩展。 有关Platform launch扩展如何在Platform中工作的更多信息，请参阅[Adobe Experience Platform Launch扩展概述](../launch-extensions/overview.md)。

![Facebook Pixel扩展](../../assets/catalog/advertising/facebook-pixel/catalog.png)

## 先决条件 {#prerequisites}

[!DNL Destinations]目录中提供了此扩展，可供已购买Platform的所有客户使用。

要使用此扩展，您需要访问Adobe Experience Platform Launch。 platform launch以内置增值功能的形式提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取Platform launch的访问权限，并要求他们授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

要安装[!DNL Facebook Pixel]扩展，请执行以下操作：

在[Platform接口](http://platform.adobe.com/)中，转到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL Catalog]**。

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后选择右边栏中的&#x200B;**[!UICONTROL 配置]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控件呈灰显状态，则您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限。 请参阅[先决条件](#prerequisites)。

在&#x200B;**[!UICONTROL 选择可用的Platform launch属性]**&#x200B;窗口中，选择要在其中安装扩展的Platform launch属性。 您还可以选择在Platform launch中创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解Platform launch文档[属性页面部分](../../../tags/ui/administration/companies-and-properties.md#properties-page)中的属性。

利用工作流，可Platform launch完成安装。

您还可以直接在[Adobe Experience Platform Launch界面](https://launch.adobe.com/)中安装该扩展。 请参阅Platform launch文档中的[添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 。


## 如何使用扩展 {#how-to-use}

安装扩展后，您可以直接在Platform launch中为其设置规则。

在Platform launch中，您可以为已安装的扩展设置规则，以便仅在某些情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅[规则文档](../../../tags/ui/managing-resources/rules.md)。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在Platform launch界面中配置、升级和删除扩展。

>[!TIP]
>
>如果您的某个资产上已安装扩展，则Platform UI仍会为该扩展显示&#x200B;**[!UICONTROL Install]**。 按照[Install extension](#install-extension)中所述启动安装工作流，以开始Platform launch并配置或删除您的扩展。

要升级扩展，请参阅Platform launch文档中的[扩展升级](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 。
