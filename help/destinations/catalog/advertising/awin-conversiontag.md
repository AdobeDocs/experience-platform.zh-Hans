---
keywords: Awin广告商转化标记扩展；转化标记；Awin；AWIN
title: Awin广告商转化标记扩展
description: Awin广告商转化标记扩展是Adobe Experience Platform中的一个广告目标。 有关扩展功能的更多信息，请参阅Adobe Exchange上的扩展页面。
exl-id: 99feb169-acf3-4e68-8785-3f4cf565e5a9
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 3%

---

# Awin广告商转化标记扩展 {#awin-conversiontag-extension}

## 概述 {#overview}

转化标记是AWIN.Tracking.Sale JavaScript对象的声明，该声明在确认页面上完成，以指示Mastertag已发生转化。 然后，它将执行必要的跟踪请求。

Awin Advertiser Conversion Tag是Adobe Experience Platform中的一个广告扩展。 有关扩展功能的详细信息，请参阅[Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html)上的扩展页面。

此目标是标记扩展。 有关标记扩展如何在Platform中工作的更多信息，请参阅[标记扩展概述](../launch-extensions/overview.md)。

UI中的![Awin Advertiser Conversiontag扩展](../../assets/catalog/advertising/awin-conversion-tag/catalog.png)

## 先决条件 {#prerequisites}

所有购买了Platform的客户都可在“目标”目录中使用此扩展。

要使用此扩展，您需要具有对Platform中标记的访问权限。 标记以内置增值功能的方式提供给Adobe Experience Cloud客户。 请联系您的组织管理员，以获取UI中数据收集功能的访问权限，并要求他们向您授予&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您能够安装扩展。

## 安装扩展 {#install-extension}

要安装[!DNL Awin Advertiser Conversion Tag]扩展，请执行以下操作：

在[平台接口](https://platform.adobe.com/)中，转到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**。

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后在右边栏中选择&#x200B;**[!UICONTROL 配置]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控件呈灰显状态，则表示您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限。 请参阅[先决条件](#prerequisites)。

选择要安装扩展的标记属性。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。在[标记文档](../../../tags/ui/administration/companies-and-properties.md)中了解属性。

工作流会将您转到数据收集UI以完成安装。

有关扩展配置选项和安装支持的信息，请参阅Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html)上的[Awin Advertiser Conversion Tag页。

您还可以直接在[数据收集UI](https://experience.adobe.com/#/data-collection/)中安装该扩展。 有关详细信息，请参阅有关[添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)的指南。


## 如何使用扩展 {#how-to-use}

安装扩展后，您可以开始设置规则。 在数据收集UI中，您可以为已安装的扩展设置规则，以便仅在特定情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅标记文档中有关[规则](../../../tags/ui/managing-resources/rules.md)的概述。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果扩展已安装在您的某个资产上，则UI仍会显示该扩展的&#x200B;**[!UICONTROL Install]**。 按照[安装扩展](#install-extension)中的说明启动安装工作流，以配置或删除您的扩展。

要升级扩展，请参阅标记文档中的[扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)指南。
