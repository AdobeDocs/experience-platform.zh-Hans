---
keywords: InMoment；inmoment；Inmoment；Launch集成
title: InMoment扩展
description: InMoment扩展是Adobe Experience Platform中的一个调查目标。 有关扩展功能的更多信息，请参阅Adobe交换上的扩展页面。
exl-id: 61f32bc1-97a6-45ff-a962-990a2e522735
source-git-commit: b4e869f9bc29122db4fc66ccda752a50c7db729f
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 5%

---

# [!DNL InMoment] 扩展 {#inmoment-extension}

## 概述 {#overview}

此 [!DNL InMoment] 标记扩展允许您通过Digital Intercept产品快速轻松地启用在线反馈。 在该应用程序中，可以通过CXI Cloud Admin配置和管理截获，从而让CX经理能够更好地控制其程序。

[!DNL InMoment] 是Adobe Experience Platform中的调查扩展。 有关扩展功能的更多信息，请参阅上的扩展页面 [Adobe交换](https://exchange.adobe.com/experiencecloud.details.100847.html).

此目标是标记扩展。 有关标记扩展如何在Platform中工作的更多信息，请参阅 [标记扩展概述](../launch-extensions/overview.md).

![即时扩展](../../assets/catalog/survey/inmoment/catalog.png)

## 先决条件 {#prerequisites}

此扩展位于 [!DNL Destinations] 适用于已购买Platform的所有客户的目录。

要使用此扩展，您需要访问Adobe Experience Platform中的标记。 标记以内置增值功能的方式提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对标记的访问权限，并要求他们授予您 **[!UICONTROL manage_properties]** 权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

安装 [!DNL InMoment] 扩展名：

在 [平台界面](https://platform.adobe.com/)，转到 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**.

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后选择 **[!UICONTROL 配置]** 在右边栏中。 如果 **[!UICONTROL 配置]** 控件呈灰显状态，您缺少的是 **[!UICONTROL manage_properties]** 许可。 参见 [先决条件](#prerequisites).

选择要安装扩展的资产。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解中的属性 [“属性”页部分](../../../tags/ui/administration/companies-and-properties.md#properties-page) ，位于标记文档中的。

该工作流将引导您完成安装步骤。

有关扩展配置选项的信息，请参见 [Google Universal Analytics扩展页面](https://exchange.adobe.com/experiencecloud.details.100847.html) 在Adobe交换上。

您还可以直接在中安装扩展 [数据收集UI](https://experience.adobe.com/#/data-collection/). 有关更多信息，请参阅以下部分： [添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 标记文档中的。


## 如何使用扩展 {#how-to-use}

安装扩展后，即可开始设置规则。

您可以为已安装的扩展设置规则，以便仅在特定情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅 [标记文档](../../../tags/ui/managing-resources/rules.md).

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果某个资产上已安装该扩展，则仍会显示平台UI **[!UICONTROL 安装]** 作为扩展。 启动安装工作流，如中所述 [安装扩展](#install-extension) 以配置或删除扩展。

要升级扩展，请参阅 [扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 标记文档中的。
