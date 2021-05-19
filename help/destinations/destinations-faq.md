---
keywords: 目的地；问题；常见问题；常见问题解答；目标常见问题解答
title: 目标常见问题解答
seo-title: 目标常见问题解答
description: 有关Adobe Experience Platform目标的常见问题解答
seo-description: 有关Adobe Experience Platform目标的常见问题解答
source-git-commit: 117f0f82adb764cedaa048e718cd72fa033845a0
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 5%

---


# 目标常见问题解答 {#faq}

## [!DNL Facebook Custom Audiences] (#facebook-faq)

**在中激活受众之前，我需要做什么 [!DNL Facebook Custom Audiences]?**

在将受众区段发送到[!DNL Facebook]之前，请确保满足以下要求：

* 您的[!DNL Facebook]用户帐户必须为您计划使用的Ad帐户启用&#x200B;**[!DNL Manage campaigns]**&#x200B;权限。
* **Adobe Experience Cloud**&#x200B;业务帐户必须作为广告合作伙伴添加到您的[!DNL Facebook Ad Account]中。 使用 `business ID=206617933627973`. 有关详细信息，请参阅Facebook文档中的[将合作伙伴添加到您的业务经理](https://www.facebook.com/business/help/1717412048538897)。
   >[!IMPORTANT]
   >
   > 配置Adobe Experience Cloud的权限时，必须启用&#x200B;**管理活动**&#x200B;权限。 [!DNL Adobe Experience Platform] 集成要求具备此权限。
* 阅读并签署[!DNL Facebook Custom Audiences]服务条款。 为此，请转到 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中 `accountID` 是您的 [!DNL Facebook Ad Account ID]。

**我是否需要向广告商帐户添加任何应用程序 [!DNL Facebook] 或像素？**

否。由于这不是基于像素的集成，因此无需向广告商帐户添加任何像素。

**facebook需要多长时间才能处理来自Adobe Experience Platform的信息？**

截至2021年3月，[!DNL Facebook Custom Audiences]需要最多1小时才能处理从[!DNL Platform]收到的信息。

**我是否可以在 [!DNL Facebook Custom Audiences] 其他应用程序( [!DNL Facebook] 如)中用于受众 [!DNL Instagram]定位？**

您可以在[!DNL Facebook Custom Audiences]支持的[!DNL Facebook]、[!DNL Instagram]、[!DNL Audience Network]和[!DNL Messenger]的Facebook系列应用程序中使用[!DNL Facebook Custom Audiences]目标进行受众定位。 在[!DNL Facebook Ads Manager]中的位置级别指示广告商要运行活动的应用程序的选择。

**连接和扩展之间 [!DNL Facebook Custom Audiences] 有何 [!DNL Facebook Pixel] 差异？**

在向[!DNL Facebook]发送受众时，[!DNL Facebook Custom Audiences]连接使用[!DNL Platform]标识，而[[!DNL Facebook Pixel] 连接](../destinations/catalog/advertising/facebook-pixel.md)使用集成在网站中的[!DNL Facebook]像素。

这两种集成是互补的，您可以同时使用这两种集成来确保更好的受众覆盖。例如，您可以使用[!DNL Facebook Pixel]扩展找到尚未创建帐户的网站访客，而[!DNL Facebook Custom Audiences]可以帮助您基于[!DNL Platform]身份目标现有客户。

**Adobe Experience Platform与支持的集成是否 [!DNL Facebook Custom Audiences] 会在用户不再有资格获得受众时使用者无法获得资格？**

是，集成支持在用户不再符合条件时从[!DNL Facebook Custom Audiences]中删除用户。

**在将受众数据发送到之前，应如何对其进行哈希处理 [!DNL Facebook]?**

[!DNL Facebook] 要求不要发送任何清晰的个人身份信息(PII)。因此，激活到[!DNL Facebook]的受众可以键出&#x200B;*散列*&#x200B;标识符，如电子邮件地址或电话号码。

有关ID匹配要求的详细说明，请参阅[ID匹配要求](catalog/social/facebook.md#id-matching-requirements)。

**我可以激活什么身份 [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] 支持激活以下身份：散列电子邮件、散列电话号码 [!DNL GAID]和自 [!DNL IDFA]定义外部ID。

## linkedIn匹配的受众 {#linkedin}

**我是否需要向广告商帐户添加任何应用程序 [!DNL LinkedIn] 或像素？**

否。由于这不是基于像素的集成，因此无需向广告商帐户添加任何像素。

**在中激活受众之前，我需要做什么 [!DNL LinkedIn Matched Audiences]?**

在使用[!UICONTROL LinkedIn匹配受众]目标之前，请确保您的[!DNL LinkedIn Campaign Manager]帐户具有[!DNL Creative Manager]权限级别或更高级别。

要了解如何编辑您的[!DNL LinkedIn Campaign Manager]用户权限，请参阅LinkedIn文档中的[添加、编辑和删除广告帐户的用户权限](https://www.linkedin.com/help/lms/answer/5753)。

**在将受众数据发送到之前，应如何对其进行哈希处理 [!DNL LinkedIn]?**

[!DNL LinkedIn] 要求不要发送任何清晰的个人身份信息(PII)。因此，激活到[!DNL LinkedIn]的受众可以键出&#x200B;*散列*&#x200B;标识符，如电子邮件地址或电话号码。

有关ID匹配要求的详细说明，请参阅[ID匹配要求](catalog/social/linkedin.md#id-matching-requirements)。

**我可以激活什么身份 [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] 支持激活以下身份：散乱的 [!DNL GAID]电子邮件 [!DNL IDFA]。
