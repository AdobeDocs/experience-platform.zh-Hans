---
solution: Experience Platform
title: 具有訂閱資料型別的通用行銷偏好設定欄位
description: 本檔案提供具有訂閱XDM資料型別的一般行銷偏好設定欄位概觀。
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 1%

---

# [!UICONTROL 具有訂閱的一般行銷偏好設定欄位] 資料型別

[!UICONTROL 具有訂閱的一般行銷偏好設定欄位] 是標準XDM資料型別，說明客戶為特定行銷偏好設定的選擇。

>[!NOTE]
>
>此資料型別旨在用來自訂您組織同意綱要的結構，使用 [[!UICONTROL 同意和偏好設定] 欄位群組](../field-groups/profile/consents.md) 作為基準線。
>
>如果您不需要 `subscriptions` 對應特定行銷偏好設定欄位，您可以使用 [基本行銷欄位資料型別](./marketing-field.md) 而非。

![](../images/data-types/marketing-field-subscriptions.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `reason` | 字符串 | 當客戶選擇退出行銷使用案例時，此字串欄位代表客戶選擇退出的原因。 |
| `subscriptions` | 地图 | 特定訂閱的客戶行銷偏好設定地圖。 請參閱以下小節： [訂閱](#subscriptions) 以取得詳細資訊。 |
| `time` | 日期時間 | 行銷偏好設定變更時間的ISO 8601時間戳記（如適用）。 |
| `val` | 字符串 | 客戶針對此行銷使用案例提供的偏好設定選擇。 請參閱 [下一節](#val) 以取得接受的值和定義。 |

{style="table-layout:auto"}

## `val` {#val}

下表概述下列專案的可接受值 `val`：

| 值 | 标题 | 描述 |
| --- | --- | --- |
| `y` | 是（選擇加入） | 客戶已選擇加入偏好設定。 換言之，他們 **do** 同意使用相關偏好設定所指示的資料。 |
| `n` | 否（選擇退出） | 客戶已選擇退出偏好設定。 換言之，他們 **不要** 同意使用相關偏好設定所指示的資料。 |
| `p` | 擱置中的驗證 | 系統尚未收到最終偏好設定值。 這通常用於需要兩步驟驗證的同意中。 例如，如果客戶選擇接收電子郵件，該同意將設為 `p` 直到他們選取電子郵件中的連結，以確認他們提供了正確的電子郵件地址，同意才會更新為 `y`.<br><br>如果此喜好設定未使用兩集驗證程式，則 `p` 選擇可用於指出客戶尚未回應同意提示。 例如，您可以自動將值設為 `p` 在網站首頁，客戶尚未回應同意提示時。 在不需要明確同意的管轄區中，您也可以使用它來表示客戶尚未明確選擇退出（換句話說，假設您同意）。 |
| `u` | 未知 | 客戶的偏好設定資訊不明。 |
| `dy` | 是（選擇加入）的預設值 | 客戶本身並未提供同意值，且預設會被視為選擇加入（「是」）。 換言之，在客戶另外表示同意之前，一律假定客戶同意。<br><br>請注意，如果貴公司隱私權政策的法律或變更導致部分或所有使用者的預設值變更，您必須手動更新包含預設值的所有設定檔。 |
| `dn` | 「否」（選擇退出）的預設值 | 客戶本身並未提供同意值，且預設會被視為選擇退出（「否」）。 換言之，客戶被假定已拒絕同意，直到他們指出不同意。<br><br>請注意，如果貴公司隱私權政策的法律或變更導致部分或所有使用者的預設值變更，您必須手動更新包含預設值的所有設定檔。 |
| `LI` | 合法利益 | 為特定目的收集和處理此資料的合法商業利益，超過其對個人的潛在傷害。 |
| `CT` | 合約 | 為特定目的收集資料是履行與個人的合約義務所必需的。 |
| `CP` | 遵守法律義務 | 為了符合企業的法律義務，必須針對特定目的收集資料。 |
| `VI` | 個人的重大利益 | 為了保護個人切身利益，需要為特定目的收集資料。 |
| `PI` | 公共利益 | 為了公眾利益或行使官方權力，需要為特定目的收集資料。 |

{style="table-layout:auto"}

## `subscriptions` {#subscriptions}

某些企業允許客戶選擇加入與特定行銷管道相關聯的不同訂閱。 例如，銀行公司可能會允許客戶訂閱超額帳戶的電話警示，或接收忠誠計畫優惠方案的銷售電話。

以下JSON代表包含「 」的電話聯絡行銷管道的行銷欄位範例。 `subscriptions` 地圖。 中的每一個索引鍵 `subscriptions` 物件代表行銷管道的個別訂閱。 反過來，每個訂閱都包含一個選擇加入值(`val`)。

```json
"email-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "topics": ["discounts", "early-access"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "newsletters": {
      "val": "y",
      "type": "advertising",
      "topics": ["hardware"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "tparan@example.com": {
          "time": "2020-02-03T07:54:21+07:00",
          "source": "call center"
        }
      }
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `val` | 此 [同意值](#val) 以取得訂閱。 |
| `type` | 訂閱型別。 這可以是任何描述性字串，但不得超過15個字元。 |
| `topics` | 一組字串，代表客戶所訂閱的興趣區域，可用來傳送相關內容給客戶。 |
| `subscribers` | 選用的對應型別欄位，代表已訂閱特定訂閱的一組識別碼（例如電子郵件地址或電話號碼）。 此物件中的每個索引鍵都代表相關識別碼，並包含兩個子屬性： <ul><li>`time`：身分訂閱時間的ISO 8601時間戳記（如適用）。</li><li>`source`：訂閱者源自的來源。 這可以是任何描述性字串，但不得超過15個字元。</li></ul> |

{style="table-layout:auto"}

## 其他资源

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
