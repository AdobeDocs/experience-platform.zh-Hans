---
keywords: 目标；问题；常见问题解答；常见问题解答；目标常见问题解答
title: 关于 Experience Cloud 核心服务
seo-title: 关于 Experience Cloud 核心服务
description: 有关Adobe Experience Platform目标的最常见问题解答
seo-description: 有关Adobe Experience Platform目标的最常见问题解答
source-git-commit: 47b3ef28281e3480e8b194486845f4fb4326b7d4
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 6%

---


# 关于 Experience Cloud 核心服务 {#faq}

## 概述 {#overview}

本文档提供了有关Adobe Experience Platform目标的常见问题解答。 有关与其他[!DNL Platform]服务（包括所有[!DNL Platform] API中遇到的服务）相关的问题和疑难解答，请参阅[Experience Platform疑难解答指南](../landing/troubleshooting.md)。

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**在中激活受众之前，我需要执行哪些操 [!DNL Facebook Custom Audiences]作？**

在将受众区段发送到[!DNL Facebook]之前，请确保满足以下要求：

* 您的[!DNL Facebook]用户帐户必须为您计划使用的广告帐户启用&#x200B;**[!DNL Manage campaigns]**&#x200B;权限。
* **Adobe Experience Cloud**&#x200B;业务帐户必须作为广告合作伙伴添加到您的[!DNL Facebook Ad Account]中。 使用 `business ID=206617933627973`. 有关详细信息，请参阅Facebook文档中的[将合作伙伴添加到您的业务经理](https://www.facebook.com/business/help/1717412048538897)。
   >[!IMPORTANT]
   >
   > 配置Adobe Experience Cloud的权限时，必须启用&#x200B;**管理促销活动**&#x200B;权限。 [!DNL Adobe Experience Platform] 集成要求具备此权限。
* 阅读并签署[!DNL Facebook Custom Audiences]服务条款。 为此，请转到 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中 `accountID` 是您的 [!DNL Facebook Ad Account ID]。

**是否需要向广告商帐户添加任何应用程序或 [!DNL Facebook] 像素？**

否。由于这不是基于像素的集成，因此无需向广告商帐户添加任何像素。

**facebook需要多长时间才能处理来自Adobe Experience Platform的信息？**

自2021年3月起，[!DNL Facebook Custom Audiences]最多需要1小时才能处理从[!DNL Platform]收到的信息。

**我能否在其 [!DNL Facebook Custom Audiences] 他应用程序（如）中 [!DNL Facebook] 用于受众定 [!DNL Instagram]位？**

您可以使用[!DNL Facebook Custom Audiences]目标在[!DNL Facebook Custom Audiences]支持的Facebook系列应用程序（包括[!DNL Facebook]、[!DNL Instagram]、[!DNL Audience Network]和[!DNL Messenger]）中定位受众。 [!DNL Facebook Ads Manager]的版面级别会显示广告商要在上运行促销活动的所选应用程序。

**连接和扩展之间有 [!DNL Facebook Custom Audiences] 何区 [!DNL Facebook Pixel] 别？**

在向[!DNL Facebook]发送受众时，[!DNL Facebook Custom Audiences]连接使用[!DNL Platform]标识，而[[!DNL Facebook Pixel] 连接](../destinations/catalog/advertising/facebook-pixel.md)使用集成在网站中的[!DNL Facebook]像素。

这两种集成是互补的，您可以同时使用这两种集成来确保更好的受众覆盖。例如，您可以使用[!DNL Facebook Pixel]扩展来帮助潜在的尚未创建帐户的网站访客，而[!DNL Facebook Custom Audiences]可以帮助您根据[!DNL Platform]身份定位现有客户。

**当用户不再符合受 [!DNL Facebook Custom Audiences] 众的资格时，Adobe Experience Platform与支持的集成是否会使他们从受众中取消资格？**

是，当用户不再符合条件时，该集成支持从[!DNL Facebook Custom Audiences]中删除用户。

**如何在将受众数据发送到之前对其进行哈希处 [!DNL Facebook]理？**

[!DNL Facebook] 要求不要发送任何个人身份信息(PII)。因此，激活到[!DNL Facebook]的受众可以与&#x200B;*哈希*&#x200B;标识符（如电子邮件地址或电话号码）关联。

有关ID匹配要求的详细说明，请参阅[ID匹配要求](catalog/social/facebook.md#id-matching-requirements)。

**我可以在中激活哪种身份 [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] 支持激活以下标识：经过哈希处理的电子邮件、经过哈希处理的 [!DNL GAID]电话号码 [!DNL IDFA]、和自定义外部ID。

## linkedIn匹配的受众 {#linkedin}

**是否需要向广告商帐户添加任何应用程序或 [!DNL LinkedIn] 像素？**

否。由于这不是基于像素的集成，因此无需向广告商帐户添加任何像素。

**在中激活受众之前，我需要执行哪些操 [!DNL LinkedIn Matched Audiences]作？**

在使用[!UICONTROL LinkedIn匹配受众]目标之前，请确保您的[!DNL LinkedIn Campaign Manager]帐户具有[!DNL Creative Manager]权限级别或更高级别。

要了解如何编辑[!DNL LinkedIn Campaign Manager]用户权限，请参阅LinkedIn文档中的[添加、编辑和删除广告帐户的用户权限](https://www.linkedin.com/help/lms/answer/5753) 。

**如何在将受众数据发送到之前对其进行哈希处 [!DNL LinkedIn]理？**

[!DNL LinkedIn] 要求不要发送任何个人身份信息(PII)。因此，激活到[!DNL LinkedIn]的受众可以与&#x200B;*哈希*&#x200B;标识符（如电子邮件地址或电话号码）关联。

有关ID匹配要求的详细说明，请参阅[ID匹配要求](catalog/social/linkedin.md#id-matching-requirements)。

**我可以在中激活哪种身份 [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] 支持激活以下标识：经过哈希处理的 [!DNL GAID]电子邮件和 [!DNL IDFA]。
