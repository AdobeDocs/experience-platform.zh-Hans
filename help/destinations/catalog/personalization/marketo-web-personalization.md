---
keywords: Marketo Web个性化；marketo Web个性化；Marketo Web个性化扩展；marketo Web个性化扩展；marketo；Marketo
title: Marketo Web Personalization扩展
description: Marketo Web Personalization扩展是Adobe Experience Platform中的个性化目标。 有关扩展功能的更多信息，请参阅Adobe交换上的扩展页面。
exl-id: 2f194a5e-13b7-460a-a968-29131771efca
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 4%

---

# [!DNL Marketo Web Personalization] 扩展 {#marketo-web-personalization-extension}

## 概述 {#overview}

此扩展部署脚本 [!DNL Marketo's] Web个性化和内容人工智能应用程序。 [!DNL Marketo] Web个性化可根据Web访客特征唯一地标识和个性化内容，例如匿名访客的作品集和 [!DNL Marketo] 面向已知访客的参与平台。 [!DNL Marketo] ContentAI包含由AI提供支持的推荐功能，以及针对B2B客户所独有的Web和电子邮件营销活动的个性化功能。

[!DNL Marketo Web Personalization] 是Adobe Experience Platform中的个性化扩展。 有关Marketo中Web个性化和ContentAI的更多信息，请阅读 [Web个性化概述](https://experienceleague.adobe.com/docs/marketo/using/product-docs/web-personalization/understanding-web-personalization/web-personalization-overview.html).

此目标是标记扩展。 有关标记扩展如何在Platform中工作的更多信息，请参阅 [标记扩展概述](../launch-extensions/overview.md).

![Marketo Web Personalization扩展](../../assets/catalog/personalization/marketo-web-personalization/catalog.png)

## 先决条件 {#prerequisites}

此扩展位于 [!DNL Destinations] 适用于已购买Platform的所有客户的目录。

要使用此扩展，您需要具有对Adobe Experience Platform中标记的访问权限。 标记以内置增值功能的方式提供给Adobe Experience Cloud客户。 请联系您的组织管理员以获取对标记的访问权限，并要求他们授予您 **[!UICONTROL manage_properties]** 权限，以便您可以安装扩展。

## 安装扩展 {#install-extension}

安装 [!DNL Marketo Web Personalization] 扩展名：

在 [平台界面](https://platform.adobe.com/)，转到 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**.

从目录中选择扩展或使用搜索栏。

单击目标将其突出显示，然后选择 **[!UICONTROL 配置]** 在右边栏中。 如果 **[!UICONTROL 配置]** 控件呈灰显状态，您缺少 **[!UICONTROL manage_properties]** 许可。 请参阅 [先决条件](#prerequisites).

选择要安装扩展的资产。 您还可以选择创建新资产。 资产是规则、数据元素、配置的扩展、环境和库的集合。了解中的属性 [“属性”页面部分](../../../tags/ui/administration/companies-and-properties.md#properties-page) ，在标记文档中。

该工作流将指导您完成安装步骤。

您还可以直接在中安装扩展 [数据收集UI](https://experience.adobe.com/#/data-collection/). 有关更多信息，请参阅以下部分： [添加新扩展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 标记文档中的。

## 如何使用扩展 {#how-to-use}

安装扩展后，您可以开始设置规则。

您可以为已安装的扩展设置规则，以便仅在特定情况下将事件数据发送到扩展目标。 有关为扩展设置规则的更多信息，请参阅 [标记文档](../../../tags/ui/managing-resources/rules.md).

## 配置、升级和删除扩展 {#configure-upgrade-delete}

您可以在数据收集UI中配置、升级和删除扩展。

>[!TIP]
>
>如果某个资产上已安装了扩展，则仍会显示平台UI **[!UICONTROL 安装]** 用于扩展。 启动安装工作流，如中所述 [安装扩展](#install-extension) 以配置或删除扩展。

要升级扩展，请参阅 [扩展升级过程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 标记文档中的。
