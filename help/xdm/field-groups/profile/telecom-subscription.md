---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；個人設定檔；欄位；綱要；綱要；電信；訂閱；電信；綱要設計；欄位群組；欄位群組；
solution: Experience Platform
title: 電信訂閱結構描述欄位群組
description: 本檔案提供Telecom Subscription結構描述欄位群組的概觀。
exl-id: 00c20081-09d0-425c-9894-0f957558bd43
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 4%

---

# [!UICONTROL 電信訂閱] 結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../name-updates.md) 以取得詳細資訊。

[!UICONTROL 電信訂閱] 是的標準結構描述欄位群組 [[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md) 說明客戶的電信訂閱計畫，包括定價、套件和個別產品訂閱。

欄位群組提供單一物件型別欄位， `telecomSubscription`，其屬性如下所述。

![電信訂閱結構](../../images/field-groups/telecom-subscription/structure.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `internetSubscription` | 物件陣列 | 說明網際網路訂閱計畫細節，例如，資料上限、連線型別和速度細節。 請參閱 [以下區段](#internetSubscription) 以取得詳細資訊。 |
| `landlineSubscription` | 物件陣列 | 說明有線電話訂閱計畫詳細資料，包括選取的功能、分鐘數和撥號計畫。 請參閱 [以下區段](#landlineSubscription) 以取得詳細資訊。 |
| `mediaSubscription` | 物件陣列 | 說明媒體訂閱計畫詳細資料，包括頻道數量和包含的串流服務。 請參閱 [以下區段](#mediaSubscription) 以取得詳細資訊。 |
| `mobileSubscription` | 物件陣列 | 說明行動訂閱計畫詳細資料，包括線路數、資料費率、成本等。 請參閱 [以下區段](#mobileSubscription) 以取得詳細資訊。 |
| `primarySubscriber` | [[!UICONTROL 人员]](../../data-types/person.md) | 說明訂閱的擁有者。 |
| `bundleName` | 字符串 | 擷取客戶註冊的任何型別訂閱套件的名稱，例如 `Internet + Media`. |
| `primaryPartyID` | 字符串 | 負責訂閱的主要人員識別碼，通常可能是他們的裝置電話號碼。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

## `internetSubscription` {#internetSubscription}

`internetSubscription` 以物件陣列的形式提供。 每個物件的結構如下所述。

![internetSubscription](../../images/field-groups/telecom-subscription/internetSubscription.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `subscriptionDetails` | [[!UICONTROL 電信訂閱]](../../data-types/telecom-subscription.md) | 說明訂閱的一般詳細資料，包括訂閱長度、費用、狀態等。 說明訂閱的一般詳細資料，包括訂閱長度、費用、狀態等。 |
| `connectionType` | 字符串 | 訂閱的連線型別。 |
| `dataCap` | 整数 | 帳戶的資料上限，以兆位元組(MB)為單位。 |
| `downloadSpeed` | 整数 | 訂閱可用的最大下載速度（百萬位元組，簡稱MB）。 |
| `selfSetup` | 布尔值 | 指出客戶是否有資格在沒有技術人員造訪的情況下進行網際網路設定。 |
| `uploadSpeed` | 整数 | 訂閱可用的最大上傳速度（百萬位元組，簡稱MB）。 |

{style="table-layout:auto"}

## `landlineSubscription` {#landlineSubscription}

`landlineSubscription` 以物件陣列的形式提供。 每個物件的結構如下所述。

![有線電話訂閱](../../images/field-groups/telecom-subscription/landlineSubscription.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL 電話號碼]](../../data-types/telecom-subscription.md) | 指派給此訂閱的電話號碼。 |
| `subscriptionDetails` | [[!UICONTROL 電信訂閱]](../../data-types/telecom-subscription.md) | 說明訂閱的一般詳細資料，包括訂閱長度、費用、狀態等。 |
| `callBlocking` | 布尔值 | 指出有線電話訂閱功能是否包含來電封鎖。 |
| `callForwarding` | 布尔值 | 指出有線電話訂閱功能是否包含來電轉接。 |
| `callWaiting` | 布尔值 | 指出有線電話訂閱功能是否包含來電等候。 |
| `callerID` | 布尔值 | 指示有線電話訂閱功能是否包含來電顯示。 |
| `internationalCalling` | 布尔值 | 指出有線電話訂閱功能是否包含國際通話。 |
| `minutes` | 整数 | 訂閱內可用的每月分鐘數。 |
| `threeWayCalling` | 布尔值 | 指出有線電話訂閱功能是否包含三方通話。 |
| `unlimitedDomesticLongDistance` | 布尔值 | 指出有線電話訂閱功能是否包含不限次數的國內長途電話。 |
| `unlimitedLocalCalling` | 布尔值 | 指示有線電話訂閱功能是否包含無限制的本機通話。 |
| `voicemail` | 布尔值 | 指出有線電話訂閱功能是否包含語音信箱。 |

{style="table-layout:auto"}

## `mediaSubscription` {#mediaSubscription}

`mediaSubscription` 以物件陣列的形式提供。 每個物件的結構如下所述。

![mediaSubscription](../../images/field-groups/telecom-subscription/mediaSubscription.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `streamingServices` | 对象数组 | 訂閱隨附的所有串流服務清單。 每個陣列專案都包含以下屬性： <ul><li>`promotionLength`：促銷活動的時長（以月為單位），前提是已將串流服務新增為促銷活動的一部分。</li><li>`promotionalAddition`：指出是否將串流服務新增為促銷優惠的一部分。</li><li>`serviceName`：串流服務的名稱。</li></ul> |
| `subscriptionDetails` | [[!UICONTROL 電信訂閱]](../../data-types/telecom-subscription.md) | 說明訂閱的一般詳細資料，包括訂閱長度、費用、狀態等。 |
| `channels` | 整数 | 媒體訂閱包含的頻道數。 |

{style="table-layout:auto"}

## `mobileSubscription` {#mobileSubscription}

`mobileSubscription` 以物件陣列的形式提供。 每個物件的結構如下所述。

![mobileSubscription](../../images/field-groups/telecom-subscription/mobileSubscription.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL 電話號碼]](../../data-types/telecom-subscription.md) | 指派給此訂閱的電話號碼。 |
| `subscriptionDetails` | [[!UICONTROL 電信訂閱]](../../data-types/telecom-subscription.md) | 說明訂閱的一般詳細資料，包括訂閱長度、費用、狀態等。 |
| `earlyUpgradeEnrollment` | 布尔值 | 指出客戶是否選擇提早升級。 |
| `planLevel` | 字符串 | 指派給此訂閱的行動方案名稱。 |
| `portedNumber` | 布尔值 | 指出客戶是否從其他電信業者移轉其號碼。 |

{style="table-layout:auto"}
