---
keywords: bizible；bizible扩展；bizible目标
title: Bizible扩展
description: Bizible扩展是Adobe Experience Platform中的电子邮件目标。 有关扩展功能的更多信息，请参阅Adobe Exchange上的扩展页面。
exl-id: 9e45416d-b951-411c-a59f-34f84529f721
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 4%

---

# [!DNL Bizible] 扩展 {#bizible-extension}

## 概述 {#overview}

[!DNL Bizible]是行业领先的B2B归因解决方案，它让您能够无与伦比地查看您的数据，因此您可以做出有助于增长的明智决策。

[!DNL Bizible]是Adobe Experience Platform中的电子邮件扩展。 有关Bizible的详细信息，请阅读Bizible概述资源中的[营销归因](https://experienceleague.adobe.com/docs/bizible/using/introduction-to-bizible/overview-resources/marketing-attribution.html?lang=zh-Hans)。

此目标是标记扩展。 有关标记扩展如何在Experience Platform中工作的更多信息，请参阅[标记扩展概述](../launch-extensions/overview.md)。

![Bizible扩展](../../assets/catalog/email/bizible/catalog.png)

## 先决条件 {#prerequisites}

此扩展位于[!DNL Destinations]目录中，适用于已购买Experience Platform的所有客户。

要使用此扩展，您需要具有对Adobe Experience Platform中标记的访问权限。 标记以内置增值功能的方式提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对标记的访问权限，并要求他们授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您能够安装扩展。

## 安装扩展 {#install-extension}

要安装[!DNL Bizible]扩展，请执行以下操作：

在[Experience Platform界面](https://platform.adobe.com/)中，转到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**。

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后在右边栏中选择&#x200B;**[!UICONTROL 配置]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控件呈灰显状态，则表示您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限。 请参阅[先决条件](#prerequisites)。

选择要安装扩展的标记属性。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。在[标记文档](../../../tags/ui/administration/companies-and-properties.md)中了解属性。

工作流会将您转到数据收集UI以完成安装。

您还可以直接在[数据收集UI](https://experience.adobe.com/#/data-collection/)中安装该扩展。 有关详细信息，请参阅有关[添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)的指南。

## 如何使用扩展 {#how-to-use}

安装扩展后，您可以开始设置规则。 在数据收集UI中，您可以为已安装的扩展设置规则，以便仅在特定情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅标记文档中有关[规则](../../../tags/ui/managing-resources/rules.md)的概述。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果扩展已安装在您的某个资产上，则UI仍会显示该扩展的&#x200B;**[!UICONTROL Install]**。 按照[安装扩展](#install-extension)中的说明启动安装工作流，以配置或删除您的扩展。

要升级扩展，请参阅标记文档中的[扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)指南。
