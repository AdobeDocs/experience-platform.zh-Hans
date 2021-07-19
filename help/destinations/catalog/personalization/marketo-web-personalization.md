---
keywords: Marketo Web个性化；marketo Web个性化；Marketo Web个性化扩展；marketo Web个性化扩展；marketo;Marketo
title: Marketo Web个性化扩展
description: Marketo Web个性化扩展是Adobe Experience Platform中的一个个性化目标。 有关扩展功能的更多信息，请参阅Exchange上的扩展页面Adobe。
exl-id: 2f194a5e-13b7-460a-a968-29131771efca
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 3%

---

# [!DNL Marketo Web Personalization] 扩展 {#marketo-web-personalization-extension}

## 概述 {#overview}

此扩展将部署[!DNL Marketo’s] Web个性化和ContentAI应用程序的脚本。 [!DNL Marketo] Web个性化可唯一地识别内容并将其个性化为Web访客特征，例如匿名访客的Firmagraphics和已知访客的参与平台中的 [!DNL Marketo] 一系列行为属性。[!DNL Marketo] ContentAI包含针对B2B客户独有的Web和电子邮件促销活动的AI支持的推荐和个性化功能。

[!DNL Marketo Web Personalization] 是Adobe Experience Platform中的一个个性化扩展。有关扩展功能的更多信息，请参阅[AdobeExchange](https://exchange.adobe.com/experiencecloud.details.101232.marketo-web-personalization.html)上的扩展页面。

此目标是Adobe Experience Platform Launch扩展。 有关Platform launch扩展如何在Platform中工作的更多信息，请参阅[Adobe Experience Platform Launch扩展概述](../launch-extensions/overview.md)。

![Marketo Web个性化扩展](../../assets/catalog/personalization/marketo-web-personalization/catalog.png)

## 先决条件 {#prerequisites}

[!DNL Destinations]目录中提供了此扩展，可供已购买Platform的所有客户使用。

要使用此扩展，您需要访问Adobe Experience Platform Launch。 platform launch以内置增值功能的形式提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取Platform launch的访问权限，并要求他们授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

要安装[!DNL Marketo Web Personalization]扩展，请执行以下操作：

在[Platform接口](http://platform.adobe.com/)中，转到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL Catalog]**。

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后选择右边栏中的&#x200B;**[!UICONTROL 配置]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控件呈灰显状态，则您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限。 请参阅[先决条件](#prerequisites)。

在&#x200B;**[!UICONTROL 选择可用的Platform launch属性]**&#x200B;窗口中，选择要在其中安装扩展的Platform launch属性。 您还可以选择在Platform launch中创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解Platform launch文档[属性页面部分](../../../tags/ui/administration/companies-and-properties.md#properties-page)中的属性。

利用工作流，可Platform launch完成安装。

有关扩展配置选项和安装支持的信息，请参阅AdobeExchange](https://exchange.adobe.com/experiencecloud.details.101232.marketo-web-personalization.html)上的[Marketo Web个性化页面。

您还可以直接在[Adobe Experience Platform Launch界面](https://launch.adobe.com/)中安装该扩展。 请参阅Platform launch文档中的[添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 。

## 如何使用扩展 {#how-to-use}

安装扩展后，您可以直接在Platform launch中为其设置规则。

在Platform launch中，您可以为已安装的扩展设置规则，以便仅在某些情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅[规则文档](../../../tags/ui/managing-resources/rules.md)。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在Platform launch界面中配置、升级和删除扩展。

>[!TIP]
>
>如果您的某个资产上已安装扩展，则Platform UI仍会为该扩展显示&#x200B;**[!UICONTROL Install]**。 按照[Install extension](#install-extension)中所述启动安装工作流，以开始Platform launch并配置或删除您的扩展。

要升级扩展，请参阅Platform launch文档中的[扩展升级](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 。
