---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；個人設定檔；欄位；結構；結構；忠誠度詳細資料；結構描述設計；欄位群組；欄位群組；
solution: Experience Platform
title: 熟客方案詳細資料結構欄位群組
description: 本檔案提供「熟客方案詳細資料」結構欄位群組的概觀。
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 2%

---

# [!UICONTROL 熟客方案細節] 結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../name-updates.md) 以取得詳細資訊。

[!UICONTROL 熟客方案細節] 是的標準結構描述欄位群組 [[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md). 欄位群組提供單一物件型別欄位， `loyalty`，會擷取和客戶忠誠度計畫中的個人會籍相關的資訊。

![](../../images/field-groups/loyalty-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `pointsExpiration` | 物件陣列 | 列出任何即將過期的熟客點數（或熟客點數群組），以及到期日期。 每個陣列專案都必須是包含下列兩個屬性的物件： <ul><li>`pointsExpirationDate`：點到期的ISO 8601日期時間。</li><li>`pointsExpiring`：截至相關到期日的點數餘額。</li></ul> |
| `joinDate` | 日期時間 | 個人加入忠誠度計畫的ISO 8601日期時間。 |
| `loyaltyID` | 字串陣列 | 代表與熟客方案會員相關聯的熟客方案ID。 |
| `points` | 双精度 | 目前忠誠會員的忠誠度積分或獎勵餘額。 |
| `pointsRedeemed` | 双精度 | 忠誠會員已套用於購買或以其他方式兌換的積分數。 |
| `program` | 字符串 | 個人註冊的熟客方案名稱。 |
| `status` | 字符串 | 個人忠誠度會籍的目前狀態，例如 `active`， `disabled`，或 `suspended`. |
| `tier` | 字符串 | 擷取人員註冊的熟客方案層級。 |
| `upgradeDate` | 字符串 | 忠誠會員升級至其最近層級的日期。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
