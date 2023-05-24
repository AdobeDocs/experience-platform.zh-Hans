---
keywords: Experience Platform；首頁；Intelligent Services；熱門主題；Intelligent Service；Intelligent Service
solution: Experience Platform
title: 準備資料以用於Intelligent Services
description: 為了讓Intelligent Services從行銷事件資料中探索見解，資料必須在語義上豐富化，並以標準結構維護。 Intelligent Services使用Experience Data Model (XDM)結構描述來達成此目的。
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: 87a8ad253abb219662034652b5f8c4fabfa40484
workflow-type: tm+mt
source-wordcount: '2936'
ht-degree: 0%

---

# 準備資料以用於中 [!DNL Intelligent Services]

為了 [!DNL Intelligent Services] 若要從行銷事件資料中探索深入分析，資料必須在語義上豐富化，並以標準結構維護。 [!DNL Intelligent Services] 善用 [!DNL Experience Data Model] (XDM)結構描述才能達到此目的。 具體來說，就是所有用於 [!DNL Intelligent Services] 必須符合消費者ExperienceEvent (CEE) XDM結構描述或使用Adobe Analytics聯結器。 此外，Customer AI支援Adobe Audience Manager聯結器。

本檔案提供將多個管道的行銷事件資料對應至CEE結構描述的一般指引，概述結構描述內重要欄位的資訊，以協助您決定如何有效地將資料對應至其結構。 如果您打算使用Adobe Analytics資料，請檢視以下專案的區段： [Adobe Analytics資料準備](#analytics-data). 如果您打算使用Adobe Audience Manager資料（僅限Customer AI），請檢視以下區段： [AdobeAudience Manger資料準備](#AAM-data).

## 資料需求

[!DNL Intelligent Services] 會根據您建立的目標而需要不同的歷史資料量。 無論如何，您準備的資料 **全部** [!DNL Intelligent Services] 必須包含正面和負面客戶歷程/事件。 同時具有負值和正值事件可改善模型精確度和精確度。

例如，如果您使用Customer AI來預測購買產品的傾向，Customer AI模型需要成功購買路徑的範例和失敗路徑的範例。 這是因為在模型訓練期間，Customer AI會尋找哪些事件和歷程會導致購買。 這也包括未購買的客戶所執行的動作，例如個人停止其將專案新增至購物車的歷程。 這些客戶可能會表現出相似的行為，但是Customer AI可以提供見解並深入研究導致更高傾向分數的主要差異和因素。 同樣地，Attribution AI需要事件和歷程這兩種型別，才能顯示量度，例如接觸點有效性、排名在前的轉換路徑，以及依接觸點位置的劃分。

如需有關歷史資料需求的更多範例和資訊，請造訪 [Customer AI](./customer-ai/data-requirements.md#data-requirements) 或 [Attribution AI](./attribution-ai/input-output.md#data-requirements) 輸入/輸出檔案中的歷史資料需求區段。

### 彙整資料的准則

建議您儘可能拼接通用ID中的使用者事件。 例如，您可能有跨10個事件具有「id1」的使用者資料。 稍後，該使用者刪除了Cookie ID，並在接下來的20個事件中記錄為「id2」。 如果您知道id1和id2對應至相同的使用者，最佳做法是將所有30個事件與通用id拼接在一起。

如果無法執行此操作，您應在建立模型輸入資料時，將每組事件視為不同的使用者。 這可確保在模型訓練和評分期間獲得最佳結果。

## 工作流程摘要

準備程式會因您的資料是儲存在Adobe Experience Platform中還是儲存在外部而異。 本節總結了您在任一情況下所需採取的必要步驟。

### 外部資料準備

如果您的資料儲存在Experience Platform以外，您需要將資料對應到 [消費者ExperienceEvent結構描述](#cee-schema). 此結構描述可以透過自訂欄位群組增強，以更好地擷取您的客戶資料。 對應後，您可以使用消費者ExperienceEvent結構描述和建立資料集 [將您的資料內嵌至Platform](../ingestion/home.md). 之後，您便可在設定 [!DNL Intelligent Service].

根據 [!DNL Intelligent Service] 如果您希望使用，可能需要不同的欄位。 請注意，如果您有可用的資料，最佳實務就是將資料新增至欄位。 若要進一步瞭解必填欄位，請造訪 [Attribution AI](./attribution-ai/input-output.md) 或 [Customer AI](./customer-ai/data-requirements.md) 資料需求指南。

### Adobe Analytics資料準備 {#analytics-data}

Customer AI和Attribution AI原生支援Adobe Analytics資料。 若要使用Adobe Analytics資料，請依照檔案中概述的步驟設定 [Analytics來源聯結器](../sources/tutorials/ui/create/adobe-applications/analytics.md).

一旦來源聯結器將您的資料串流到Experience Platform中，您就可以在執行個體設定期間選取Adobe Analytics作為資料來源，然後選取資料集。 在連線設定期間會自動建立所有必要的結構描述欄位群組和個別欄位。 您不需要將資料集ETL （擷取、轉換、載入）為CEE格式。

如果您比較流經Adobe Analytics來源聯結器至Adobe Experience Platform的資料與Adobe Analytics資料，您可能會注意到一些差異。 Analytics來源聯結器在轉換為體驗資料模型(XDM)結構描述期間可能會捨棄多列。 整列不適用於轉換的原因有好幾種，包括遺漏時間戳記、遺漏人員ID、無效或大筆人員ID、無效分析值等等。

如需詳細資訊和範例，請瀏覽以下檔案： [比較Adobe Analytics和Customer Journey Analytics資料](https://www.adobe.com/go/compare-aa-data-to-cja-data). 本文章旨在協助您診斷並解決這些差異，好讓您和您的團隊能夠將Adobe Experience Platform資料用於智慧型服務，不會受到資料完整性疑慮的阻礙。

在Adobe Experience Platform查詢服務中，依channel.typeAtSource查詢執行下列開始和結束時間戳記之間的記錄總數，以依行銷管道尋找計數。

```SELECT channel.typeAtSource as typeAtSource,
       Count(_id) AS Records 
FROM  df_hotel
WHERE timestamp>=from_utc_timestamp('2021-05-15','UTC')
        AND timestamp<from_utc_timestamp('2022-01-10','UTC')
        AND timestamp IS NOT NULL
        AND enduserids._experience.aaid.id IS NOT NULL
GROUP BY channel.typeAtSource
```

>[!IMPORTANT]
>
>Adobe Analytics聯結器最多需要四週的時間來回填資料。 如果您最近才設定連線，您應確認資料集具有客戶或Attribution AI所需的最小資料長度。 請檢閱歷史資料區段： [Customer AI](./customer-ai/data-requirements.md#data-requirements) 或 [Attribution AI](./attribution-ai/input-output.md#data-requirements)，並確認您有足夠的資料達成預測目標。

### Adobe Audience Manager資料準備（僅限Customer AI） {#AAM-data}

Customer AI原生支援Adobe Audience Manager資料。 若要使用Audience Manager資料，請依照檔案中概述的步驟設定 [Audience Manager來源聯結器](../sources/tutorials/ui/create/adobe-applications/audience-manager.md).

一旦來源聯結器將您的資料串流到Experience Platform中，您就可以在Customer AI設定期間選取Adobe Audience Manager作為資料來源，然後選取資料集。 所有結構描述欄位群組和個別欄位會在連線設定期間自動建立。 您不需要將資料集ETL （擷取、轉換、載入）為CEE格式。

>[!IMPORTANT]
>
>如果您最近設定了聯結器，您應該確認資料集具有所需的最小資料長度。 請檢閱以下文章的歷史資料區段： [輸入/輸出檔案](./customer-ai/data-requirements.md) ，並確認您有足夠的資料達成預測目標。

### [!DNL Experience Platform] 資料準備

如果您的資料已儲存在 [!DNL Platform] 並且不要透過Adobe Analytics或Adobe Audience Manager （僅限Customer AI）來源聯結器串流，請遵循以下步驟。 我們仍建議您瞭解CEE結構。

1. 檢閱結構 [消費者ExperienceEvent結構描述](#cee-schema) 以及決定是否可將您的資料對應至其欄位。
2. 請聯絡Adobe諮詢服務，協助將您的資料對應到結構描述並將其擷取到 [!DNL Intelligent Services]，或 [請依照本指南中的步驟操作](#mapping) 如果您想要自行對應資料。

## 瞭解CEE結構 {#cee-schema}

消費者ExperienceEvent結構描述個人與數位行銷事件（網頁或行動裝置）以及線上或離線商務活動相關的行為。 以下專案需要使用此結構描述： [!DNL Intelligent Services] 由於它的語義定義良好的欄位（欄），避免任何未知的名稱，否則會使資料不太清楚。

CEE結構描述和所有XDM ExperienceEvent結構描述一樣，會在事件（或事件集）發生時擷取系統以時間序列為基礎的狀態，包括時間點和所涉及的主體身分。 體驗事件是所發生事件的事實記錄，因此是不可變的，並代表在沒有彙總或詮釋的情況下所發生的情況。

[!DNL Intelligent Services] 利用此結構描述中的數個關鍵欄位，從行銷事件資料產生深入分析，所有這些可在根層級找到，並展開以顯示其必要的子欄位。

![](./images/data-preparation/schema-expansion.gif)

和所有XDM結構描述一樣，CEE結構描述欄位群組也是可擴展的。 換言之，其他欄位可新增至CEE欄位群組，如有需要，多個結構描述中可包含不同的變數。

欄位群組的完整範例可在以下網址找到： [公用XDM存放庫](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). 此外，您還可以檢視和複製下列專案 [JSON檔案](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) 有關如何將資料結構化以符合CEE架構的範例。 瞭解下節中概述的關鍵欄位時，請參閱這兩個範例，以判斷如何將您自己的資料對應到結構描述。

## 關鍵欄位

CEE欄位群組內有數個關鍵欄位，應加以使用以便用於 [!DNL Intelligent Services] 以產生有用的深入分析。 本節說明這些欄位的使用案例和預期資料，並提供參考檔案的連結以取得更多範例。

### 必填欄位

雖然強烈建議使用所有關鍵欄位，但有兩個欄位 **必填** 為了 [!DNL Intelligent Services] 若要運作：

* [主要身分欄位](#identity)
* [xdm：timestamp](#timestamp)
* [xdm：channel](#channel) (僅對於Attribution AI為必要)

#### 主要标识 {#identity}

結構描述中的其中一個欄位必須設定為主要身分欄位，這樣才允許 [!DNL Intelligent Services] 將時間序列資料的每個例項連結至個人。

您必須根據資料的來源和性質，決定要當作主要身分使用的最佳欄位。 身分欄位必須包括 **身分名稱空間** 表示欄位預期做為值的身分資料型別。 一些有效的名稱空間值包括：

>[!NOTE]
>
>Experience CloudID (ECID)也稱為MCID，並將繼續用於名稱空間。

* &quot;电子邮件&quot;
* &quot;phone&quot;
* &quot;mcid&quot; (適用於Adobe Audience Manager ID)
* &quot;aaid&quot; (適用於Adobe Analytics ID)

如果您不確定應使用哪個欄位作為主要身分，請聯絡Adobe諮詢服務以決定最佳解決方案。 如果未設定主要身分，Intelligent Service應用程式會使用以下預設行為：

| 默认 | 归因人工智能 | Customer AI |
| --- | --- | --- |
| 身分資料行 | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| 命名空间 | AAID | ECID |

若要設定主要身分，請從以下網址瀏覽至您的結構描述： **[!UICONTROL 結構描述]** 標籤並選取結構描述名稱超連結以開啟 **[!DNL Schema Editor]**.

![導覽至結構描述](./images/data-preparation/navigate_schema.png)

接下來，導覽至您要作為主要身分的欄位，然後選取它。 此 **[!UICONTROL 欄位屬性]** 該欄位的功能表隨即開啟。

![選取欄位](./images/data-preparation/find_field.png)

在 **[!UICONTROL 欄位屬性]** 功能表，向下捲動直到您找到 **[!UICONTROL 身分]** 核取方塊。 核取此方塊後，將選取的身分設定為 **[!UICONTROL 主要身分]** 出現。 也請選取此方塊。

![選取核取方塊](./images/data-preparation/set_primary_identity.png)

接下來，您必須提供 **[!UICONTROL 身分名稱空間]** 從下拉式清單中的預先定義名稱空間清單。 在此範例中，會選取ECID名稱空間，因為Adobe Audience Manager ID `mcid.id` 正在使用中。 選取 **[!UICONTROL 套用]** 若要確認更新，請選取 **[!UICONTROL 儲存]** 以儲存對結構描述的變更。

![儲存變更](./images/data-preparation/select_namespace.png)

#### xdm：timestamp {#timestamp}

此欄位代表事件發生時的日期時間。 根據ISO 8601標準，此值必須以字串形式提供。

#### xdm：channel {#channel}

>[!NOTE]
>
>只有在使用Attribution AI時，此欄位才為必要。

此欄位代表與ExperienceEvent相關的行銷管道。 欄位包含有關頻道型別、媒體型別和位置型別的資訊。

![](./images/data-preparation/channel.png)

**範例結構描述**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

有關每個必要子欄位的完整資訊，請參見 `xdm:channel`，請參閱 [體驗管道結構描述](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) 規格 如需一些對應範例，請參閱 [下表](#example-channels).

#### 管道對應範例 {#example-channels}

下表提供一些對映至的行銷管道範例 `xdm:channel` 綱要：

| 渠道 | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| 付费搜索 | https:/<span>/ns.adobe.com/xdm/channel-types/search | 付費 | 點按次數 |
| 社交 — 行銷 | https:/<span>/ns.adobe.com/xdm/channel-types/social | 盈餘 | 點按次數 |
| 显示 | https:/<span>/ns.adobe.com/xdm/channel-types/display | 付費 | 點按次數 |
| 电子邮件 | https:/<span>/ns.adobe.com/xdm/channel-types/email | 付費 | 點按次數 |
| 內部反向連結 | https:/<span>/ns.adobe.com/xdm/channel-types/direct | 擁有 | 點按次數 |
| 顯示檢視 | https:/<span>/ns.adobe.com/xdm/channel-types/display | 付費 | 曝光次數 |
| QR碼重新導向 | https:/<span>/ns.adobe.com/xdm/channel-types/direct | 擁有 | 點按次數 |
| 移动设备 | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | 擁有 | 點按次數 |

### 建議欄位

本節將概述其餘主要欄位。 雖然這些欄位不一定需要 [!DNL Intelligent Services] 為了發揮作用，強烈建議您儘可能多地使用它們，以獲得更豐富的見解。

#### xdm：productListItems

此欄位是代表客戶所選產品的專案陣列，包括產品SKU、名稱、價格和數量。

![](./images/data-preparation/productListItems.png)

**範例結構描述**

```json
[
  {
    "xdm:SKU": "1002352692",
    "xdm:name": "24-Watt 8-Light Chrome Integrated LED Bath Light",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 159.45
  },
  {
    "xdm:SKU": "3398033623",
    "xdm:name": "16ft RGB LED Strips",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 79.99
  }
]
```

有關每個必要子欄位的完整資訊，請參見 `xdm:productListItems`，請參閱 [商務詳細資料結構描述](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 規格

#### xdm：commerce

此欄位包含有關ExperienceEvent的商務特定資訊，包括採購單編號和付款資訊。

![](./images/data-preparation/commerce.png)

**範例結構描述**

```json
{
    "xdm:order": {
      "xdm:purchaseID": "a8g784hjq1mnp3",
      "xdm:purchaseOrderNumber": "123456",
      "xdm:payments": [
        {
          "xdm:transactionID": "transactid-a111",
          "xdm:paymentAmount": 59,
          "xdm:paymentType": "credit_card",
          "xdm:currencyCode": "USD"
        },
        {
          "xdm:transactionId": "transactid-a222",
          "xdm:paymentAmount": 100,
          "xdm:paymentType": "gift_card",
          "xdm:currencyCode": "USD"
        }
      ],
      "xdm:currencyCode": "USD",
      "xdm:priceTotal": 159
    },
    "xdm:purchases": {
      "xdm:value": 1
    }
  }
```

有關每個必要子欄位的完整資訊，請參見 `xdm:commerce`，請參閱 [商務詳細資料結構描述](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 規格

#### xdm：web

此欄位代表與ExperienceEvent相關的網頁詳細資訊，例如互動、頁面詳細資訊和反向連結。

![](./images/data-preparation/web.png)

**範例結構描述**

```json
{
  "xdm:webPageDetails": {
    "xdm:siteSection": "Shopping Cart",
    "xdm:server": "example.com",
    "xdm:name": "Purchase Confirmation",
    "xdm:URL": "https://www.example.com/orderConf",
    "xdm:errorPage": false,
    "xdm:homePage": false,
    "xdm:pageViews": {
      "xdm:value": 1
    }
  },
  "xdm:webReferrer": {
    "xdm:URL": "https://www.example.com/checkout",
    "xdm:referrerType": "internal"
  }
}
```

有關每個必要子欄位的完整資訊，請參見 `xdm:productListItems`，請參閱 [ExperienceEvent Web詳細資料結構描述](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) 規格

#### xdm：marketing

此欄位包含與使用接觸點啟用的行銷活動相關的資訊。

![](./images/data-preparation/marketing.png)

**範例結構描述**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

有關每個必要子欄位的完整資訊，請參見 `xdm:productListItems`，請參閱 [行銷密碼](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) 規格

## 對應和擷取資料 {#mapping}

一旦您確定行銷事件資料是否可對應至CEE結構描述後，下一步就是確定要帶入哪些資料 [!DNL Intelligent Services]. 所有歷史資料使用於 [!DNL Intelligent Services] 必須在資料的最短四個月時間範圍內，加上預期作為回顧期間的天數。

決定您要傳送的資料範圍後，請聯絡Adobe諮詢服務，協助將您的資料對應到結構描述並將其擷取到服務中。

如果您擁有 [!DNL Adobe Experience Platform] 訂閱，並想自行對應及擷取資料，請遵循下節中概述的步驟。

### 使用Adobe Experience Platform

>[!NOTE]
>
>下列步驟需要訂閱Experience Platform。 如果您無法存取平台，請跳至 [後續步驟](#next-steps) 區段。

本節概述對應及擷取資料至Experience Platform以供使用的工作流程 [!DNL Intelligent Services]，包含教學課程的連結，以取得詳細步驟。

#### 建立CEE方案和資料集

當您準備好開始準備要擷取的資料時，第一步是建立採用CEE欄位群組的新XDM結構描述。 以下教學課程會逐步說明在UI或API中建立新結構的程式：

* [在UI中建立結構描述](../xdm/tutorials/create-schema-ui.md)
* [在API中建立結構描述](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>上述教學課程遵循建立結構描述的一般工作流程。 為結構描述選擇類別時，您必須使用 **XDM ExperienceEvent類別**. 選擇此類別後，您就可以將CEE欄位群組新增到結構描述中。

將CEE欄位群組新增到結構描述後，您可以視需要新增其他欄位群組，以用於資料內的其他欄位。

建立並儲存結構描述後，您就可以根據該結構描述建立新的資料集。 以下教學課程會逐步說明在UI或API中建立新資料集的程式：

* [在UI中建立資料集](../catalog/datasets/user-guide.md#create) （遵循使用現有結構描述的工作流程）
* [在API中建立資料集](../catalog/datasets/create.md)

建立資料集後，您可以在的Platform UI中找到 **[!UICONTROL 資料集]** 工作區。

![](images/data-preparation/dataset-location.png)

#### 將身分欄位新增至資料集

如果您要從以下來源匯入資料： [!DNL Adobe Audience Manager]， [!DNL Adobe Analytics]，或是其他外部來源，您就可以選擇將結構描述欄位設定為身分欄位。 若要將結構描述欄位設定為身分欄位，請檢視內關於設定身分欄位的區段 [UI教學課程](../xdm/tutorials/create-schema-ui.md#identity-field) 或 [api教學課程](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) 用於建立結構描述。

如果您從本機CSV檔案擷取資料，您可以跳至的下一節： [對應和擷取資料](#ingest).

#### 對應及擷取資料 {#ingest}

建立CEE結構和資料集後，您可以開始將資料表對應至結構，並將資料擷取到Platform。 請參閱教學課程，位置如下： [將CSV檔案對應至XDM結構描述](../ingestion/tutorials/map-csv/overview.md) 瞭解如何在UI中執行此動作的步驟。 您可以使用下列專案 [範例JSON檔案](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) ，在使用您自己的資料之前測試擷取程式。

填入資料集後，相同的資料集可用於擷取其他資料檔案。

如果您的資料儲存在支援的協力廠商應用程式中，您也可以選擇建立 [來源聯結器](../sources/home.md) 將行銷事件資料內嵌至 [!DNL Platform] 即時。

## 后续步骤 {#next-steps}

本檔案提供準備您的資料以用於的一般指引 [!DNL Intelligent Services]. 如果您需要根據使用案例提供其他諮詢，請聯絡Adobe諮詢支援。

成功將客戶體驗資料填入資料集後，您就可以使用 [!DNL Intelligent Services] 以產生深入分析。 請參閱下列檔案以開始使用：

* [归因人工智能概述](./attribution-ai/overview.md)
* [客户人工智能概述](./customer-ai/overview.md)
