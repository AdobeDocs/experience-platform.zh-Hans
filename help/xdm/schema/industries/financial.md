---
solution: Experience Platform
title: 金融服務業資料模型ERD
description: 檢視實體關係圖(ERD)，該圖描述銀行、金融服務和保險(BFSI)行業的標準化資料模型。 此資料模型與Adobe Experience Platform中使用的Experience Data Model (XDM)相容。
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 3%

---

# [!UICONTROL 金融服務] 產業資料模型ERD

下列實體關係圖(ERD)代表銀行、金融服務和保險(BFSI)行業的標準化資料模型。 ERD會刻意以非標準化方式呈現，並考量資料如何儲存於Adobe Experience Platform。

>[!NOTE]
>
>說明的ERD是您應如何針對此產業使用案例建立資料模型的建議。 若要在Platform中使用此資料模型，您必須自行建構建議的結構描述及其關係。 請參閱管理指南 [結構描述](../../ui/resources/schemas.md) 和 [關係](../../tutorials/relationship-ui.md) （在UI中）以取得詳細資訊。

使用下列圖例來解譯此ERD：

* 中顯示的每個實體都是以基礎實體為基礎 [體驗資料模型(XDM)類別](../composition.md#class).
* 對於指定的實體，每個列都標示在 **粗體** 代表欄位群組或資料型別，其提供的相關欄位會以無粗體文字列示於下方。
* 指定實體的最重要欄位會以紅色反白顯示。
* 所有可用於識別個別客戶的屬性都會標示為「身分」，而其中一個屬性會標示為「主要身分」。
* 實體關係會標示為非相依關係，因為Cookie型事件通常無法判斷執行交易的人或個人。

![](../../images/industries/financial.png)

>[!NOTE]
>
>體驗事件實體包含「_ID」欄位，代表唯一識別碼(`_id`)屬性，由XDM體驗事件類別提供。 參閱參考檔案： [XDM ExperienceEvent](../../classes/experienceevent.md) 以取得此值預期值的詳細資訊。

## [!UICONTROL 金融服務] 使用案例

下表概述幾個常見財務使用案例的建議類別和結構描述欄位群組。

| 用例 | 建議的類別和欄位群組 |
| --- | --- |
| 透過全通道報告深入分析和自動化歷程，大規模推動偏好區段的個人化，以增加偏好獎勵計畫的註冊。 | <ul><li>**[[!UICONTROL 产品]](../../classes/product.md)**:<ul><li>[[!UICONTROL 產品類別]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 卡片動作]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 報價請求細節]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL 存款細節]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 管道詳細資料]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL 餘額轉帳]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口統計細節]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯絡詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 熟客方案細節]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 最佳化線上和離線頻道的跨頻道個人化。 | <ul><li>**[[!UICONTROL 产品]](../../classes/product.md)**:<ul><li>[[!UICONTROL 產品類別]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 管道詳細資料]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口統計細節]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯絡詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 熟客方案細節]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 透過使用從跨管道行為分析獲得的見解，識別可能導致新產品選件的產品使用模式，推動新的收入機會。 | <ul><li>**[[!UICONTROL 策略]](../../classes/policy.md)**</li><li>**[[!UICONTROL 产品]](../../classes/product.md)**:<ul><li>[[!UICONTROL 產品類別]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 卡片動作]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 支援網站搜尋]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL 存款細節]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 管道詳細資料]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口統計細節]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯絡詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 熟客方案細節]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
