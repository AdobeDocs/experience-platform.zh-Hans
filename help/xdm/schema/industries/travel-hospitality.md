---
solution: Experience Platform
title: 旅遊業及旅館業資料模型ERD
description: 檢視實體關係圖(ERD)，其說明適用於旅遊業和酒店業的標準化資料模型，且與Experience Data Model (XDM)相容，以便在Adobe Experience Platform中使用。
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 3%

---

# [!UICONTROL 旅遊業及旅館業] 產業資料模型ERD

下列實體關係圖(ERD)代表旅遊業及旅館業的標準化資料模型。 ERD會刻意以非標準化方式呈現，並考量資料如何儲存於Adobe Experience Platform。

>[!NOTE]
>
>說明的ERD是您應如何針對此產業使用案例建立資料模型的建議。 若要在Platform中使用此資料模型，您必須自行建構建議的結構描述及其關係。 請參閱管理指南 [結構描述](../../ui/resources/schemas.md) 和 [關係](../../tutorials/relationship-ui.md) （在UI中）以取得詳細資訊。

使用下列圖例來解譯此ERD：

* 中顯示的每個實體都是以基礎實體為基礎 [體驗資料模型(XDM)類別](../composition.md#class).
* 對於指定的實體，每個列都標示在 **粗體** 代表欄位群組或資料型別，其提供的相關欄位會以無粗體文字列示於下方。
* 指定實體的最重要欄位會以紅色反白顯示。
* 所有可用於識別個別客戶的屬性都會標示為「身分」，而其中一個屬性會標示為「主要身分」。
* 實體關係會標示為非相依關係，因為Cookie型事件通常無法判斷執行交易的人或個人。

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>體驗事件實體包含「_ID」欄位，代表唯一識別碼(`_id`)屬性，由XDM體驗事件類別提供。 參閱參考檔案： [XDM ExperienceEvent](../../classes/experienceevent.md) 以取得此值預期值的詳細資訊。

## [!UICONTROL 旅遊業及旅館業] 使用案例

下表概述旅遊業及旅館業幾個常見使用案例的建議類別和結構描述欄位群組。

| 用例 | 建議的類別和欄位群組 |
| --- | --- |
| 向即將預訂飯店的市內賓客和賓客交叉銷售餐飲和其他常駐景點。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[預訂詳細資料](../../field-groups/event/reservation-details.md)</li><li>[住宿預訂](../../field-groups/event/lodging-reservation.md)</li><li>[餐飲預訂](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM 个人资料](../../classes/individual-profile.md)**:<ul><li>[人口統計細節](../../field-groups/profile/demographic-details.md)</li><li>[個人聯絡詳細資訊](../../field-groups/profile/personal-contact-details.md)</li><li>[工作聯絡詳細資訊](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 將餐飲及其他住家景點追加銷售給市場內的賓客和即將預訂旅館的賓客。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[預訂詳細資料](../../field-groups/event/reservation-details.md)</li><li>[餐飲預訂](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM 个人资料](../../classes/individual-profile.md)**:<ul><li>[人口統計細節](../../field-groups/profile/demographic-details.md)</li><li>[個人聯絡詳細資訊](../../field-groups/profile/personal-contact-details.md)</li><li>[工作聯絡詳細資訊](../../field-groups/profile/work-contact-details.md)</li><li>[熟客方案細節](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 將飯店和其他住家景點追加銷售給市場內的賓客和即將預訂飯店的賓客。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[預訂詳細資料](../../field-groups/event/reservation-details.md)</li><li>[住宿預訂](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[XDM 个人资料](../../classes/individual-profile.md)**:<ul><li>[人口統計細節](../../field-groups/profile/demographic-details.md)</li><li>[個人聯絡詳細資訊](../../field-groups/profile/personal-contact-details.md)</li><li>[工作聯絡詳細資訊](../../field-groups/profile/work-contact-details.md)</li><li>[熟客方案細節](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 向即將預訂飯店的市內賓客和賓客追加銷售航班和其他常駐景點。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[預訂詳細資料](../../field-groups/event/reservation-details.md)</li><li>[航班預訂](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[XDM 个人资料](../../classes/individual-profile.md)**:<ul><li>[人口統計細節](../../field-groups/profile/demographic-details.md)</li><li>[個人聯絡詳細資訊](../../field-groups/profile/personal-contact-details.md)</li><li>[工作聯絡詳細資訊](../../field-groups/profile/work-contact-details.md)</li><li>[熟客方案細節](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
