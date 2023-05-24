---
title: 標籤和事件轉送的發行說明
description: 有关 Adobe Experience Platform 中的标记和事件转发的最新发行说明。
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 626330395c2d6b813d5d2157e92ada77ab4f96b1
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 3%

---

# 標籤和事件轉送的發行說明

>[!IMPORTANT]
>
>往前看，本頁將不再提供標籤和事件轉送發行說明。 請參閱最新版本 [Adobe Experience Platform發行說明](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=en#data-collection) 以取得詳細的標籤和事件轉送更新。

## 2023 年 4 月 26 日

* **OAuth JWT密碼**：此 [OAuth JWT密碼](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) 可讓客戶使用Adobe和Google服務權杖，在事件轉送中支援伺服器對伺服器的互動。

下列新擴充功能已發行：

* **[!DNL Pinterest Conversions API]擴充功能**：此 [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) 事件轉送擴充功能可讓您運用Adobe Experience Platform Edge Network中擷取的資料，並將其傳送至 [!DNL Pinterest] 以伺服器端事件的形式使用 [!DNL Pinterest Conversions API].

## 2023 年 3 月 29 日

**Quick Stark工作流程（測試版）**

從資料收集首頁畫面存取「快速入門」底下的全新快速入門工作流程！ 以下工作流程現在可作為公開測試版提供給客戶。
* **[中繼轉換API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start)**：事件轉送客戶可以快速收集並轉送事件資料，從伺服器端到中繼只要幾個簡單步驟就能進行廣告轉換。
* **[行動SDK](https://developer.adobe.com/client-sdks/documentation/)**：客戶只需幾個簡單步驟，即可快速實作Mobile SDK並驗證基本行動事件。

已發行新的擴充功能：

* **[!DNL Braze]事件轉送擴充功能**：此 [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 事件轉送擴充功能可讓您運用Adobe Experience Platform Edge Network中擷取的資料，並將其傳送至 [!DNL Braze] 以伺服器端事件的形式使用 [!DNL Braze] 使用者追蹤API。
* **[Epsilon事件API] 事件轉送擴充功能**：此 [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 擴充功能可讓您運用事件轉送，擷取Adobe Experience Platform Edge Network中的事件資訊，並將其傳送至 [!DNL Epsilon] 使用 [!DNL Epsilon] 事件API。
* **[!DNL Mixpanel]事件轉送擴充功能**：此 [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 擴充功能可讓您運用事件轉送，擷取Adobe Experience Platform Edge Network中的事件資訊，並將其傳送至 [!DNL Mixpanel] 使用追蹤事件API。

## 2023 年 1 月 25 日

* **新主畫面**：資料收集UI首頁已更新，加入實用的入門資訊和連結，以簡化生產力。 这包括：
   1. 開始使用的檔案和建議工作流程
   1. 最近使用的屬性、規則和資料元素
   1. 熱門擴充功能
   1. 包含快速安裝功能的新擴充功能更新
* **傳送資料至 [!DNL Google Ads] 使用事件轉送**：您現在可以使用 [[!DNL Google Ads Enhanced Conversions] API擴充功能](../extensions/server/google-ads-enhanced-conversions/overview.md) 用於事件轉送，結合 [Google Oauth 2秘密](../ui/event-forwarding/secrets.md#google-oauth2)，以安全地傳送伺服器端資料至 [!DNL Google Ads] 即時。

## 2022 年 11 月 23 日

* **[!DNL AWS]事件轉送的擴充功能**：您現在可以將資料傳送至 [!DNL Amazon Web Services] ([!DNL AWS])使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 副檔名。 請參閱 [[!DNL AWS] 擴充功能概觀](../../tags/extensions/server/aws/overview.md) 以取得詳細資訊。
* **[!DNL Google Ads Enhanced Conversions]事件轉送的擴充功能**：您現在可以將轉換資料傳送至 [!DNL Google Ads] 使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 副檔名。 請參閱 [[!DNL Google Ads Enhanced Conversions] 擴充功能概觀](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 以取得詳細資訊。
* **[!DNL Microsoft Azure]事件轉送的擴充功能**：您現在可以將資料傳送至 [!DNL Microsoft Azure] 使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 副檔名。 請參閱 [[!DNL Microsoft Azure] 擴充功能概觀](../../tags/extensions/server/azure/overview.md) 以取得詳細資訊。

## 2022 年 10 月 26 日

* **資料串流的敏感資料處理**：資料串流現在運用數種平台技術，可適當處理由健康保險便利與責任法案(HIPAA)等法規強制執行的敏感資料。 請參閱以下小節： [處理資料串流中的敏感資料](../../edge/datastreams/overview.md#sensitive) 以取得詳細資訊。
* **[!DNL Splunk]事件轉送的擴充功能**：您現在可以將資料傳送至 [!DNL Splunk] 使用 [事件轉送](../ui/event-forwarding/overview.md) 副檔名。 請參閱 [[!DNL Splunk] 擴充功能概觀](../extensions/server/splunk/overview.md) 以取得詳細資訊。
* **[!DNL Zendesk]事件轉送的擴充功能**：您現在可以將資料傳送至 [!DNL Zendesk] 使用 [事件轉送](../ui/event-forwarding/overview.md) 副檔名。 請參閱 [[!DNL Zendesk] 擴充功能概觀](../extensions/server/zendesk/overview.md) 以取得詳細資訊。

## 2022 年 9 月 28 日

* **Adobe Experience Platform左側導覽整合**：先前專屬資料收集UI的所有功能（包括標籤和事件轉送）現在也可透過Experience PlatformUI中類別底下的左側導覽取得 **[!UICONTROL 資料彙集]**. 如此一來，當您在Platform中使用資料收集功能時，便不需要在UI之間切換。
* **標籤和事件轉送中的使用者歸因**：現在，在標籤和事件轉送中列出可用屬性時，每個列出的屬性都會顯示上次更新時間以及由誰更新。
* **[[!DNL Snap Conversions API] 擴充功能](https://exchange.adobe.com/apps/ec/108550) 用於事件轉送**：您現在可以將資料傳送至 [!DNL Snapchat Conversions API] 使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 副檔名。 有關如何驗證和使用API的詳細資訊，請參閱 [[!DNL Snapchat Marketing API] 檔案](https://marketingapi.snapchat.com/docs/conversion.html).

## 2022 年 7 月 27 日

* 現在可透過Adobe Experience Platform資料收集資訊卡底下的Adobe Admin Console管理標籤和事件轉送功能的存取。 請參閱指南： [資料彙集許可權](../../collection/permissions.md) 以取得詳細資訊。
* 支援Internet Explorer 10和11 [已棄用](../ie-deprecation.md).

## 2022 年 6 月 22 日

已發行新的擴充功能：

* [Google Data Layer標籤擴充功能](../extensions/client/google-data-layer/overview.md)：可讓您在標籤實作中使用Google資料層。
* [Google Ads增強型轉換事件轉送擴充功能](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html)：可讓您即時增強Google Ads轉換。
* [Mailchimp事件轉送擴充功能](../extensions/server/mailchimp/overview.md)：傳送事件至Mailchimp行銷API，其可觸發Mailchimp行銷活動、歷程或交易的電子郵件。