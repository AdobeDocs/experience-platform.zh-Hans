---
keywords: 目标；问题；常见问题解答；常见问题解答；目标常见问题解答
title: 常见问题解答
description: 关于Adobe Experience Platform目标最常见问题的解答
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 810bcd011fd6e172c79f4482e047aa6e715c3918
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 4%

---

# 常见问题解答 {#faq}

## 概述 {#overview}

本文档提供有关Adobe Experience Platform目标的常见问题解答。 有关其他方面的问题和疑难解答 [!DNL Platform] 服务，包括在所有服务中遇到的 [!DNL Platform] API，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md).

## 一般目标问题 {#general}

### 为什么在Experience PlatformUI和导出的CSV文件中看到不同的配置文件计数？

+++答案由于Experience Platform执行分段的方式，这是正常行为。

流式分段会更新一天中流式受众的个人资料计数，而批量分段每24小时更新一次批量受众的个人资料计数。

当受众导出计划与分段计划不同时，UI和导出的之间的配置文件计数 [!DNL CSV] 文件将有所不同，尤其是在处理流受众时。

请参阅 [Segmentation Service文档](../segmentation/home.md) 以了解更多详细信息。
+++

### 为什么在停用更新的受众并将其重新激活到同一目标时，匹配率会很低？

+++回答

在受众重新激活到同一流目的地时，来自流目的地的受众的停用和不会触发回填。

**示例**

您已将包含10个配置文件的受众激活到流目标。

在激活受众后，您意识到需要更改受众配置，因此您需要停用受众并更改其填充标准，从而形成具有100个配置文件的受众群体。

您将更新的受众重新激活到同一目标，但由于没有触发回填，因此您的目标不会收到额外的90个配置文件。

**解决方案**

为确保将所有配置文件都发送到您的目标，您必须使用新配置创建新受众，然后将其激活到您的目标。

+++


## [!DNL Facebook Custom Audiences] {#facebook-faq}

### 在中激活受众之前，我需要做什么？ [!DNL Facebook Custom Audiences]？

+++回答在将受众发送至 [!DNL Facebook]，确保您满足以下要求：

