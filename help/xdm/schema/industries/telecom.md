---
solution: Experience Platform
title: 電信產業資料模型ERD
description: 檢視實體關係圖(ERD)，此圖表說明電信業的標準化資料模型，與Experience Data Model (XDM)相容，以便用於Adobe Experience Platform。
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 2%

---

# [!UICONTROL 電信] 產業資料模型ERD

下列實體關係圖(ERD)代表電信行業的標準化資料模型。 ERD會刻意以非標準化方式呈現，並考量資料如何儲存於Adobe Experience Platform。

>[!NOTE]
>
>說明的ERD是您應如何針對此產業使用案例建立資料模型的建議。 若要在Platform中使用此資料模型，您必須自行建構建議的結構描述及其關係。 請參閱管理指南 [結構描述](../../ui/resources/schemas.md) 和 [關係](../../tutorials/relationship-ui.md) （在UI中）以取得詳細資訊。

使用下列圖例來解譯此ERD：

* 中顯示的每個實體都是以基礎實體為基礎 [體驗資料模型(XDM)類別](../composition.md#class).
* 對於指定的實體，每個列都標示在 **粗體** 代表欄位群組或資料型別，其提供的相關欄位會以無粗體文字列示於下方。
* 指定實體的最重要欄位會以紅色反白顯示。
* 所有可用於識別個別客戶的屬性都會標示為「身分」，而其中一個屬性會標示為「主要身分」。
* 實體關係會標示為非相依關係，因為Cookie型事件通常無法判斷執行交易的人或個人。


![](../../images/industries/telecom.png)

>[!NOTE]
>
>體驗事件實體包含「_ID」欄位，代表唯一識別碼(`_id`)屬性，由XDM體驗事件類別提供。 參閱參考檔案： [XDM ExperienceEvent](../../classes/experienceevent.md) 以取得此值預期值的詳細資訊。

## [!UICONTROL 電信] 使用案例

下表概述電信業幾個常見使用案例的建議類別和結構描述欄位群組。

| 用例 | 建議的類別和欄位群組 |
| --- | --- |
| 根據客戶目前的持有量及瀏覽行為，瞭解適合追加銷售或交叉銷售機會的客戶。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 追加銷售細節]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL 升級詳細資料]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 電信訂閱]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL 人口統計細節]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯絡詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| 透過相關廣告和自動個人化電子郵件，重新鎖定購物車放棄者。 在廣告轉換時抑制廣告。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 商務詳細資料]](../../field-groups/event/upsell-details.md) （擷取購物車放棄次數）</li></ul></li><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 電信訂閱]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL 人口統計細節]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯絡詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| 當客戶標籤為可能流失（根據員工互動或自動化機器學習演演算法）時，將客戶詳細資料傳送至數位和非數位頻道。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 行銷活動行銷細節]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL 管道詳細資料]](../../field-groups/event/channel-details.md)</li><li>包含個人化內容的自訂欄位群組</li></ul></li><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口統計細節]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯絡詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
