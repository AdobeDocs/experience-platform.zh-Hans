---
keywords: Audience ManagerDIL扩展；目标audience manager；dil扩展
title: Audience ManagerDIL扩展
description: Audience ManagerDIL扩展是Adobe Experience Platform中的数据管理平台(DMP)目标。 有关扩展功能的更多信息，请参阅Adobe交换上的扩展页面。
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# Audience ManagerDIL扩展 {#aam-dil-extension}

## 概述 {#overview}

这是Adobe Audience ManagerData Integration Library扩展（客户端实施）。 注意：此扩展不适用于Adobe Analytics数据的服务器端转发(SSF)。 对于SSF，请使用Adobe Analytics扩展。 重要信息：从版本8.0开始，DIL对 [!DNL Experience Cloud] ID服务版本3.3或更高版本。 请同时实施两者 [!DNL Experience Cloud] ID服务和DIL（完整） [!DNL Audience Manager] 数据集成功能。

[!DNL Audience Manager] DIL是Adobe Experience Platform中的数据管理平台(DMP)扩展。 有关扩展功能的更多信息，请参阅 [“Audience Manager扩展”页](../../../tags/extensions/client/audience-manager/overview.md) 标记文档中的。

此目标是标记扩展。 有关扩展如何在Platform中工作的更多信息，请参阅 [标记扩展概述](../launch-extensions/overview.md).

![Audience ManagerDIL扩展](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## 先决条件 {#prerequisites}

此扩展位于 [!DNL Destinations] 适用于已购买Platform的所有客户的目录。

要使用此扩展，您需要访问Adobe Experience Platform中的标记。 标记以内置增值功能的方式提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对标记的访问权限，并要求他们授予您 **[!UICONTROL manage_properties]** 权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

安装 [!DNL Audience Manager] DIL扩展：

在 [平台界面](https://platform.adobe.com/)，转到 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**.

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后选择 **[!UICONTROL 配置]** 在右边栏中。 如果 **[!UICONTROL 配置]** 控件呈灰显状态，您缺少的是 **[!UICONTROL manage_properties]** 许可。 参见 [先决条件](#prerequisites).

选择要安装扩展的资产。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解中的属性 [标记文档](../../../tags/ui/administration/companies-and-properties.md#properties-page).

该工作流将引导您完成安装步骤。

有关扩展配置选项的信息，请参见 [“Audience Manager扩展”页](../../../tags/extensions/client/audience-manager/overview.md) 标记文档中的。

您还可以直接在中安装扩展 [数据收集UI](https://experience.adobe.com/#/data-collection/). 请参阅指南，网址为 [添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 了解更多信息。

## 如何使用扩展 {#how-to-use}

安装扩展后，即可开始设置规则。 在数据收集UI中，您可以为已安装的扩展设置规则，以便仅在特定情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅 [规则](../../../tags/ui/managing-resources/rules.md) 标记文档中的。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果某个资产上已安装该扩展，则仍会显示UI **[!UICONTROL 安装]** 作为扩展。 启动安装工作流，如中所述 [安装扩展](#install-extension) 以配置或删除扩展。

要升级扩展，请参阅 [扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 标记文档中的。
