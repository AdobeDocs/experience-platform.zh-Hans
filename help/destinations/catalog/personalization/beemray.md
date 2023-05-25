---
keywords: beemray扩展
title: Beemray扩展
description: Beemray扩展是Adobe Experience Platform中的个性化目标。 有关扩展功能的更多信息，请参阅Adobe交换上的扩展页面。
exl-id: 5bb639f5-42b5-48ae-a3e9-7585595ab925
source-git-commit: c8d6c156b3351324fe1be11144afeae91f7a2a59
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 3%

---

# [!DNL Beemray] 扩展 {#beemray-extension}

## 概述 {#overview}

[!DNL Beemray] 帮助您根据情境来加快产品速度。 使您能够获得见解、构建新体验、推动交互并参与真正重要的时刻。 Beemray使用机器学习实现情境智能自动化。 Beemray可连接到Adobe Experience Cloud和您的其他技术合作伙伴。 所有事情都实时发生。 此扩展将安装 [!DNL Beemray] 您网站上的SDK。

Beemray是Adobe Experience Platform中的个性化扩展。 有关扩展功能的更多信息，请参阅上的扩展页面 [Adobe交换](https://exchange.adobe.com/experiencecloud.details.101063.beemray-human-context.html).

此目标是标记扩展。 有关标记扩展如何在Platform中工作的更多信息，请参阅 [标记扩展概述](../launch-extensions/overview.md).

![Beemray扩展](../../assets/catalog/personalization/beemray/catalog.png)

## 先决条件 {#prerequisites}

此扩展位于 [!DNL Destinations] 适用于已购买Platform的所有客户的目录。

要使用此扩展，您需要访问Adobe Experience Platform中的标记。 标记以内置增值功能的方式提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对标记的访问权限，并要求他们授予您 **[!UICONTROL manage_properties]** 权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

安装 [!DNL Beemray] 扩展名：

在 [平台界面](https://platform.adobe.com/)，转到 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**.

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后选择 **[!UICONTROL 配置]** 在右边栏中。 如果 **[!UICONTROL 配置]** 控件呈灰显状态，您缺少的是 **[!UICONTROL manage_properties]** 许可。 参见 [先决条件](#prerequisites).

选择要在其中安装扩展的标记属性。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解中的属性 [标记文档](../../../tags/ui/administration/companies-and-properties.md).

该工作流会将您转到数据收集UI以完成安装。

有关扩展配置选项和安装支持的信息，请参阅 [Adobe交换上的Beemray页](https://exchange.adobe.com/experiencecloud.details.101063.beemray-human-context.html).

您还可以直接在中安装扩展 [数据收集UI](https://experience.adobe.com/#/data-collection/). 请参阅指南，网址为 [添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 了解更多信息。

## 如何使用扩展 {#how-to-use}

安装扩展后，即可开始设置规则。 在数据收集UI中，您可以为已安装的扩展设置规则，以便仅在特定情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅 [规则](../../../tags/ui/managing-resources/rules.md) 标记文档中的。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果某个资产上已安装该扩展，则仍会显示UI **[!UICONTROL 安装]** 作为扩展。 启动安装工作流，如中所述 [安装扩展](#install-extension) 以配置或删除扩展。

要升级扩展，请参阅 [扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 标记文档中的。
