---
keywords: 目标；问题；常见问题解答；常见问题解答；目标常见问题解答
title: 常见问题解答
description: 关于Adobe Experience Platform目标最常见问题的解答
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 1%

---

# 常见问题解答 {#faq}

## 概述 {#overview}

本文档提供有关Adobe Experience Platform目标的常见问题解答。 有关其他[!DNL Experience Platform]服务（包括在所有[!DNL Experience Platform] API中遇到的服务）的问题和疑难解答，请参阅[Experience Platform疑难解答指南](../landing/troubleshooting.md)。

## 一般目标问题 {#general}

### 为什么在Experience Platform UI和导出的CSV文件中看到不同的配置文件计数？

+++回答
由于Experience Platform执行分段的方式，这是正常行为。

流式分段会更新一天中流式受众的个人资料计数，而批量分段每24小时更新一次批量受众的个人资料计数。

当受众导出计划与分段计划不同时，UI和导出的[!DNL CSV]文件之间的配置文件计数将不同，尤其是当涉及流受众时。

有关更多详细信息，请参阅[分段服务文档](../segmentation/home.md)。
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

### 从目标中删除受众时，是否有任何发送到目标的信号指示该受众已删除？

+++回答

不需要，Experience Platform目标与目标系统的客户实例之间没有依赖关系。 在接收方，目标系统将看到的唯一指示是它停止接收该受众数据。

+++

<!--
## [!DNL Experience Cloud Audiences] {#eca-faq}

### What are the differences between the Experience Cloud Audiences and Adobe Target destinations?

+++Answer

See the table below for a feature comparison between the Experience Cloud Audiences and Adobe Target destinations.

||Experience Cloud Audiences|Adobe Target|
|---|---|---|
| **Supported Experience Cloud apps** | Supports audience activation to Audience Manager, Adobe Target, Adobe Analytics, Advertising Cloud, Marketo, Adobe Campaign | Supports audience activation only to Adobe Target |
| **Supports audience activation** | ✓ | ✓ |
| **Supports attribute activation** | X | ✓ |
| **Latency** | Profiles begin activating in 6 hours. Full population is visible in 48 hours​. |Depends on implementation​ type. <ul><li>Web SDK enables same-page/next-page​ personalization.</li><li>AT.js enables next-session personalization.</li></ul> |
| **DULE support** | ✓ | ✓ |
| **Marketing actions support** | ✓ | ✓ |
| **Supported IDs** | [!DNL ECID], [!DNL GAID], [!DNL IDFA], [!DNL email_lc_sha256] | Any ID type |
| **Sandbox support** | One sandbox | Multiple sandboxes |
| **Consent support** | X | Yes. Requires Privacy & Security Shield. |
| **Edge segmentation support** | Supports activation of edge audiences. Does not support edge segmentation. | Supports edge segmentation and activation of edge audiences. |
| **Supported audiences** | All types of audiences  | Edge merge policy required for activation.|

+++

-->

## [!DNL Facebook Custom Audiences] {#facebook-faq}

### 在[!DNL Facebook Custom Audiences]中激活受众之前，我需要做什么？

+++回答
在将受众发送到[!DNL Facebook]之前，请确保您满足以下要求：

* 您的[!DNL Facebook]用户帐户必须为计划使用的广告帐户启用&#x200B;**[!DNL Manage campaigns]**&#x200B;权限。
* **Adobe Experience Cloud**&#x200B;商业帐户必须添加为您[!DNL Facebook Ad Account]中的广告合作伙伴。 使用`business ID=206617933627973`。 有关详细信息，请参阅Facebook文档中的[将合作伙伴添加到业务管理器](https://www.facebook.com/business/help/1717412048538897)。

  >[!IMPORTANT]
  >
  > 配置Adobe Experience Cloud的权限时，必须启用&#x200B;**管理营销活动**&#x200B;权限。 [!DNL Adobe Experience Platform]集成需要此项。
