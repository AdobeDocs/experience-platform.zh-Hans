---
keywords: 廣告；標準；
title: 標準連線
description: 標準提供值得信賴且具影響力的廣告，讓開放網際網路上的每位消費者都能獲得更豐富的體驗。 Criteo擁有世界上最大的商業資料集和同級最佳的AI，可確保整個購物歷程的每個接觸點都經過個人化，以便在適當的時間透過適當的廣告觸及客戶。
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: 8211ca28462548e1c17675e504e6de6f5cc55e73
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 3%

---

# (Beta) Criteo連線

## 概述 {#overview}

>[!IMPORTANT]
>
>此檔案頁面是由Criteo建立。 此產品目前為測試版，功能可能會有所變更。 如有任何查詢或更新要求，請直接聯絡條件 [此處](mailto:criteoTechnicalPartnerships@criteo.com).

標準提供值得信賴且具影響力的廣告，讓開放網際網路上的每位消費者都能獲得更豐富的體驗。 Criteo擁有世界上最大的商業資料集和同級最佳的AI，可確保整個購物歷程的每個接觸點都經過個人化，以便在適當的時間透過適當的廣告觸及客戶。

## 先决条件 {#prerequisites}

* 您必須擁有管理員使用者帳戶 [標準管理中心](https://marketing.criteo.com).
* 您將需要您的Criteo廣告商ID （如果您沒有此ID，請詢問您的Criteo聯絡人）。
* 您需要提供 [!DNL GUM caller ID]，以備您使用 [!DNL GUM ID] 作為識別碼。

## 限制 {#limitations}

* 標準僅接受 [!DNL SHA-256] — 雜湊和純文字電子郵件(將轉換為 [!DNL SHA-256] （在傳送之前）。 請勿傳送任何PII （個人識別資訊，例如個人姓名或電話號碼）。
* 條件至少需要由使用者端提供一個識別碼。 它會排定優先順序 [!DNL GUM ID] 做為雜湊電子郵件上的識別碼，因為它有助於提高符合率。

![先决条件](../../assets/catalog/advertising/criteo/prerequisites.png)

## 支援的身分 {#supported-identities}

標準支援下表所述的身分啟用。 進一步瞭解 [身分](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| 目標身分 | 描述 | 注意事项 |
| --- | --- | --- |
| `email_sha256` | 使用SHA-256演演算法雜湊處理的電子郵件地址 | Adobe Experience Platform支援純文字和SHA-256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請檢查 [!UICONTROL 套用轉換] 選項，讓Platform在啟動時自動雜湊資料。 |
| `gum_id` | 准則 [!DNL GUM] Cookie識別碼 | [!DNL GUM IDs] 允許客戶維持其使用者身分識別系統與Criteo的使用者身分識別([!DNL UID])。 如果識別碼型別為 `gum_id`，其他引數， [!DNL GUM Caller ID]，也必須包含。 請聯絡您的Criteo帳戶團隊以取得適當的 [!DNL GUM Caller ID] 或以取得此專案的詳細資訊 [!DNL GUM ID] 同步（如有需要）。 |

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
| --- | --- | --- |
| 匯出型別 | 区段导出 | 您正在匯出區段（受眾）的所有成員，而這些成員具有「 」中使用的識別碼（名稱、電話號碼或其他）。 [!DNL Criteo] 目的地。 |
| 匯出頻率 | 串流 | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](../../destination-types.md#streaming-destinations). |

## 用例 {#use-cases}

協助您更清楚瞭解如何使用 [!DNL Criteo] 目的地，以下是Adobe Experience Platform客戶可以達成的一些目標 [!DNL Criteo]：

### 使用案例1 ：取得流量

利用相關的產品優惠方案和彈性的創意來展示您的企業。 有了智慧型產品推薦，您的廣告會自動加入最有可能觸發造訪和參與的產品。 彈性的鎖定目標可讓您從Criteo的商務資料集或您自己的潛在客戶清單和AdobeCDP區段建立受眾。

### 使用案例2 ：提高網站轉換率

當訪客離開您的網站時，提醒他們缺少什麼，重新定位廣告可透過顯示特殊優惠和高度相關優惠方案來提高轉換率，無論他們接下來前往何處。 連線您的AdobeCDP區段，以重新吸引現有客戶或鎖定與您最忠誠的購物者類似的消費者。

## 連線至標準 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 驗證至條件

連線步驟如下：

1. 登入Adobe Experience Platform並連線至標準目的地。

   ![登录](../../assets/catalog/advertising/criteo/connect-destination.png)

1. 系統會將您重新導向至條件以授權連線。 您可能需要先使用您的條件憑證登入：

   ![標準登入](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![標準登入](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![標準登入](../../assets/catalog/advertising/criteo/log-in-3.png)


### 連線引數 {#connection-parameters}

在對目的地進行驗證之後，請填寫以下連線引數。

![連線引數](../../assets/catalog/advertising/criteo/connection-parameters.png)

| 字段 | 描述 | 必需 |
| --- | --- | --- |
| 名称 | 可協助您日後辨識此目的地的名稱。 您在這裡選擇的名稱將是 [!DNL Audience] 名稱於「標準管理中心」，且無法在稍後階段修改。 | 是 |
| 描述 | 可協助您日後識別此目的地的說明。 | 否 |
| 廣告商ID | 貴組織的標準廣告商ID。 請聯絡您的Criteo客戶經理以取得此資訊。 | 是 |
| 准則 [!DNL GUM caller ID] | [!DNL GUM Caller ID] 您的組織的所有成員。 請聯絡您的Criteo帳戶團隊以取得適當的 [!DNL GUM Caller ID] 或以取得此專案的詳細資訊 [!DNL GUM] 同步（如有需要）。 | 是，只要 [!DNL GUM ID] 提供為識別碼 |

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate-segments}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [對串流區段匯出目的地啟用設定檔和區段](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

## 匯出的資料 {#exported-data}

您可在以下位置檢視匯出的區段： [標準管理中心](https://marketing.criteo.com/audience-manager/dashboard).

新增使用者個人資料的請求內文，接收者為 [!DNL Criteo] 連線看起來類似這樣：

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "add",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

移除使用者個人資料的請求內文，已由 [!DNL Criteo] 連線看起來類似這樣：

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "remove",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

## 資料使用與控管 {#data-usage}

處理您的資料時，所有Adobe Experience Platform目的地都符合資料使用原則。 如需Adobe Experience Platform如何實施資料控管的詳細資訊，請閱讀 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans).

## 其他资源

* [Criteo說明中心](https://help.criteo.com/kb/en)
* [Criteo開發人員入口網站](https://developers.criteo.com)
