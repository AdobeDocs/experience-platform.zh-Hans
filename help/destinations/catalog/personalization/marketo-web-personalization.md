---
keywords: Marketo Web Personalization；marketo Web个性化；Marketo Web Personalization扩展；marketo Web个性化扩展；marketo；Marketo
title: Marketo Web Personalization扩展
description: Marketo Web Personalization扩展是Adobe Experience Platform中的个性化目标。 有关扩展功能的更多信息，请参阅Adobe Exchange上的扩展页面。
exl-id: 2f194a5e-13b7-460a-a968-29131771efca
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 3%

---

# [!DNL Marketo Web Personalization] 扩展 {#marketo-web-personalization-extension}

## 概述 {#overview}

此扩展为[!DNL Marketo's] Web Personalization和ContentAI应用程序部署脚本。 [!DNL Marketo] Web Personalization可唯一地根据Web访客特性标识和个性化内容，例如匿名访客的firmographics和[!DNL Marketo]参与平台中针对已知访客的各种行为属性。 [!DNL Marketo] ContentAI包含AI支持的推荐功能，以及针对B2B客户所独有的Web和电子邮件营销活动的个性化功能。

[!DNL Marketo Web Personalization]是Adobe Experience Platform中的个性化扩展。 有关Marketo中Web个性化和ContentAI的更多信息，请阅读[Web Personalization概述](https://experienceleague.adobe.com/docs/marketo/using/product-docs/web-personalization/understanding-web-personalization/web-personalization-overview.html?lang=zh-Hans)。

此目标是标记扩展。 有关标记扩展如何在Experience Platform中工作的更多信息，请参阅[标记扩展概述](../launch-extensions/overview.md)。

![Marketo Web Personalization扩展](../../assets/catalog/personalization/marketo-web-personalization/catalog.png)

## 先决条件 {#prerequisites}

此扩展位于[!DNL Destinations]目录中，适用于已购买Experience Platform的所有客户。

要使用此扩展，您需要具有对Adobe Experience Platform中标记的访问权限。 标记以内置增值功能的方式提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对标记的访问权限，并要求他们授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您能够安装扩展。

## 安装扩展 {#install-extension}

要安装[!DNL Marketo Web Personalization]扩展，请执行以下操作：

在[Experience Platform界面](https://platform.adobe.com/)中，转到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**。

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后在右边栏中选择&#x200B;**[!UICONTROL 配置]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控件呈灰显状态，则表示您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限。 请参阅[先决条件](#prerequisites)。

选择要安装扩展的资产。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。在标记文档的[属性页面](../../../tags/ui/administration/companies-and-properties.md#properties-page)部分中了解属性。

该工作流将指导您完成安装步骤。

您还可以直接在[数据收集UI](https://experience.adobe.com/#/data-collection/)中安装该扩展。 有关详细信息，请参阅标记文档中有关[添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)的部分。

## 如何使用扩展 {#how-to-use}

安装扩展后，您可以开始设置规则。

您可以为已安装的扩展设置规则，以便仅在特定情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅[标记文档](../../../tags/ui/managing-resources/rules.md)。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果某个资产上已安装该扩展，则Experience Platform UI仍会显示该扩展的&#x200B;**[!UICONTROL Install]**。 按照[安装扩展](#install-extension)中的说明启动安装工作流，以配置或删除您的扩展。

要升级扩展，请参阅标记文档中的[扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)指南。
