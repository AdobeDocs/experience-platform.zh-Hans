---
keywords: beemray，beemray扩展
title: Beemray扩展
description: Beemray扩展是Adobe Experience Platform中的个性化目标。 有关扩展功能的更多信息，请参阅Exchange上的扩展页面Adobe。
exl-id: 5bb639f5-42b5-48ae-a3e9-7585595ab925
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 3%

---

# [!DNL Beemray] 扩展 {#beemray-extension}

## 概述 {#overview}

[!DNL Beemray] 有助于您根据情景情境加快产品速度。使您能够获得洞察、构建新体验、推动交互并参与真正重要的时刻。 Beemray使用机器学习实现了情境智能自动化。 Beemray连接到Adobe Experience Cloud和您的其他技术合作伙伴。 一切都是实时进行的。 此扩展会在您的网站上安装[!DNL Beemray] SDK。

Beemray是Adobe Experience Platform中的一个个性化扩展。 有关扩展功能的更多信息，请参阅[AdobeExchange](https://exchange.adobe.com/experiencecloud.details.101063.beemray-human-context.html)上的扩展页面。

此目标是[!DNL Adobe Experience Platform Launch]扩展。 有关[!DNL Platform Launch]扩展如何在Platform中工作的更多信息，请参阅[Experience Platform Launch扩展概述](../launch-extensions/overview.md)。

![Beemray扩展](../../assets/catalog/personalization/beemray/catalog.png)

## 先决条件 {#prerequisites}

[!DNL Destinations]目录中提供了此扩展，可供已购买Platform的所有客户使用。

要使用此扩展，您需要访问[!DNL Adobe Experience Platform Launch]。 [!DNL Platform Launch] 以内置增值功能的形式提供给Adobe Experience Cloud客户。请联系您的组织管理员以获取[!DNL Platform Launch]的访问权限，并要求他们授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

要安装[!DNL Beemray]扩展，请执行以下操作：

在[Platform接口](http://platform.adobe.com/)中，转到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL Catalog]**。

从目录中选择扩展或使用搜索栏。

单击目标以将其突出显示，然后选择右边栏中的&#x200B;**[!UICONTROL 配置]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控件呈灰显状态，则您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;权限。 请参阅[先决条件](#prerequisites)。

在&#x200B;**[!UICONTROL 选择可用的Platform launch属性]**&#x200B;窗口中，选择要在其中安装扩展的[!DNL Platform Launch]属性。 您还可以选择在[!DNL Platform Launch]中创建新属性。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解[!DNL Launch]文档的[属性页面部分](../../../tags/ui/administration/companies-and-properties.md#properties-page)中的属性。

工作流会引导您完成[!DNL Platform Launch]安装。

有关扩展配置选项和安装支持的信息，请参阅AdobeExchange](https://exchange.adobe.com/experiencecloud.details.101063.beemray-human-context.html)上的[Beemray页面。

您还可以直接在[Adobe Experience Platform Launch界面](https://launch.adobe.com/)中安装该扩展。 请参阅[!DNL Platform Launch]文档中的[添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 。

## 如何使用扩展 {#how-to-use}

安装该扩展后，便可以直接在[!DNL Platform Launch]中为其设置规则。

在[!DNL Platform Launch]中，您可以为已安装的扩展设置规则，以便仅在某些情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅[规则文档](../../../tags/ui/managing-resources/rules.md)。

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在[!DNL Platform Launch]界面中配置、升级和删除扩展。

>[!TIP]
>
>如果您的某个资产上已安装扩展，则Platform UI仍会为该扩展显示&#x200B;**[!UICONTROL Install]**。 按照[Install extension](#install-extension)中所述启动安装工作流，以转到[!DNL Platform Launch]并配置或删除您的扩展。

要升级扩展，请参阅[!DNL Platform Launch]文档中的[扩展升级](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 。