* 您的 [!DNL Facebook] 用户帐户必须具有 **[!DNL Manage campaigns]** 为您计划使用的Ad帐户启用的权限。
* 此 **Adobe Experience Cloud** 必须将商业帐户作为广告合作伙伴添加到您的 [!DNL Facebook Ad Account]. 使用 `business ID=206617933627973`。请参阅 [将合作伙伴添加到您的业务经理](https://www.facebook.com/business/help/1717412048538897) 有关详细信息，请参阅Facebook文档。
  >[!IMPORTANT]
  >
  > 配置Adobe Experience Cloud的权限时，必须启用 **管理营销活动** 许可。 [!DNL Adobe Experience Platform] 集成要求具备此权限。
* 阅读并签署 [!DNL Facebook Custom Audiences] 服务条款。 为此，请转到 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中 `accountID` 是您的 [!DNL Facebook Ad Account ID]。
+++

### 是否需要向我的页面添加任何应用程序或像素？ [!DNL Facebook] 广告商帐户？

+++答案否。 由于这不是基于像素的集成，因此无需向广告商帐户中添加任何像素。
+++

### facebook需要多长时间来处理来自Adobe Experience Platform的信息？

+++截至2021年3月的答复， [!DNL Facebook Custom Audiences] 需要长达一小时来处理从收到的信息 [!DNL Platform].
+++

### 我可以使用 [!DNL Facebook Custom Audiences] 用于其他中的受众定位 [!DNL Facebook] 应用程序，例如 [!DNL Instagram]？

+++Amswer您可以使用 [!DNL Facebook Custom Audiences] 适用于受众定位的Facebook系列应用程序受支持的目标 [!DNL Facebook Custom Audiences]，包括 [!DNL Facebook]， [!DNL Instagram]， [!DNL Audience Network]、和 [!DNL Messenger]. 中的版面级别会显示广告商要在其上运行营销活动的所选应用程序。 [!DNL Facebook Ads Manager].
+++

### 两者之间有何区别？ [!DNL Facebook Custom Audiences] 连接和 [!DNL Facebook Pixel] 扩展？

+++回答 [!DNL Facebook Custom Audiences] 连接使用 [!DNL Platform] 将受众发送到时的身份 [!DNL Facebook]，而 [[!DNL Facebook Pixel] 连接](../destinations/catalog/advertising/facebook-pixel.md) 使用 [!DNL Facebook] 集成在网站中的像素。

这两种集成是互补的，您可以同时使用这两种集成来确保更好的受众覆盖。例如，您可以使用 [!DNL Facebook Pixel] 用于潜在访客且尚未创建帐户的扩展，而 [!DNL Facebook Custom Audiences] 可以帮助您定位现有客户，基于 [!DNL Platform] 身份。
+++

### Adobe Experience Platform是否与集成 [!DNL Facebook Custom Audiences] 支持在用户不再符合受众资格时取消其受众资格?**

+++回答是，该集成支持从删除用户 [!DNL Facebook Custom Audiences] 当他们不再符合条件时。
+++

### 在发送受众数据到之前，我应如何对其进行哈希处理 [!DNL Facebook]？

+++回答
[!DNL Facebook] 要求不发送明确的个人身份信息(PII)。 因此，受众激活到 [!DNL Facebook] 可以中断连接 *哈希* 标识符，例如电子邮件地址或电话号码。

有关ID匹配要求的详细说明，请参阅 [ID匹配要求](catalog/social/facebook.md#id-matching-requirements).
+++

### 我可以在哪种身份中激活 [!DNL Facebook Custom Audiences]？

+++回答
[!DNL Facebook Custom Audiences] 支持激活以下身份：经过哈希处理的电子邮件、经过哈希处理的电话号码， [!DNL GAID]， [!DNL IDFA]和自定义外部ID。
+++

### 我能否在Platform UI中为单独的Facebook帐户创建多个Facebook目标？

+++回答是。 Experience Platform中的Facebook目标与Facebook中的广告帐户的比率是1:1。 您可以为公司中的每个Facebook广告帐户创建单独的Facebook目标。 请遵循 [目标连接教程](/help/destinations/ui/connect-destination.md) 并为Platform UI中的每个新Facebook目标连接到单独的Facebook帐户。 您可以连接到的Facebook广告帐户数量没有限制。
+++

## Google 客户匹配 {#google-customer-match}

### 将受众导出到Google Customer Match时，为什么在Google界面中的受众名称末尾附加了额外的数字？

+++回答Google要求受众名称是唯一的。 您所看到的数字是 [UNIX时间戳](https://www.unixtimestamp.com/) 如果将同一受众映射到多个Google目标，则会附加这些受众以保持受众名称唯一。
+++

## linkedIn匹配的受众 {#linkedin}

### 是否需要向我的页面添加任何应用程序或像素？ [!DNL LinkedIn] 广告商帐户？

+++答案否。 由于这不是基于像素的集成，因此无需向广告商帐户中添加任何像素。
+++

### 在中激活受众之前，我需要做什么？ [!DNL LinkedIn Matched Audiences]？

+++在使用之前，请回答 [!UICONTROL linkedIn匹配的受众] 目标，确保 [!DNL LinkedIn Campaign Manager] 帐户具有 [!DNL Creative Manager] 权限级别或更高。

要了解如何编辑您的 [!DNL LinkedIn Campaign Manager] 用户权限，请参阅 [添加、编辑和删除广告帐户的用户权限](https://www.linkedin.com/help/lms/answer/5753) 请参阅LinkedIn文档。
+++

### 在发送受众数据到之前，我应如何对其进行哈希处理 [!DNL LinkedIn]？

+++回答
[!DNL LinkedIn] 要求不发送明确的个人身份信息(PII)。 因此，受众激活到 [!DNL LinkedIn] 可以中断连接 *哈希* 标识符，例如电子邮件地址或电话号码。

有关ID匹配要求的详细说明，请参阅 [ID匹配要求](catalog/social/linkedin.md#id-matching-requirements).
+++

### 我可以在哪种身份中激活 [!DNL LinkedIn]？

+++回答
[!DNL LinkedIn Matched Audiences] 支持激活以下标识：哈希电子邮件， [!DNL GAID]、和 [!DNL IDFA].
+++

## 通过Adobe Target和自定义个性化目标实现同一页面和下一页面个性化 {#same-next-page-personalization}

### 是否需要使用Experience PlatformWeb SDK将受众和属性发送到Adobe Target？

+++回答否， [Web SDK](../edge/home.md) 无需将受众激活到 [Adobe Target](catalog/personalization/adobe-target-connection.md).

但是，如果 [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=en) 代替Web SDK，仅支持下一会话个性化。

对象 [同一页面和下一页面个性化](ui/activate-edge-personalization-destinations.md) 用例，您必须使用 [Web SDK](../edge/home.md) 或 [边缘网络服务器API](../server-api/overview.md). 请参阅相关文档 [将受众激活到Edge目标](ui/activate-edge-personalization-destinations.md) 以了解更多实施详细信息。
+++

### 我可以从Real-time Customer Data Platform发送到Adobe Target或自定义个性化目标的属性数量是否存在限制？

+++回答是，将受众激活到Adobe Target或自定义个性化目标时，同页和下一页个性化用例最多支持每个沙盒30个属性。 有关激活护栏的更多信息，请参阅 [护栏文档](guardrails.md#edge-destinations-activation).
+++

### 激活支持哪些类型的属性（例如数组、映射等）？

+++答案目前，仅支持静态的单值属性，例如 `person.name.firstName`. 当前不支持数组属性。
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### 在Experience Platform中创建受众后，需要多长时间才能将该受众用于Edge分段用例？

+++应答受众定义将传播到 [边缘网络](../edge/home.md) 最多一小时内。 但是，如果在这第一个小时内激活了受众，则可能会错过一些符合受众条件的访客。
+++

### 在Adobe Target中，我可以在哪里查看激活的属性？

+++应答属性将在Target中的 [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) 和 [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html?lang=zh-Hans) 选件。
+++

### 我是否可以创建没有数据流的目标，然后在以后将数据流添加到同一目标？

+++答案当前不支持通过目标UI执行此操作。 如果在此情况下您需要帮助，请联系您的Adobe代表。
+++

### 如果我删除Adobe Target目标，会发生什么情况？

+++答案当您删除目标时，所有在目标下映射的受众和属性都会从Adobe Target中删除，同时也会从Edge Network中删除。
+++

### 集成是否可以使用Edge Network服务器API？

+++答案是，边缘网络服务器API可与自定义个性化目标配合使用。 由于配置文件属性可能包含敏感数据，为了保护此数据，自定义个性化目标要求您使用Edge Network服务器API进行数据收集。 此外，所有API调用都必须在 [已验证的上下文](../server-api/authentication.md).
+++

### 我只能有一个边缘活动合并策略。 我是否可以生成使用其他合并策略的受众，并且仍然将这些受众作为流受众发送到Adobe Target？

+++答案否。 要激活到Adobe Target的所有受众都必须使用active-on-edge [合并策略](../profile/merge-policies/ui-guide.md).
+++

### 数据使用标签和执行(DULE)以及同意策略是否已实施？

+++回答是。 此 [数据治理和同意策略](../data-governance/home.md) 创建并与所选营销操作相关联将控制所选属性的激活。
+++
