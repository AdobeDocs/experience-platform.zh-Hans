---
keywords: GTAG;Google Gtag;Google扩展；Google Gtag扩展；GTAG
title: Google扩展
description: Google gtag扩展是Adobe Experience Platform中的一个广告目的地。 有关扩展功能的更多信息，请参阅Exchange上的扩展页面Adobe。
exl-id: 14a466f2-78a0-4493-93cd-3dcdae048042
source-git-commit: c3f6650df5fabe9736e4b11a43c41ae39f014425
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 3%

---

# Google扩展 {#gtag-advertising-extension}

>[!IMPORTANT]
>
>此处介绍的Google gtag扩展已弃用，并由 [[!DNL Google Global Site Tag (gtag)]](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) 扩展由 [!DNL Acronym]. 您可以在 [!DNL Google Global Site Tag (gtag)] 扩展 [[!UICONTROL 标记]](../../../tags/home.md) 工作区。

## 概述 {#overview}

加载Google `gtag.js` 将事件数据发送到您的网站 [!DNL Google Analytics]、Google Ads和 [!DNL Google Marketing Platform]. 此扩展仅会将标记代码添加到您的网站。 您将需要使用其他Google扩展来添加将使用gtag的事件和操作。

Google gtag是Adobe Experience Platform中的一项广告扩展。 有关扩展功能的更多信息，请参阅 [Adobe交换](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

此目标是一个标记扩展。 有关标记扩展在Platform中工作方式的更多信息，请参阅 [标记扩展概述](../launch-extensions/overview.md).

![Google扩展](../../assets/catalog/advertising/gtag-advertising/catalog.png)

## 先决条件 {#prerequisites}

此扩展位于 [!DNL Destinations] 目录。

要使用此扩展，您需要访问Adobe Experience Platform中的标记。 标记作为内置增值功能提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对标记的访问权限，并要求他们向您授予 **[!UICONTROL manage_properties]** 权限，以便安装扩展。

## 安装扩展 {#install-extension}

要安装Google gtag扩展，请执行以下操作：

在 [平台界面](https://platform.adobe.com/)，转到 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**.

从目录中选择扩展或使用搜索栏。

单击目标以突出显示它，然后选择 **[!UICONTROL 配置]** 中。 如果 **[!UICONTROL 配置]** 控件呈灰显状态，表示您缺少 **[!UICONTROL manage_properties]** 权限。 请参阅 [先决条件](#prerequisites).

选择要在其中安装扩展的资产。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解 [“属性”页面部分](../../../tags/ui/administration/companies-and-properties.md#properties-page) 的。

工作流可指导您完成完成安装的步骤。

有关扩展配置选项和安装支持的信息，请参阅 [GoogleAdobeExchange上的gtag页面](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

您还可以直接在 [数据收集UI](https://experience.adobe.com/#/data-collection/). 有关更多信息，请参阅 [添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) （位于标记文档中）。

## 如何使用扩展 {#how-to-use}

安装扩展后，您可以开始设置规则。

您可以为已安装的扩展设置规则，以便仅在某些情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅 [标记文档](../../../tags/ui/managing-resources/rules.md).

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果您的其中一个资产上已安装扩展，则仍会显示Platform UI **[!UICONTROL 安装]** 的子项。 启动安装工作流，如 [安装扩展](#install-extension) 配置或删除扩展。

要升级扩展，请参阅 [扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) （位于标记文档中）。
