---
title: Google AdsDestination
seo-title: Google广告目标
description: Google Ads（以前称为Google AdWords）是一项在线广告服务，允许企业通过基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示按点击付费广告。
seo-description: Google Ads（以前称为Google AdWords）是一项在线广告服务，允许企业通过基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示按点击付费广告。
translation-type: tm+mt
source-git-commit: 3e510c891c84fb3dc1632bd1182ef1e010ea898f

---


# Google广告目标

## 概述

Google Ads（以前称为Google AdWords）是一项在线广告服务，允许企业通过基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示按点击付费广告。

## 目标规范

请注意Google Ads目标特有的以下详细信息：

* 您可以将以下身份发 [送到](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) Google Ads目标：Google **Cookie ID、IDFA、GAID、Roku ID、Microsoft ID、Amazon Fire TV ID**。
* 激活的受众是在Google平台中以编程方式创建的。
* Adobe实时CDP当前不包含用于验证成功激活的度量标准。 请参阅Google中的受众计数以验证集成并了解受众定位规模。

>[!IMPORTANT]
>
>如果您希望使用Google Ads创建您的第一个目标，并且以前（使用Audience Manager或其他应用程序）未在 [Experience Cloud ID服务中启用](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID同步功能，请联系Adobe Consulting或客户关怀以启用ID同步。 如果您之前在Audience Manager中设置了Google集成，则您设置的ID同步将转入Adobe实时CDP。

## 先决条件

### 现有Google Ads帐户

Google暂停了与第三方供应商的任何新的Google Ads集成。 您必须与Google Ads进行现有集成，才能执行下一节中的白名单步骤，并在Adobe实时CDP中创建Google Ads目标。

### 白名单

>[!NOTE]
>
>在Adobe实时CDP中设置您的第一个Google广告目标之前，必须填写白名单。 在创建目标之前，请确保Google已完成下面描述的白名单过程。

在Adobe实时CDP中创建Google广告目标之前，您必须联系Google，要求将Adobe列入白名单并将您的帐户列入白名单。 联系Google并提供以下信息：

* **帐户ID** :这是Adobe在Google上的帐户ID。 要获取此ID，请与Adobe客户关怀或您的Adobe代表联系。
* **客户ID** :这是Adobe在Google上的客户帐户ID。 要获取此ID，请与Adobe客户关怀或您的Adobe代表联系。
* 您的帐户类型：AdWords ****
* **Google AdWords ID** :这是您在Google上的ID。 ID格式通常为123-456-7890。

## 创建目标

1. 在“ **[!UICONTROL 连接”>“目标]**”中，选择“Google广告”，然后选择“ **[!UICONTROL 创建目标”]**。
   ![Connect Google广告目标](/help/rtcdp/destinations/assets/google-2-destination.png)

2. 在创建目标向导中，填写目标的基本信息。
   ![Google Ads的基本信息](/help/rtcdp/destinations/assets/google-2-basic-information.png)
* **名称**:填写此目标的首选名称。
* **说明**:可选。 例如，您可以提及要为此目标使用哪个营销活动。
* **帐户类型**:AdWords是唯一可用的选项。
* **帐户ID**:使用Google Ads填写您的帐户ID。 ID格式通常为123-456-7890。

## 激活区段至Google广告

有关如何将区段激活到Google Ads的说明，请参阅将 [数据激活到目标](/help/rtcdp/destinations/activate-destinations.md)。

