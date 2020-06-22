---
title: Google Ad Manager目标
seo-title: Google Ad Manager目标
description: 'Google Ad Manager以前称为DoubleClick for Publishers或DoubleClick AdX，是Google的广告服务平台，它使出版商能够通过视频和移动应用程序管理其网站上广告的显示。 '
seo-description: 'Google Ad Manager以前称为DoubleClick for Publishers或DoubleClick AdX，是Google的广告服务平台，它使出版商能够通过视频和移动应用程序管理其网站上广告的显示。 '
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---


# Google Ad Manager目标

## 概述

Google Ad Manager以前称为DoubleClick for Publishers或DoubleClick AdX，是Google的广告服务平台，它使出版商能够通过视频和移动应用程序管理其网站上广告的显示。

## 目标规范

请注意Google Ad Manager目标的以下详细信息：

* 您可以将以下身份 [发送](../../identity-service/namespaces.md) 到Google Ad Manager目标： **Google Cookie ID、IDFA、GAID、Roku ID、Microsoft ID、Amazon Fire TV ID**。
* 激活的受众是在Google平台中以编程方式创建的。
* Adobe实时CDP当前不包含用于验证成功激活的度量。 请参阅Google中的受众计数，验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望使用Google Ad Manager创建您的第一个目标，并且过去(使用 [Experience Cloud或其他应用程序](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) )未在Audience ManagerID服务中启用ID同步功能，请联系Adobe Consulting或客户关怀以启用ID同步。 如果您以前在Audience Manager中设置Google集成，则您设置的ID同步将结转到Adobe实时CDP。

## 先决条件

### 允许列表

>[!NOTE]
>
>在Adobe实时CDP中设置您的第一个Google Ad Manager目标之前，允许列表是必填的。 在创建目标之前，请确保Google已完成下面描述的允许列表过程。

在Adobe实时CDP中创建Google Ad Manager目标之前，您必须联系Google，让Adobe进入允许数据提供商的列表，并将您的帐户添加到允许列表。 联系Google并提供以下信息：

* **帐户ID** : 这是Adobe在Google上的帐户ID。 要获取此ID，请与Adobe客户服务或Adobe代表联系。
* **客户ID** : 这是Adobe在Google上的客户帐户ID。 要获取此ID，请与Adobe客户服务或Adobe代表联系。
* **网络ID** : 这是您在Google Ad Manager上的帐户
* **受众链接ID** : 这是您在Google Ad Manager上的帐户
* 您的帐户类型。 **Google或AdX** 购 **买者的DFP**。

## 创建目标

1. 在“ **[!UICONTROL 连接”>“目标]**”中，选择“Google广告管理器”，然后选择“ **[!UICONTROL 创建目标”]**。
   ![连接Google Ad Manager目标](/help/rtcdp/destinations/assets/google-1-destination.png)

2. 在创建 **目标** 工作流的设置步骤中，填写目 [!UICONTROL 标的基本信] 息。 <br>

   ![基本信息Google Ad Manager](/help/rtcdp/destinations/assets/ad-manager-setup-step.png)
* **[!UICONTROL 名称]**: 填写此目标的首选名称。
* **[!UICONTROL 描述]**: 可选。 例如，您可以提到您使用此目标的活动。
* **[!UICONTROL 帐户类型]**: 根据您在Google上的帐户选择一个选项：
   * 用于 `DFP by Google` DoubleClick for Publishers
   * 用 `AdX buyer` 于Google AdX
* **[!UICONTROL 帐户ID]**: 使用Google填写您的帐户ID。 这可以是您的网络ID或受众链接ID。 通常，这是一个8位数字的ID。
* **[!UICONTROL 营销用例]**: 市场营销用例指明要将数据导出到目标的目的。 您可以从Adobe定义的营销用例中进行选择，也可以创建自己的营销用例。 有关营销使用案例的更多信息， [请参阅实时CDP中的数据管理](/help/rtcdp/privacy/data-governance-overview.md#destinations) 。 有关Adobe定义的个别营销用例的信息，请参阅数 [据使用策略概述](/help/data-governance/policies/overview.md#core-actions)。

> [!NOTE]
>
> 设置Google广告管理器目标时，请与您的Google客户经理或Adobe代表联系，了解您的帐户类型。

## 将区段激活到Google Ad Manager

有关如何将区段激活到Google Ad Manager的说明，请参阅将 [数据激活到目标](/help/rtcdp/destinations/activate-destinations.md)。