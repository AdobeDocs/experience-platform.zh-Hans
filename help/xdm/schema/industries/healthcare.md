---
title: 醫療保健產業資料模型ERD
description: 檢視實體關係圖(ERD)，該圖描述醫療保健行業的標準化資料模型。 此資料模型與Adobe Experience Platform中使用的Experience Data Model (XDM)相容。
exl-id: ebcf97ec-f5a4-46e5-b1ad-c80d55aa2c6e
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 4%

---

# [!UICONTROL 醫療保健] 產業資料模型ERD

下列實體關係圖(ERD)代表醫療保健行業的標準化資料模型。 ERD會刻意以非標準化方式呈現，並考量資料如何儲存於Adobe Experience Platform。

>[!NOTE]
>
>說明的ERD是您應如何針對此產業使用案例建立資料模型的建議。 若要在Platform中使用此資料模型，您必須自行建構建議的結構描述及其關係。 請參閱管理指南 [結構描述](../../ui/resources/schemas.md) 和 [關係](../../tutorials/relationship-ui.md) （在UI中）以取得詳細資訊。

使用下列圖例來解譯此ERD：

* 中顯示的每個實體都是以基礎實體為基礎 [體驗資料模型(XDM)類別](../composition.md#class).
* 對於指定的實體，每個列都標示在 **粗體** 代表欄位群組或資料型別，其提供的相關欄位會以無粗體文字列示於下方。
* 指定實體的最重要欄位會以紅色反白顯示。
* 所有可用於識別個別客戶的屬性都會標示為「身分」，而其中一個屬性會標示為「主要身分」。
* 實體關係會標示為非相依關係，因為Cookie型事件通常無法判斷執行交易的人或個人。

![此影像顯示醫療保健產業資料模型的實體關係圖](../../images/industries/healthcare.png)

>[!NOTE]
>
>每個實體都包含「_ID」欄位，代表唯一字串識別碼(`_id`)屬性。 此欄位用於追蹤個別記錄或事件的唯一性、防止資料重複，以及在下游服務中查閱該資料。 某些情況下， `_id` 可以是 [通用唯一識別碼(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全域唯一識別碼(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>請務必區分 **此欄位不代表與個人相關的身分**&#x200B;而是資料本身的記錄。 與個人、事件或企業實體相關的身分資料應委派至 [身分欄位](../composition.md#identity) 由相容的欄位群組所提供。

## [!UICONTROL 醫療保健] 使用案例

下表概述幾個常見醫療保健使用案例的建議類別和結構描述欄位群組。

| 用例 | 建議的類別和欄位群組 |
| --- | --- |
| 改善購買保險的消費者的數位贏取和體驗。 示例包括： <ul><li>當人們存取包含一般資訊（例如計畫、計畫名稱/層級、Medicaid、健康計畫等）的頁面時，請瞭解他們的行為以及他們想要什麼，以便傳送促銷電子郵件或在具有廣告的第三方平台上鎖定他們。</li><li>當人們搜尋心臟健康和疫苗資訊時，請傳送心臟健康的疫苗相關資訊，以建立品牌知名度或要求他們排程疫苗。</li></ul> | <ul><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 醫療保健會員詳細資訊]](../../field-groups/profile/healthcare-member-details.md)</li><li>建立於以下兩者之間的關聯性欄位： `planID` 屬性及使用的結構描述 [!UICONTROL 計畫] 類別。</li></ul></li><li>**[[!UICONTROL 付款人]](../../classes/payer.md)**</li><li>**[[!UICONTROL 规划]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 醫療保健計畫詳細資料]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 應用程式詳細資料]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL Sitetool詳細資料]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL  行銷活動行銷細節]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| 根據過去的線上行為和健康資料，透過目標定位廣告增加數位化患者的贏取。 | <ul><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 醫療保健會員詳細資訊]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 提供者]](../../classes/provider.md)**：<ul><li>[[!UICONTROL 醫療保健提供者]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 網頁詳細資訊]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 廣告詳細資料]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| 透過不同管道追蹤保險的行銷情況，以便瞭解客戶如何找到保險公司，進而改善健康計畫的註冊和帳戶建立作業。 | <ul><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 醫療保健會員詳細資訊]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 付款人]](../../classes/payer.md)**</li><li>**[[!UICONTROL 规划]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 醫療保健計畫詳細資料]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 網頁詳細資訊]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 廣告詳細資料]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| 避免醫療保險服務中斷。 | <ul><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 醫療保健會員詳細資訊]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 规划]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 醫療保健計畫詳細資料]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| 使用直接對客戶(DTC)廣告向供應商促銷藥物資訊。 | <ul><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 醫療保健會員詳細資訊]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 藥物]](../../classes/medication.md)**：<ul><li>[[!UICONTROL 醫療保健]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 網頁詳細資訊]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 廣告詳細資料]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
