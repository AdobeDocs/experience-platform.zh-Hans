---
title: Google Ad Manager目标
seo-title: Google Ad Manager目标
description: 'Google Ad Manager（以前称为DoubleClick for Publishers或DoubleClick AdX）是Google的广告服务平台，它为出版商提供了通过视频和移动应用程序管理其网站上广告显示的方法。 '
seo-description: 'Google Ad Manager（以前称为DoubleClick for Publishers或DoubleClick AdX）是Google的广告服务平台，它为出版商提供了通过视频和移动应用程序管理其网站上广告显示的方法。 '
translation-type: tm+mt
source-git-commit: 3e510c891c84fb3dc1632bd1182ef1e010ea898f

---


# Google Ad Manager目标

## 概述

Google Ad Manager（以前称为DoubleClick for Publishers或DoubleClick AdX）是Google的广告服务平台，它为出版商提供了通过视频和移动应用程序管理其网站上广告显示的方法。

## 目标规范

请注意Google Ad Manager目标的以下详细信息：

* 您可以将以下身份发 [送到](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) Google Ad Manager目标：Google **Cookie ID、IDFA、GAID、Roku ID、Microsoft ID、Amazon Fire TV ID**。
* 激活的受众是在Google平台中以编程方式创建的。
* Adobe实时CDP当前不包含用于验证成功激活的度量标准。 请参阅Google中的受众计数以验证集成并了解受众定位规模。

>[!IMPORTANT]
>
>如果您希望使用Google Ad Manager创建您的第一个目标，并且过去（使用Audience Manager或其他应用程序）未在 [Experience Cloud ID服务中启用](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID同步功能，请联系Adobe Consulting或客户关怀以启用ID同步。 如果您之前在Audience Manager中设置了Google集成，则您设置的ID同步将转入Adobe实时CDP。

## 先决条件

### 白名单

>[!NOTE]
>
>在Adobe实时CDP中设置您的第一个Google Ad Manager目标之前，必须填写白名单。 在创建目标之前，请确保Google已完成下面描述的白名单过程。

在Adobe实时CDP中创建Google Ad Manager目标之前，您必须联系Google，要求将Adobe作为数据提供者列入白名单，并将您的帐户列入白名单。 联系Google并提供以下信息：

* **帐户ID** :这是Adobe在Google上的帐户ID。 要获取此ID，请与Adobe客户关怀或您的Adobe代表联系。
* **客户ID** :这是Adobe在Google上的客户帐户ID。 要获取此ID，请与Adobe客户关怀或您的Adobe代表联系。
* **网络ID** :这是您在Google广告管理器上的帐户
* **受众链接ID** :这是您在Google广告管理器上的帐户
* 您的帐户类型。 **DFP，由Google** 或 **AdX购买者提供**。

## 创建目标

1. 在中， **[!UICONTROL Connections > Destinations]**&#x200B;选择Google广告管理器，然后选择 **[!UICONTROL Create destination]**。
   ![连接Google Ad Manager目标](/help/rtcdp/destinations/assets/google-1-destination.png)

2. 在创建目标向导中，填写目标的基本信息。
   ![基本信息Google广告经理](/help/rtcdp/destinations/assets/google-1-basic-information.png)
* **名称**:填写此目标的首选名称。
* **说明**:可选。 例如，您可以提及要为此目标使用哪个营销活动。
* **帐户类型**:根据您在Google上的帐户，选择一个选项：
   * 用 `DFP by Google` 于DoubleClick for Publishers
   * 用 `AdX buyer` 于Google AdX
* **帐户ID**:使用Google填写您的帐户ID。 这可以是您的网络ID或受众链接ID。 通常，这是一个8位数字ID。

>[!NOTE]
>
>设置Google广告管理器目标时，请与您的Google客户经理或Adobe代表联系，以了解您拥有的帐户类型。

## 将区段激活到Google Ad Manager

有关如何将区段激活到Google Ad Manager的说明，请参阅将数 [据激活到目标](/help/rtcdp/destinations/activate-destinations.md)。