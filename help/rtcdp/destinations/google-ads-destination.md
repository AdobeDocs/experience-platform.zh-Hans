---
title: Google AdsDestination
seo-title: Google广告目标
description: Google Ads（以前称为Google AdWords）是一种在线广告服务，允许企业在基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示中按点击付费广告。
seo-description: Google Ads（以前称为Google AdWords）是一种在线广告服务，允许企业在基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示中按点击付费广告。
translation-type: tm+mt
source-git-commit: 121ae74e9c352b1f6fc12093d815e711ebd817b8
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# Google广告目标

## 概述

Google Ads（以前称为Google AdWords）是一种在线广告服务，允许企业在基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示中按点击付费广告。

## 目标规范

请注意Google Ads目标特有的以下详细信息：

* 您可以将以下身份 [发送](../../identity-service/namespaces.md) 到Google Ads目标： **Google Cookie ID、IDFA、GAID、Roku ID、Microsoft ID、Amazon Fire TV ID**。
* 激活的受众是在Google平台中以编程方式创建的。
* Adobe实时CDP当前不包含用于验证成功激活的度量。 请参阅Google中的受众计数，验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望使用Google Ads创建您的第一个目标，并且过去(使用受众管理器 [](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) 或其他应用程序)未在Experience Cloud ID服务中启用ID同步功能，请联系Adobe Consulting或客户关怀以启用ID同步。 如果您以前在受众管理器中设置Google集成，则您设置的ID同步将结转到Adobe实时CDP。

## 先决条件

### 现有Google Ads帐户

谷歌暂停了任何与第三方供应商集成的新Google Ads。 您必须已与Google Ads集成，才能执行下一节中的白名单步骤，并在Adobe实时CDP中创建Google Ads目标。

### 白名单

>[!NOTE]
>
>在Adobe实时CDP中设置您的第一个Google Ads目标之前，必须填写白名单。 在创建目标之前，请确保Google已完成下面描述的白名单过程。

在Adobe实时CDP中创建Google Ads目标之前，您必须联系Google，要求将Adobe列入白名单并将您的帐户列入白名单。 联系Google并提供以下信息：

* **帐户ID** : 这是Adobe在Google上的帐户ID。 要获取此ID，请与Adobe客户服务或Adobe代表联系。
* **客户ID** : 这是Adobe在Google上的客户帐户ID。 要获取此ID，请与Adobe客户服务或Adobe代表联系。
* 您的帐户类型： **AdWords**
* **Google AdWords ID** : 这是你在谷歌的ID。 ID格式通常为123-456-7890。

## 创建目标

1. 在“ **[!UICONTROL 连接”>“目标]**”中，选择“Google Ads”，然后选择“ **[!UICONTROL 创建目标”]**。
   ![连接Google广告目标](/help/rtcdp/destinations/assets/google-2-destination.png)

2. 在创建目标工作流中，填写目 [!UICONTROL 标的基本] 信息。 <br>
   ![Google Ads的基本信息](/help/rtcdp/destinations/assets/google-2-basic-information.png)
* **[!UICONTROL 名称]**: 填写此目标的首选名称。
* **[!UICONTROL 描述]**: 可选。 例如，您可以提到您使用此目标的活动。
* **[!UICONTROL 帐户类型]**: AdWords是唯一可用的选项。
* **[!UICONTROL 帐户ID]**: 使用Google Ads填写您的帐户ID。 ID格式通常为123-456-7890。

## 激活Google广告的细分

有关如何将区段激活到Google Ads的说明，请参阅将 [数据激活到目标](/help/rtcdp/destinations/activate-destinations.md)。

