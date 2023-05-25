---
keywords: 目标；问题；常见问题解答；常见问题解答；目标常见问题解答
title: 常见问题解答
description: 关于Adobe Experience Platform目标的最常见问题解答
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 4%

---

# 常见问题解答 {#faq}

## 概述 {#overview}

本文档提供了有关Adobe Experience Platform目标的常见问题解答。 有关其他方面的问题和疑难解答 [!DNL Platform] 服务，包括在所有服务中遇到的 [!DNL Platform] API，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md).

## 一般目标问题 {#general}

**为什么在Experience PlatformUI和导出的CSV文件中看到不同的配置文件计数？**

由于Experience Platform执行分段的方式，这是正常行为。

流式分段会更新一整天流式区段的配置文件计数，而批量分段每24小时更新一次批量区段的配置文件计数。

当区段导出计划与分段计划不同时，配置文件在UI和导出的之间计数 [!DNL CSV] 文件将有所不同，尤其是在流区段方面。

请参阅 [分段服务文档](../segmentation/home.md) 了解更多详细信息。

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**在中激活受众之前，我需要做什么 [!DNL Facebook Custom Audiences]？**

在将受众区段发送到之前 [!DNL Facebook]，确保您满足以下要求：

* 您的 [!DNL Facebook] 用户帐户必须具有 **[!DNL Manage campaigns]** 为您计划使用的广告帐户启用的权限。
* 此 **Adobe Experience Cloud** 必须将商业帐户作为广告合作伙伴添加到您的 [!DNL Facebook Ad Account]. 使用 `business ID=206617933627973`。参见 [将合作伙伴添加到您的业务经理](https://www.facebook.com/business/help/1717412048538897) 有关详细信息，请参阅Facebook文档。
   >[!IMPORTANT]
   >
   > 配置Adobe Experience Cloud的权限时，您必须启用 **管理营销活动** 许可。 [!DNL Adobe Experience Platform] 集成要求具备此权限。
* 阅读并签署 [!DNL Facebook Custom Audiences] 服务条款。 为此，请转到 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中 `accountID` 是您的 [!DNL Facebook Ad Account ID]。

**我是否需要向添加任何应用程序或像素 [!DNL Facebook] 广告商帐户？**

不会。由于这不是基于像素的集成，因此无需向广告商帐户中添加任何像素。

**facebook处理来自Adobe Experience Platform的信息需要多长时间？**

截至2021年3月， [!DNL Facebook Custom Audiences] 最多需要一小时来处理从收到的信息 [!DNL Platform].

**我可以使用吗 [!DNL Facebook Custom Audiences] 用于其他中的受众定位 [!DNL Facebook] 应用程序，例如 [!DNL Instagram]？**

您可以使用 [!DNL Facebook Custom Audiences] 跨Facebook系列受支持的应用程序进行受众定位的目标 [!DNL Facebook Custom Audiences]，包括 [!DNL Facebook]， [!DNL Instagram]， [!DNL Audience Network]、和 [!DNL Messenger]. 中的版面级别会显示广告商要在其上运行营销活动的所选应用程序 [!DNL Facebook Ads Manager].

**两者之间有何区别 [!DNL Facebook Custom Audiences] 连接和 [!DNL Facebook Pixel] 扩展？**

此 [!DNL Facebook Custom Audiences] 连接使用情况 [!DNL Platform] 将受众发送到时的身份 [!DNL Facebook]，而 [[!DNL Facebook Pixel] 连接](../destinations/catalog/advertising/facebook-pixel.md) 使用 [!DNL Facebook] 集成在网站中的像素。

这两种集成是互补的，您可以同时使用这两种集成来确保更好的受众覆盖。例如，您可以使用 [!DNL Facebook Pixel] 扩展程序，适用于尚未创建帐户的潜在网站访客，而 [!DNL Facebook Custom Audiences] 可以帮助您定位现有客户，基于 [!DNL Platform] 身份。

**Adobe Experience Platform是否与集成 [!DNL Facebook Custom Audiences] 支持在不再符合受众资格时取消其受众资格？**

是，该集成支持从删除用户 [!DNL Facebook Custom Audiences] 当他们不再符合条件时。

**在发送受众数据之前，我应如何对其进行哈希处理？ [!DNL Facebook]？**

[!DNL Facebook] 要求不发送明确的个人身份信息(PII)。 因此，受众激活到 [!DNL Facebook] 可以被关掉 *哈希* 标识符，例如电子邮件地址或电话号码。

有关ID匹配要求的详细说明，请参阅 [ID匹配要求](catalog/social/facebook.md#id-matching-requirements).

**我可以激活哪种身份 [!DNL Facebook Custom Audiences]？**

[!DNL Facebook Custom Audiences] 支持激活以下标识：经过哈希处理的电子邮件、经过哈希处理的电话号码， [!DNL GAID]， [!DNL IDFA]和自定义外部ID。

**我能否在Platform UI中为单独的Facebook帐户创建多个Facebook目标？**

可以。Experience Platform中的Facebook目标与Facebook中的广告帐户之比是1:1。 您可以为公司中的每个Facebook广告帐户创建单独的Facebook目标。 请遵循 [目标连接教程](/help/destinations/ui/connect-destination.md) 并为Platform UI中的每个新Facebook目标连接到单独的Facebook帐户。 您可以连接到的Facebook广告帐户数量没有限制。

## Google 客户匹配 {#google-customer-match}

**将区段导出到Google Customer Match时，为什么在Google界面的区段名称末尾附加了额外的数字？**

Google要求区段名称是唯一的。 您所看到的数字是 [UNIX时间戳](https://www.unixtimestamp.com/) 如果将同一区段映射到多个Google目标，则会附加这些区段以保持区段名称唯一。

## linkedIn匹配的受众 {#linkedin}

**我是否需要向添加任何应用程序或像素 [!DNL LinkedIn] 广告商帐户？**

不会。由于这不是基于像素的集成，因此无需向广告商帐户中添加任何像素。

**在中激活受众之前，我需要做什么 [!DNL LinkedIn Matched Audiences]？**

在使用 [!UICONTROL linkedIn匹配的受众] 目标，确保您的 [!DNL LinkedIn Campaign Manager] 帐户具有 [!DNL Creative Manager] 权限级别或更高。

要了解如何编辑您的 [!DNL LinkedIn Campaign Manager] 用户权限，请参见 [添加、编辑和删除广告帐户的用户权限](https://www.linkedin.com/help/lms/answer/5753) 在LinkedIn文档中。

**在发送受众数据之前，我应如何对其进行哈希处理？ [!DNL LinkedIn]？**

[!DNL LinkedIn] 要求不发送明确的个人身份信息(PII)。 因此，受众激活到 [!DNL LinkedIn] 可以被关掉 *哈希* 标识符，例如电子邮件地址或电话号码。

有关ID匹配要求的详细说明，请参阅 [ID匹配要求](catalog/social/linkedin.md#id-matching-requirements).

**我可以激活哪种身份 [!DNL LinkedIn]？**

[!DNL LinkedIn Matched Audiences] 支持激活以下标识：经过哈希处理的电子邮件， [!DNL GAID]、和 [!DNL IDFA].
