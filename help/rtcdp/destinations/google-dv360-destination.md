---
title: Google Display & Video 360 Destination
seo-title: Google Display & Video 360 Destination
description: Display & Video 360（以前称为DoubleClick Bid Manager）是一种工具，用于跨显示、视频和移动库存源执行重定位和受众目标数字活动。
seo-description: 'Display & Video 360（以前称为DoubleClick Bid Manager）是一种工具，用于跨显示、视频和移动库存源执行重定位和受众目标数字活动。 '
translation-type: tm+mt
source-git-commit: 121ae74e9c352b1f6fc12093d815e711ebd817b8
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---


# Google Display &amp; Video 360 Destination

## 概述

Display &amp; Video 360（以前称为DoubleClick Bid Manager）是一种工具，用于跨显示屏、视频和移动库存源执行重定位和受众目标数字活动。

## 目标规范

请注意Google Display &amp; Video 360目标特有的以下详细信息：

* 您可以将以下身份 [发送](../../identity-service/namespaces.md) 到Google Display &amp; Video 360目标： **Google Cookie ID、IDFA、GAID、Roku ID、Microsoft ID、Amazon Fire TV ID**。
* 激活的受众是在Google平台中以编程方式创建的。
* Adobe实时CDP当前不包含用于验证成功激活的度量。 请参阅Google中的受众计数，验证集成并了解受众定位大小。

>[!IMPORTANT]
>
>如果您希望使用Google Display &amp; Video 360创建您的第一个目标，并且过去(使用Adobe受众管理器或其他应用程序 [](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) )未在Experience Cloud ID服务中启用ID同步功能，请联系Adobe Consulting或客户关怀以启用ID同步。 如果您以前在受众管理器中设置Google集成，则您设置的ID同步将结转到Adobe实时CDP。

## 先决条件

### 白名单

>[!NOTE]
>
>在Adobe实时CDP中设置您的第一个Google Display &amp; Video 360目标之前，必须填写白名单。 在创建目标之前，请确保Google已完成下面描述的白名单过程。

在Adobe实时CDP中创建Google Display &amp; Video 360目标之前，您必须联系Google，要求将Adobe列入白名单，并将您的帐户列入白名单。 联系Google并提供以下信息：

* **帐户ID** : 这是Adobe在Google上的帐户ID。 要获取此ID，请与Adobe客户服务或Adobe代表联系。
* **客户ID** : 这是Adobe在Google上的客户帐户ID。 要获取此ID，请与Adobe客户服务或Adobe代表联系。
* **您的帐户类型**: 使 **[!DNL Invite advertiser]** 用以仅允许受众共享到您的Display &amp; Video 360帐户中的特定品牌，或 **[!DNL Invite partner]** 者使用以允许受众共享到您的Display &amp; Video 360帐户中的所有品牌。

## 创建目标

1. 在“ **[!UICONTROL 连接”>“目标]**”中，选择“Google Display &amp; Video 360”，然后选择“创 **[!UICONTROL 建目标”]**。
   ![Connect Google Display &amp; Video 360目标](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. 在创建目标工作流中，填写目 [!UICONTROL 标的基本] 信息。 <br>
   ![基本信息Google Display &amp; Video 360](/help/rtcdp/destinations/assets/google-dv360-basic-information.png)
* **[!UICONTROL 名称]**: 填写此目标的首选名称。
* **[!UICONTROL 描述]**: 可选。 例如，您可以提到您使用此目标的活动。
* **[!UICONTROL 帐户类型]**: 根据您在Google上的帐户选择一个选项：
   * 使 `Invite Advertiser` 用以仅允许受众共享到您的显示和视频360帐户中的特定品牌。
   * 使 `Invite Partner` 用，允许受众共享到您的Display &amp; Video 360帐户中的所有品牌。
* **[!UICONTROL 帐户ID]**: 使用Google填 **[!DNL Invite partner]** 写您 **[!DNL Invite advertiser]** 的或帐户ID。 通常，这是一个6或7位数字ID。

>[!NOTE]
>
>设置Google Display &amp; Video 360目标时，请与您的Google客户经理或Adobe代表联系，了解您的帐户类型。

## 将区段激活到Google Display &amp; Video 360

有关如何将区段激活到Google Display &amp; Video 360的说明，请参阅将 [数据激活到目标](/help/rtcdp/destinations/activate-destinations.md)。