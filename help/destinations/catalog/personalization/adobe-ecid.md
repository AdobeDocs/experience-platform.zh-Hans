---
Keywords: ECID;ecid
title: Experience Cloud ID 服务扩展
description: Experience CloudID服务扩展是Adobe Experience Platform中的一个个性化目标。 有关扩展功能的更多信息，请参阅Exchange上的扩展页面Adobe。
exl-id: 4cc49c14-66ec-43e0-a106-70d9c3646d87
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 4%

---

# [!DNL Experience Cloud] ID服务扩展 {#adobe-ecid-extension}

## 概述 {#overview}

此扩展将实施 [!DNL Experience Cloud] ID服务，用于识别所有访客 [!DNL Experience Cloud] 解决方案。

[!DNL Experience Cloud] ID服务是Adobe Experience Platform中的一个个性化扩展。 有关扩展功能的更多信息，请参阅 [Experience CloudID服务扩展页面](../../../tags/extensions/client/id-service/overview.md) （位于标记文档中）。

此目标是一个标记扩展。 有关标记扩展在Platform中的工作方式的更多信息，请参阅 [标记扩展概述](../launch-extensions/overview.md).

![AdobeECID扩展](../../assets/catalog/personalization/adobe-ecid/catalog.png)

## 先决条件 {#prerequisites}

目标目录中提供的这项扩展适用于已购买平台的所有客户。

要使用此扩展，您需要访问Platform中的标记。 标记作为内置增值功能提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取数据收集UI的访问权限，并要求他们授予您 **[!UICONTROL manage_properties]** 权限，以便安装扩展。

## 安装扩展 {#install-extension}

安装 [!DNL Experience Cloud] ID服务扩展：

在 [平台界面](https://platform.adobe.com/)，转到 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**.

从目录中选择扩展或使用搜索栏。

单击目标以突出显示它，然后选择 **[!UICONTROL 配置]** 中。 如果 **[!UICONTROL 配置]** 控件呈灰显状态，表示您缺少 **[!UICONTROL manage_properties]** 权限。 请参阅 [先决条件](#prerequisites).

选择要在其中安装扩展的标记属性。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解 [标记文档](../../../tags/ui/administration/companies-and-properties.md).

利用工作流，可转到数据收集UI以完成安装。

有关扩展配置选项和安装支持的信息，请参阅 [Experience CloudID服务扩展页面](../../../tags/extensions/client/id-service/overview.md) （位于标记文档中）。

您还可以直接在 [数据收集UI](https://experience.adobe.com/#/data-collection/). 请参阅 [添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 以了解更多信息。

## 如何使用扩展 {#how-to-use}

安装扩展后，您可以开始设置规则。 在数据收集UI中，您可以为已安装的扩展设置规则，以便仅在某些情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅 [规则](../../../tags/ui/managing-resources/rules.md) （位于标记文档中）。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果某个资产上已安装扩展，则仍会显示UI **[!UICONTROL 安装]** 的子项。 启动安装工作流，如 [安装扩展](#install-extension) 配置或删除扩展。

要升级扩展，请参阅 [扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) （位于标记文档中）。
