---
keywords: target扩展；target；target v2；target v2扩展
title: Adobe Target v2扩展
description: Adobe Target v2扩展是Adobe Experience Platform中的个性化目标。 有关扩展功能的更多信息，请参阅Adobe Exchange上的扩展页面。
exl-id: d1d5ebbc-9093-42b0-8d88-58779df3ec89
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 4%

---

# [!DNL Adobe Target] v2扩展 {#adobe-target-v2-extension}

## 概述 {#overview}

[!DNL Adobe Target]是[!DNL Adobe Experience Cloud]解决方案，可为您提供定制和个性化客户体验所需的一切功能，从而最大限度地增加您的Web和移动设备网站、应用程序、社交媒体及其他数字渠道的收入。

[!DNL Adobe Target] v2是[!DNL Adobe Experience Platform]中的个性化扩展。 有关扩展功能的更多信息，请参阅[Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102722.adobe-target-v2-launch-extension.html)上的扩展页面。

此目标是标记扩展。 有关标记扩展如何在Experience Platform中工作的更多信息，请参阅[标记扩展概述](../launch-extensions/overview.md)。

![Adobe Target v2 扩展](../../assets/catalog/personalization/adobe-target-v2/catalog.png)

## 先决条件 {#prerequisites}

此扩展位于[!DNL Destinations]目录中，适用于已购买Experience Platform的所有客户。

要使用此扩展，您需要访问[!DNL Adobe Experience Platform]中的标记。 标记以内置增值功能的方式提供给[!DNL Adobe Experience Cloud]客户。 请联系您的组织管理员以获取对标记的访问权限，并要求他们授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您能够安装扩展。

## 安装扩展 {#install-extension}

要安装[!DNL Adobe Target] v2扩展：

在[Experience Platform界面](https://platform.adobe.com/)中，转到&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**。

从目录中选择扩展或使用搜索栏。

选择目标，然后在右边栏中选择&#x200B;**[!UICONTROL Configure]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控件呈灰显状态，则表示您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限。 请参阅[先决条件](#prerequisites)。

选择要安装扩展的资产。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。有关详细信息，请参阅标记文档中有关[属性](../../../tags/ui/administration/companies-and-properties.md#properties-page)的文档。

该工作流将指导您完成安装步骤。

有关扩展配置选项的信息，请参阅标记文档中的[Adobe Target v2扩展页面](../../../tags/extensions/client/target-v2/overview.md)。

您还可以直接在[数据收集UI](https://experience.adobe.com/#/data-collection/)中安装该扩展。 有关详细信息，请参阅有关[添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)的指南。


## 如何使用扩展 {#how-to-use}

安装扩展后，您可以开始设置规则。 在数据收集UI中，您可以为已安装的扩展设置规则，以便仅在特定情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅标记文档中有关[规则](../../../tags/ui/managing-resources/rules.md)的概述。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果某个资产上已安装该扩展，则对于该扩展，UI仍显示&#x200B;**[!UICONTROL Install]**。 按照[安装扩展](#install-extension)中的说明启动安装工作流，以配置或删除您的扩展。

要升级扩展，请参阅标记文档中的[扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)指南。
