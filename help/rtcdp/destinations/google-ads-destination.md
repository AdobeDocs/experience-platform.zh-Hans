---
title: Google AdsDestination
seo-title: Google广告目标
description: Google Ads（以前称为Google AdWords）是一项在线广告服务，允许企业通过基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示按点击付费广告。
seo-description: Google Ads（以前称为Google AdWords）是一项在线广告服务，允许企业通过基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示按点击付费广告。
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Google广告目标

## 概述

Google Ads（以前称为Google AdWords）是一项在线广告服务，允许企业通过基于文本的搜索、图形显示、YouTube视频和应用程序内移动显示按点击付费广告。

## 目标规范

请注意Google Ads目标特有的以下详细信息：

* 您可以将以下身份发 [送到](../../identity-service/namespaces.md) Google Ads目标：Google **Cookie ID、IDFA、GAID、Roku ID、Microsoft ID、Amazon Fire TV ID**。
* 激活的受众是在Google平台中以编程方式创建的。
* Adobe实时CDP当前不包含用于验证成功激活的度量标准。 请参阅Google中的受众计数，以验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望使用Google Ads创建您的第一个目标，并且以前(使用受众管理器或其他应用程序)未启用 [Experience Cloud ID服务中的](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID同步功能，请联系Adobe Consulting或客户关怀以启用ID同步。 如果您之前在受众管理器中设置了Google集成，则您设置的ID同步会转到Adobe实时CDP。

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

1. 在中， **[!UICONTROL Connections > Destinations]**&#x200B;选择“Google广告”，然后选择 **[!UICONTROL Create destination]**。
   ![Connect Google广告目标](/help/rtcdp/destinations/assets/google-2-destination.png)

2. 在创建目标工作流中，填写目 [!UICONTROL Basic Information] 标的字段。
   ![Google Ads的基本信息](/help/rtcdp/destinations/assets/google-2-basic-information.png)
* **[!UICONTROL Name]**:填写此目标的首选名称。
* **[!UICONTROL Description]**: 可选. 例如，您可以提及要为此目标使用哪个活动。
* **[!UICONTROL Account Type]**:AdWords是唯一可用的选项。
* **[!UICONTROL Account ID]**:使用Google Ads填写您的帐户ID。 ID格式通常为123-456-7890。

## 激活区段至Google广告

有关如何将区段激活到Google Ads的说明，请参阅将 [数据激活到目标](/help/rtcdp/destinations/activate-destinations.md)。

