---
keywords: Advertising Cloud；advertising cloud扩展；advertising cloud目标
title: Adobe Advertising Cloud扩展
description: Adobe Advertising Cloud扩展是Adobe Experience Platform中的一个广告目标。 有关扩展功能的更多信息，请参阅Adobe交换上的扩展页面。
exl-id: 3415a85f-5678-4f5b-b7cf-e185a66d084f
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 4%

---

# Adobe Advertising Cloud扩展 {#adobe-advertising-cloud-extension}

## 概述 {#overview}

这是 [!DNL Advertising Cloud] 用于实施的扩展 [!DNL Advertising Cloud] DSP和Search的转化和受众标记（当前不支持DCO）。

Adobe Advertising Cloud是Adobe Experience Platform中的一项广告扩展。

此目标是标记扩展。 有关标记扩展如何在Platform中工作的更多信息，请参阅 [标记扩展概述](../launch-extensions/overview.md).

![Adobe Advertising Cloud扩展](../../assets/catalog/advertising/adobe-advertising-cloud/catalog.png)

## 先决条件 {#prerequisites}

所有已购买Platform的客户都可以在“目标”目录中使用此扩展。

要使用此扩展，您需要访问Platform中的标记。 标记以内置增值功能的方式提供给Adobe Experience Cloud客户。 请联系您的组织管理员，以获取对UI中数据收集功能的访问权限，并请求他们授予您 **[!UICONTROL manage_properties]** 权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

安装Adobe Advertising Cloud扩展：

在 [平台界面](https://platform.adobe.com/)，转到 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**.

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后选择 **[!UICONTROL 配置]** 在右边栏中。 如果 **[!UICONTROL 配置]** 控件呈灰显状态，您缺少的是 **[!UICONTROL manage_properties]** 许可。 参见 [先决条件](#prerequisites).

选择要在其中安装扩展的标记属性。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解中的属性 [标记文档](../../../tags/ui/administration/companies-and-properties.md).

该工作流会将您转到数据收集UI以完成安装。

您还可以直接在中安装扩展 [数据收集UI](https://experience.adobe.com/#/data-collection/). 请参阅指南，网址为 [添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 了解更多信息。

## 如何使用扩展 {#how-to-use}

安装扩展后，即可开始设置规则。 在数据收集UI中，您可以为已安装的扩展设置规则，以便仅在特定情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅 [规则](../../../tags/ui/managing-resources/rules.md) 标记文档中的。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果某个资产上已安装该扩展，则仍会显示UI **[!UICONTROL 安装]** 作为扩展。 启动安装工作流，如中所述 [安装扩展](#install-extension) 以配置或删除扩展。

要升级扩展，请参阅 [扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 标记文档中的。
