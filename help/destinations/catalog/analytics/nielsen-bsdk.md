---
keywords: Nielsen BSDK；nielsen BSDK；nielsen BSDK
title: Nielsen BSDK扩展
description: Nielsen BSDK扩展是Adobe Experience Platform中的分析目标。 有关扩展功能的更多信息，请参阅Adobe交换上的扩展页面。
exl-id: e1c10673-e3f4-474d-98d7-960124b2bfc7
source-git-commit: b4e869f9bc29122db4fc66ccda752a50c7db729f
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 4%

---

# [!DNL Nielsen BSDK] 扩展 {#nielsen-bsdk-extension}

## 概述 {#overview}

[!DNL Nielsen Digital SDK] 标记扩展通过下列数字测量产品提供受众测量：

DCR：一种提供非线性数字内容（包括广告内容）每日测量的测量解决方案，可全面了解台式机、移动设备、平板电脑和联网设备中的数字内容受众使用情况。

DTVR：这适用于在桌面和移动设备上发生的用于参与节目源的线性电视观看。 这是第一个获得美国电影版权委员会认证的解决方案，以表彰其在电视观众评量方面做出的贡献，这些评量的内容是通过计算机和移动设备观看的节目。

[!DNL Nielsen BSDK] 是Adobe Experience Platform中的一个analytics扩展。 有关扩展功能的更多信息，请参阅上的扩展页面 [Adobe交换](https://exchange.adobe.com/experiencecloud.details.101361.html).

此目标是标记扩展。 有关标记扩展如何在Platform中工作的更多信息，请参阅 [标记扩展概述](../launch-extensions/overview.md).

![Nielsen BSDK扩展](../../assets/catalog/analytics/nielsen-bsdk/catalog.png)

## 先决条件 {#prerequisites}

此扩展位于 [!DNL Destinations] 适用于已购买Platform的所有客户的目录。

要使用此扩展，您需要访问Adobe Experience Platform中的标记。 标记以内置增值功能的方式提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对标记的访问权限，并要求他们授予您 **[!UICONTROL manage_properties]** 权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

安装 [!DNL Nielsen BSDK] 扩展名：

在 [平台界面](https://platform.adobe.com/)，转到 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**.

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后选择 **[!UICONTROL 配置]** 在右边栏中。 如果 **[!UICONTROL 配置]** 控件呈灰显状态，您缺少的是 **[!UICONTROL manage_properties]** 许可。 参见 [先决条件](#prerequisites).

选择要安装扩展的资产。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解中的属性 [“属性”页部分](../../../tags/ui/administration/companies-and-properties.md#properties-page) ，位于标记文档中的。

该工作流将引导您完成安装步骤。

有关扩展配置选项和安装支持的信息，请参阅 [Adobe交换上的Nielsen BSDK页面](https://exchange.adobe.com/experiencecloud.details.101361.html).

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
