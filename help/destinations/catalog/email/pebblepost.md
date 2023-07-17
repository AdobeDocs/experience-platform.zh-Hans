---
keywords: PebblePost；pebblepost；PebblePost程序化直邮；pebblepost程序化直邮
title: PebblePost扩展
description: PebblePost扩展是Adobe Experience Platform中的电子邮件目标。 有关扩展功能的更多信息，请参阅Adobe交换上的扩展页面。
exl-id: 2d0308db-9d75-4cd1-97de-70ce3837369d
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 4%

---

# [!DNL PebblePost] 扩展 {#pebblepost-extension}

## 概述 {#overview}

[!DNL PebblePost's Programmatic Direct Mail®] 解决方案可帮助数字营销人员将在线兴趣和意图与可转化的线下、有形媒体联系起来。 营销人员现在可以利用他们在Adobe中创建的自定义数据受众，通过相关、更持久的、在家中传播的媒体印象来定位消费者。 根据响应路径活动和现场转化实时分析性能。

[!DNL PebblePost] 是Adobe Experience Platform中的电子邮件扩展。 有关PebblePost的更多信息，请阅读 [集成博客帖子](https://blog.adobe.com/en/publish/2017/11/16/pebblepost-builds-integration-launch-adobe.html#gs.7lejiq).

此目标是标记扩展。 有关标记扩展如何在Platform中工作的更多信息，请参阅 [标记扩展概述](../launch-extensions/overview.md).

![PebblePost扩展](../../assets/catalog/email/pebblepost/catalog.png)

## 先决条件 {#prerequisites}

此扩展位于 [!DNL Destinations] 适用于已购买Platform的所有客户的目录。

要使用此扩展，您需要访问Adobe Experience Platform中的标记。 标记以内置增值功能的方式提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对标记的访问权限，并要求他们授予您 **[!UICONTROL manage_properties]** 权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

安装 [!DNL PebblePost] 扩展名：

在 [平台界面](https://platform.adobe.com/)，转到 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**.

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后选择 **[!UICONTROL 配置]** 在右边栏中。 如果 **[!UICONTROL 配置]** 控件呈灰显状态，您缺少的是 **[!UICONTROL manage_properties]** 许可。 参见 [先决条件](#prerequisites).

选择要安装扩展的资产。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解中的属性 [“属性”页部分](../../../tags/ui/administration/companies-and-properties.md#properties-page) ，位于标记文档中的。

该工作流将引导您完成安装步骤。

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
