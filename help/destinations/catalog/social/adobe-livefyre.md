---
keywords: livefyre；livefyre扩展
title: AdobeLivefyre扩展
description: AdobeLivefyre扩展是Adobe Experience Platform中的社交目标。 有关扩展功能的更多信息，请参阅Adobe交换上的扩展页面。
exl-id: a134c144-e7b8-4d48-8c90-5999e5ceb8a0
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 4%

---

# AdobeLivefyre扩展 {#adobe-livefyre-extension}

## 概述 {#overview}

通过AdobeLivefyre，您可以发现、整理用户生成的内容流并将其发布到您的网站，以创建真实且高度个性化的体验。

AdobeLivefyre是Adobe Experience Platform中的社交扩展。 有关AdobeLivefyre的更多信息，请参阅 [Livefyre实施指南](https://experienceleague.adobe.com/docs/livefyre/implementation/home.html).

此目标是标记扩展。 有关标记扩展如何在Platform中工作的更多信息，请参阅 [标记扩展概述](../launch-extensions/overview.md).

![AdobeLivefyre扩展](../../assets/catalog/social/adobe-livefyre/catalog.png)

## 先决条件 {#prerequisites}

此扩展位于 [!DNL Destinations] 适用于已购买Platform的所有客户的目录。

要使用此扩展，您需要具有对Adobe Experience Platform中标记的访问权限。 标记以内置增值功能的方式提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对标记的访问权限，并要求他们授予您 **[!UICONTROL manage_properties]** 权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

安装AdobeLivefyre扩展：

在 [平台界面](https://platform.adobe.com/)，转到 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**.

从目录中选择扩展或使用搜索栏。

单击目标将其突出显示，然后选择 **[!UICONTROL 配置]** 在右边栏中。 如果 **[!UICONTROL 配置]** 控件呈灰显状态，您缺少 **[!UICONTROL manage_properties]** 许可。 请参阅 [先决条件](#prerequisites).

选择要安装扩展的标记属性。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解中的属性 [标记文档](../../../tags/ui/administration/companies-and-properties.md).

工作流会将您转到数据收集UI以完成安装。

您还可以直接在中安装扩展 [数据收集UI](https://experience.adobe.com/#/data-collection/). 请参阅指南，网址为 [添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 以了解更多信息。

## 如何使用扩展 {#how-to-use}

安装扩展后，您可以开始设置规则。 在数据收集UI中，您可以为已安装的扩展设置规则，以便仅在特定情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅的概述 [规则](../../../tags/ui/managing-resources/rules.md) 标记文档中的。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果某个资产上已安装了扩展，则仍会显示UI **[!UICONTROL 安装]** 用于扩展。 启动安装工作流，如中所述 [安装扩展](#install-extension) 以配置或删除扩展。

要升级扩展，请参阅 [扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 标记文档中的。
