---
keywords: Audience ManagerDIL扩展；目标受众管理器；dil扩展
title: Audience ManagerDIL扩展
description: Audience ManagerDIL扩展是Adobe Experience Platform中的数据管理平台(DMP)目标。 有关扩展功能的详细信息，请参阅Adobe Exchange上的扩展页。
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 3%

---


# Audience ManagerDIL扩展{#aam-dil-extension}

## 概述 {#overview}

这是Adobe Audience Manager Data Integration Library扩展（客户端实现）。 注意：此扩展不用于Adobe Analytics数据的服务器端转发(SSF)。 对于SSF，请使用Adobe Analytics扩展。 重要说明：从8.0版开始，DIL对[!DNL Experience Cloud] ID服务3.3版或更高版本具有硬依赖性。 请实现[!DNL Experience Cloud] ID服务和DIL，以获得完整的[!DNL Audience Manager]数据集成功能。

[!DNL Audience Manager] DIL是Adobe Experience Platform中的一个数据管理平台(DMP)扩展。有关扩展功能的详细信息，请参阅Audience Manager文档中的[Experience Platform Launch扩展页面](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html)。

此目标是[!DNL Experience Platform Launch]扩展。 有关Launch扩展在平台中的工作方式的详细信息，请参阅[Experience Platform Launch扩展概述](../launch-extensions/overview.md)。

![Audience ManagerDIL扩展](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## 先决条件 {#prerequisites}

此扩展位于[!DNL Destinations]目录中，可用于所有已购买平台的客户。

要使用此扩展，您需要访问[!DNL Adobe Experience Platform Launch]。 [!DNL Platform Launch] 作为附带的增值功能提供给Adobe Experience Cloud客户。请联系您的组织管理员获取对[!DNL Platform Launch]的访问权限并要求他们授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您可以安装扩展。

## 安装扩展{#install-extension}

安装[!DNL Audience Manager]DIL扩展：

在[平台接口](http://platform.adobe.com/)中，转到&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**。

从目录中选择扩展或使用搜索栏。

单击目标以突出显示它，然后在右边栏中选择&#x200B;**[!UICONTROL Configure]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控件灰显，则您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限。 请参阅[先决条件](#prerequisites)。

在&#x200B;**[!UICONTROL Select available Launch property]**&#x200B;窗口中，选择要安装扩展的[!DNL Launch]属性。 您还可以选择在启动项中创建新属性。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解[!DNL Launch]文档的[属性页面部分](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page)中的属性。

该工作流将引导您完成[!DNL Launch]安装。

有关扩展配置选项的信息，请参阅[!DNL Experience Launch]文档中的[Audience Manager扩展页面](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html)。

您还可以直接在[Adobe Experience Platform Launch接口](https://launch.adobe.com/)中安装扩展。 请参阅[!DNL Platform Launch]文档中的[添加新扩展](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension)。

## 如何使用扩展{#how-to-use}

安装扩展后，可以直接在[!DNL Platform Launch]中开始为它设置规则。

在[!DNL Platform Launch]中，您可以设置已安装扩展的规则，以便仅在某些情况下才将事件数据发送到扩展目标。 有关设置扩展规则的详细信息，请参阅[规则文档](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)。

## 配置、升级和删除扩展{#configure-upgrade-delete}

您可以在[!DNL Platform Launch]接口中配置、升级和删除扩展。

>[!TIP]
>
>如果某个属性上已安装该扩展，则平台UI仍会显示该扩展的&#x200B;**[!UICONTROL Install]**。 启动安装工作流，如[安装扩展](#install-extension)中所述，以访问[!DNL Platform Launch]并配置或删除您的扩展。

要升级您的扩展，请参阅[!DNL Platform Launch]文档中的[扩展升级](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html)。