* 阅读并签署[!DNL Facebook Custom Audiences]服务条款。 为此，请转到`https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中`accountID`是您的[!DNL Facebook Ad Account ID]。
+++

### 是否需要向我的[!DNL Facebook]广告商帐户添加任何应用或像素？

+++回答
不是。由于这不是基于像素的集成，因此无需向广告商帐户中添加任何像素。
+++

### Facebook需要多长时间才能处理来自Adobe Experience Platform的信息？

+++回答
自2021年3月起，[!DNL Facebook Custom Audiences]需要长达一小时来处理从[!DNL Experience Platform]接收的信息。
+++

### 我能否将[!DNL Facebook Custom Audiences]用于其他[!DNL Facebook]应用（如[!DNL Instagram]）中的受众定位？

+++昂斯韦尔
您可以使用[!DNL Facebook Custom Audiences]目标在[!DNL Facebook Custom Audiences]支持的Facebook应用系列中定位受众，包括[!DNL Facebook]、[!DNL Instagram]、[!DNL Audience Network]和[!DNL Messenger]。 [!DNL Facebook Ads Manager]中的版面级别显示广告商要在其上运行营销活动的所选应用程序。
+++

### [!DNL Facebook Custom Audiences]连接与[!DNL Facebook Pixel]扩展之间有何区别？

+++回答
在向[!DNL Facebook Custom Audiences]发送受众时，[!DNL Experience Platform]连接使用[!DNL Facebook]标识，而[[!DNL Facebook Pixel] 连接](../destinations/catalog/advertising/facebook-pixel.md)使用集成在网站中的[!DNL Facebook]像素。

这两种集成是互补的；您可以同时使用这两种集成来确保更好的受众覆盖。 例如，您可以使用[!DNL Facebook Pixel]扩展来查找尚未创建帐户的网站访客，而[!DNL Facebook Custom Audiences]可以帮助您根据[!DNL Experience Platform]身份定位现有客户。
+++

### Adobe Experience Platform与[!DNL Facebook Custom Audiences]的集成是否支持在用户不再符合受众资格时取消其受众资格?**

+++回答
是，该集成支持在用户不再符合条件时将其从[!DNL Facebook Custom Audiences]中删除。
+++

### 在将受众数据发送到[!DNL Facebook]之前，我应该如何对其进行哈希处理？

+++回答
[!DNL Facebook]要求不发送明确的个人身份信息(PII)。 因此，激活到[!DNL Facebook]的受众可以用&#x200B;*散列的*&#x200B;标识符作为键值，例如电子邮件地址或电话号码。

有关ID匹配要求的详细说明，请参阅[ID匹配要求](catalog/social/facebook.md#id-matching-requirements)。
+++

### 我可以在[!DNL Facebook Custom Audiences]中激活哪种标识？

+++回答
[!DNL Facebook Custom Audiences]支持激活以下标识：哈希电子邮件、哈希电话号码、[!DNL GAID]、[!DNL IDFA]和自定义外部ID。
+++

### 我能否在Experience Platform UI中为单独的Facebook帐户创建多个Facebook目标？

+++回答
可以。Experience Platform中的Facebook目标与Facebook中的广告帐户相差1:1。 您可以为公司中的每个Facebook广告帐户创建单独的Facebook目标。 按照[目标连接教程](/help/destinations/ui/connect-destination.md)进行操作，并在Experience Platform UI中为每个新的Facebook目标连接到单独的Facebook帐户。 您可以连接到的Facebook广告帐户数量没有限制。
+++

## Google 目标客户匹配功能 {#google-customer-match}

### 将受众导出到Google Customer Match时，为什么在Google界面中的受众名称末尾附加了额外的数字？

+++回答
Google要求受众名称是唯一的。 您看到的数字是[UNIX时间戳](https://www.unixtimestamp.com/)，如果将同一受众映射到多个Google目标，则会附加这些数字以保持受众名称的唯一性。
+++

## LinkedIn匹配的受众 {#linkedin}

### 是否需要向我的[!DNL LinkedIn]广告商帐户添加任何应用或像素？

+++回答
不是。由于这不是基于像素的集成，因此无需向广告商帐户中添加任何像素。
+++

### 在[!DNL LinkedIn Matched Audiences]中激活受众之前，我需要做什么？

+++回答
在使用[!UICONTROL LinkedIn Matched Audience]目标之前，请确保您的[!DNL LinkedIn Campaign Manager]帐户具有[!DNL Creative Manager]权限级别或更高。

要了解如何编辑您的[!DNL LinkedIn Campaign Manager]用户权限，请参阅LinkedIn文档中的[添加、编辑和删除Advertising帐户的用户权限](https://www.linkedin.com/help/lms/answer/5753)。
+++

### 在将受众数据发送到[!DNL LinkedIn]之前，我应该如何对其进行哈希处理？

+++回答
[!DNL LinkedIn]要求不发送明确的个人身份信息(PII)。 因此，激活到[!DNL LinkedIn]的受众可以用&#x200B;*散列的*&#x200B;标识符作为键值，例如电子邮件地址或电话号码。

有关ID匹配要求的详细说明，请参阅[ID匹配要求](catalog/social/linkedin.md#id-matching-requirements)。
+++

### 我可以在[!DNL LinkedIn]中激活哪种标识？

+++回答
[!DNL LinkedIn Matched Audiences]支持激活以下标识：哈希电子邮件、[!DNL GAID]和[!DNL IDFA]。

+++

## 通过Adobe Target和自定义Personalization目标实现同一页面和下一页面个性化 {#same-next-page-personalization}

### 是否需要使用Experience Platform Web SDK将受众和属性发送到Adobe Target？

+++回答
不需要，不需要Web SDK才能将受众激活到[Adobe Target](catalog/personalization/adobe-target-connection.md)。

但是，如果使用[[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html)而不是Web SDK，则仅支持下一会话个性化。

对于[同一页面和下一页面个性化](ui/activate-edge-personalization-destinations.md)用例，您必须使用Web SDK或[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)。 有关更多实施详细信息，请参阅有关[将受众激活到边缘目标](ui/activate-edge-personalization-destinations.md)的文档。
+++

### 我可以从Real-time Customer Data Platform发送到Adobe Target或自定义Personalization目标的属性数量是否存在限制？

+++回答
支持，在将受众激活到Adobe Target或自定义Personalization目标时，同页和下一页个性化用例最多支持每个沙盒30个属性。 请参阅[护栏文档](guardrails.md#edge-destinations-activation)中有关激活护栏的详细信息。
+++

### 激活支持哪些类型的属性（例如数组、映射等）？

+++回答
目前，仅支持静态的单值属性，如`person.name.firstName`。 当前不支持数组属性。
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### 在Experience Platform中创建受众后，需要多长时间才能将该受众用于Edge分段用例？

+++回答
受众定义最多可在一小时内传播到Edge Network。 但是，如果在这第一个小时内激活了受众，则可能会错过一些符合受众条件的访客。
+++

### 在Adobe Target中，我可以在哪里查看激活的属性？

+++回答
可在[JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html?lang=zh-Hans)和[HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html?lang=zh-Hans)选件的Target中使用属性。
+++

### 我是否可以创建没有数据流的目标，然后在以后将数据流添加到同一目标？

+++回答
当前不支持通过目标UI执行此操作。 如果在此情况下您需要帮助，请联系您的Adobe代表。
+++

### 如果我删除Adobe Target目标，会发生什么情况？

+++回答
当您删除目标时，所有在目标下映射的受众和属性都将从Adobe Target中删除，并且也会从Edge Network中删除。
+++

### 集成是否可以使用Edge Network API？

+++回答
是，Edge Network API可与自定义Personalization目标配合使用。 由于配置文件属性可能包含敏感数据，为了保护此数据，自定义Personalization目标要求您使用Edge Network API进行数据收集。 此外，所有API调用都必须在[经过身份验证的上下文](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication/)中进行。
+++

### 我只能有一个边缘活动合并策略。 我是否可以生成使用其他合并策略的受众，并且仍然将这些受众作为流受众发送到Adobe Target？

+++回答
不是。您要激活到Adobe Target的所有受众都必须使用active-on-edge [合并策略](../profile/merge-policies/ui-guide.md)。
+++

### 数据使用标签和执行(DULE)以及同意策略是否已实施？

+++回答
可以。创建并与所选营销操作关联的[数据管理和同意策略](../data-governance/home.md)将控制所选属性的激活。
+++

### [!DNL Adobe Target]和[!DNL Custom Personalization]目标是否符合[!DNL HIPAA]？

+++回答
[!DNL Adobe Target]与[!DNL HIPPA][[!DNL Adobe Healthcare Shield]不符合](https://business.adobe.com/cn/solutions/industries/healthcare.html)。 在通过[!DNL HIPPA]或[!DNL Adobe Target]目标使用边缘个性化之前，客户应当与自己的法律团队确认[!DNL Custom Personalization]对自定义优化渠道的准备情况。

对于需要大规模应用同意策略管理的用例，客户必须购买[!DNL Adobe Privacy & Security Shield]。 [!DNL Adobe Privacy & Security Shield]功能作为高级功能套件销售，不能单独购买。

此服务包括客户管理的密钥和提升的阈值，以管理客户数据生命周期。

[!DNL Adobe Target]和[!DNL Custom Personalization]目标与[Experience Platform数据使用标签](../data-governance/labels/overview.md)和[同意策略实施服务](../data-governance/enforcement/overview.md)集成。 这些功能适用于所有客户。




+++

