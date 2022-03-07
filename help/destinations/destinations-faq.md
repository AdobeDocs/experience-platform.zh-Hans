---
keywords: 目标；问题；常见问题解答；常见问题解答；目标常见问题解答
title: 常见问题
seo-title: Frequently asked questions
description: 有关Adobe Experience Platform目标的最常见问题解答
seo-description: Answers to the most frequently asked questions about Adobe Experience Platform destinations
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: b2636377eda6740dceb9bc07fbcc082b85ff3c94
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 4%

---

# 常见问题 {#faq}

## 概述 {#overview}

本文档提供了有关Adobe Experience Platform目标的常见问题解答。 有关与其他 [!DNL Platform] 服务，包括所有 [!DNL Platform] API，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md).

## 一般目标问题 {#general}

**为什么我在Experience PlatformUI和导出的CSV文件中看到不同的配置文件计数？**

这是由于Experience Platform执行分段的方式而导致的正常行为。

流式客户细分会更新一天中流式客户细分的配置文件计数，而批量客户细分会每24小时更新一次批量客户细分的配置文件计数。

如果区段导出计划与分段计划不同，则UI和导出的配置文件会进行计数 [!DNL CSV] 文件将不同，特别是在涉及流区段时。

请参阅 [Segmentation Service文档](../segmentation/home.md) 以了解更多详细信息。

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**在中激活受众之前，我需要执行哪些操作 [!DNL Facebook Custom Audiences]?**

在将受众区段发送到 [!DNL Facebook]，请确保满足以下要求：

* 您的 [!DNL Facebook] 用户帐户必须具有 **[!DNL Manage campaigns]** 为您计划使用的广告帐户启用的权限。
* 的 **Adobe Experience Cloud** 业务帐户必须作为广告合作伙伴添加到您的 [!DNL Facebook Ad Account]. 使用 `business ID=206617933627973`. 请参阅 [将合作伙伴添加到您的业务经理](https://www.facebook.com/business/help/1717412048538897) (在Facebook文档中)。
   >[!IMPORTANT]
   >
   > 配置Adobe Experience Cloud的权限时，必须启用 **管理营销活动** 权限。 [!DNL Adobe Experience Platform] 集成要求具备此权限。
* 阅读并签署 [!DNL Facebook Custom Audiences] 服务条款。 为此，请转到 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中 `accountID` 是您的 [!DNL Facebook Ad Account ID]。

**是否需要向 [!DNL Facebook] 广告商帐户？**

不会。由于这不是基于像素的集成，因此无需向广告商帐户添加任何像素。

**facebook需要多长时间才能处理来自Adobe Experience Platform的信息？**

自2021年3月起， [!DNL Facebook Custom Audiences] 需要长达一小时的时间来处理从 [!DNL Platform].

**我能用一下吗 [!DNL Facebook Custom Audiences] 用于其他 [!DNL Facebook] 应用程序，如 [!DNL Instagram]?**

您可以使用 [!DNL Facebook Custom Audiences] 目标，用于在Facebook支持的一系列应用程序中进行受众定位 [!DNL Facebook Custom Audiences]，包括 [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network]和 [!DNL Messenger]. 在的版面级别，会显示广告商要在上运行促销活动的所选应用程序 [!DNL Facebook Ads Manager].

**这两者之间的区别 [!DNL Facebook Custom Audiences] 连接和 [!DNL Facebook Pixel] 扩展？**

的 [!DNL Facebook Custom Audiences] 连接使用 [!DNL Platform] 将受众发送到 [!DNL Facebook]，而 [[!DNL Facebook Pixel] 连接](../destinations/catalog/advertising/facebook-pixel.md) 使用 [!DNL Facebook] 网站中集成的像素。

这两种集成是互补的，您可以同时使用这两种集成来确保更好的受众覆盖。例如，您可以使用 [!DNL Facebook Pixel] 扩展，用于寻找尚未创建帐户的网站访客，而 [!DNL Facebook Custom Audiences] 可帮助您定位现有客户，具体依据 [!DNL Platform] 身份。

**Does the Adobe Experience Platform integration with [!DNL Facebook Custom Audiences] support disqualifying users from an audience when they no longer qualify for it?**

Yes, the integration supports removing users from [!DNL Facebook Custom Audiences] when they no longer qualify.

**How should I hash the audience data before sending it to [!DNL Facebook]?**

[!DNL Facebook] 要求不要发送任何个人身份信息(PII)。 因此，激活的受众 [!DNL Facebook] 可以锁上 *哈希* 标识符，如电子邮件地址或电话号码。

有关ID匹配要求的详细说明，请参阅 [ID匹配要求](catalog/social/facebook.md#id-matching-requirements).

**我可以在中激活哪种身份 [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] 支持激活以下标识：哈希电子邮件，哈希电话号码， [!DNL GAID], [!DNL IDFA]、和自定义外部ID。

**我能否在Platform UI中为单独的Facebook帐户创建多个Facebook目标？**

可以。Experience Platform中的Facebook目标为Facebook中某个广告帐户的1:1。 您可以为公司中的每个Facebook广告帐户创建一个单独的Facebook目标。 关注 [目标连接教程](/help/destinations/ui/connect-destination.md) 并在Platform UI中为每个新的Facebook目标连接单独的Facebook帐户。 您可以连接的Facebook广告帐户数量没有限制。

## Google 客户匹配 {#google-customer-match}

**将区段导出到Google客户匹配时，为什么在Google界面中的区段名称末尾会附加额外的数字？**

Google要求区段名称是唯一的。 你看到的数字 [UNIX时间戳](https://www.unixtimestamp.com/) 如果您将同一区段映射到多个Google目标，则会附加区段名称以保持区段名称唯一。

## linkedIn匹配的受众 {#linkedin}

**是否需要向 [!DNL LinkedIn] 广告商帐户？**

不会。由于这不是基于像素的集成，因此无需向广告商帐户添加任何像素。

**在中激活受众之前，我需要执行哪些操作 [!DNL LinkedIn Matched Audiences]?**

在使用 [!UICONTROL linkedIn匹配受众] 目标，确保 [!DNL LinkedIn Campaign Manager] 帐户具有 [!DNL Creative Manager] 权限级别或更高级别。

了解如何编辑 [!DNL LinkedIn Campaign Manager] 用户权限，请参阅 [添加、编辑和删除广告帐户的用户权限](https://www.linkedin.com/help/lms/answer/5753) (在LinkedIn文档中)。

**如何在将受众数据发送到之前对其进行哈希处理 [!DNL LinkedIn]?**

[!DNL LinkedIn] 要求不要发送任何个人身份信息(PII)。 因此，激活的受众 [!DNL LinkedIn] 可以锁上 *哈希* 标识符，如电子邮件地址或电话号码。

有关ID匹配要求的详细说明，请参阅 [ID匹配要求](catalog/social/linkedin.md#id-matching-requirements).

**我可以在中激活哪种身份 [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] 支持激活以下标识：哈希电子邮件， [!DNL GAID]和 [!DNL IDFA].
