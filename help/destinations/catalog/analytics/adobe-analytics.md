---
keywords: Analytics扩展；Analytics扩展；目标分析
title: Adobe Analytics 扩展
description: Adobe Analytics扩展是Adobe Experience Platform中的一个分析目标。 有关扩展功能的更多信息，请参阅Exchange上的扩展页面Adobe。
exl-id: 95b6e079-09a6-4262-bd01-11f155286aa9
source-git-commit: 468b9309c5184684c0b25c2656a9eef37715af53
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 9%

---

# Adobe Analytics 扩展

## 概述 {#overview}

Adobe Analytics 是一款行业领先的解决方案，可帮助您充分了解客户的行为和需求，并根据客户情报掌控自己的业务发展方向。

Adobe Analytics是Adobe Experience Platform中的一项analytics扩展。 有关扩展功能的更多信息，请参阅 [Adobe Analytics扩展概述](/help/tags/extensions/web/analytics/overview.md) （位于标记文档中）。

此目标是一个标记扩展。 有关标记扩展在Platform中的工作方式的更多信息，请参阅 [标记扩展概述](../launch-extensions/overview.md).

![Adobe Analytics 扩展](../../assets/catalog/analytics/adobe-analytics/catalog.png)

## 先决条件 {#prerequisites}

目标目录中提供的这项扩展适用于已购买平台的所有客户。

要使用此扩展，您需要访问Platform中的标记。 标记作为内置增值功能提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取数据收集UI的访问权限，并要求他们授予您 **[!UICONTROL manage_properties]** 权限，以便安装扩展。

## 安装扩展 {#install-extension}

要安装Adobe Analytics扩展，请执行以下操作：

在 [平台界面](https://platform.adobe.com/)，转到 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**.

从目录中选择扩展或使用搜索栏。

单击目标以突出显示它，然后选择 **[!UICONTROL 配置]** 中。 如果 **[!UICONTROL 配置]** 控件呈灰显状态，表示您缺少 **[!UICONTROL manage_properties]** 权限。 请参阅 [先决条件](#prerequisites).

选择要在其中安装扩展的标记属性。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解 [标记文档](../../../tags/ui/administration/companies-and-properties.md).

利用工作流，可转到数据收集UI以完成安装。

有关扩展配置选项的信息，请参阅 [Adobe Analytics扩展页面](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/implement-solutions/analytics.html) 标记文档。

您还可以直接在 [数据收集UI](https://experience.adobe.com/#/data-collection/). 请参阅 [添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 以了解更多信息。

## 如何使用扩展 {#how-to-use}

安装扩展后，您可以开始设置规则。 在数据收集UI中，您可以为已安装的扩展设置规则，以便仅在某些情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅 [规则](../../../tags/ui/managing-resources/rules.md) （位于标记文档中）。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果某个资产上已安装扩展，则仍会显示UI **[!UICONTROL 安装]** 的子项。 启动安装工作流，如 [安装扩展](#install-extension) 配置或删除扩展。

要升级扩展，请参阅 [扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) （位于标记文档中）。
