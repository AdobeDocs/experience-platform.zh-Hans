---
keywords: 自訂個人化；目的地；experience platform自訂目的地；
title: 自訂個人化連線
description: 此目的地提供外部個人化、內容管理系統、廣告伺服器，以及在您的網站上執行的其他應用程式，以便從Adobe Experience Platform擷取區段資訊。 此目的地會根據使用者設定檔區段成員資格，提供即時個人化。
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 09e81093c2ed2703468693160939b3b6f62bc5b6
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 6%

---

# 自訂個人化連線 {#custom-personalization-connection}

## 目的地變更記錄檔 {#changelog}

透過增強功能的Beta版 **[!UICONTROL 自訂個人化]** 目的地聯結器，您可能會看到兩個 **[!UICONTROL 自訂個人化]** 目的地目錄中的卡片。

此 **[!UICONTROL 使用屬性自訂個人化]** 聯結器目前為測試版，僅供特定數量的客戶使用。 除了 **[!UICONTROL 自訂個人化]**，則 **[!UICONTROL 使用屬性自訂個人化]** 聯結器新增選購專案 [對應步驟](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) 至啟用工作流程，可讓您將設定檔屬性對應至自訂個人化目的地，啟用以屬性為基礎的相同頁面和下一頁個人化。

>[!IMPORTANT]
>
>設定檔屬性可能包含敏感資料。 為了保護此資料， **[!UICONTROL 使用屬性自訂個人化]** 目的地要求您使用 [Edge Network Server API](/help/server-api/overview.md) 用於資料彙集。 此外，所有伺服器API呼叫都必須在 [已驗證的內容](../../../server-api/authentication.md).
>
>如果您已在使用Web SDK或Mobile SDK進行整合，您可以透過兩種方式透過伺服器API擷取屬性：
>
> * 新增透過伺服器API擷取屬性的伺服器端整合。
> * 使用自訂Javascript程式碼更新您的使用者端設定，以透過伺服器API擷取屬性。
>
> 如果您未遵循上述要求，個人化將僅以區段成員資格為基礎，與提供的體驗相同。 **[!UICONTROL 自訂個人化]** 聯結器。

![並排檢視中兩張自訂個人化目的地卡的影像。](../../assets/catalog/personalization/custom-personalization/custom-personalization-side-by-side-view.png)

## 概述 {#overview}

此目的地提供從Adobe Experience Platform擷取區段資訊至外部個人化平台、內容管理系統、廣告伺服器和客戶網站上執行的其他應用程式的方法。

## 先决条件 {#prerequisites}

這項整合由以下支援： [Adobe Experience Platform Web SDK](../../../edge/home.md) 或 [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/). 您必須使用其中一個SDK才能使用此目的地。

>[!IMPORTANT]
>
>在建立自訂個人化連線之前，請閱讀以下操作指南： [設定相同頁面和下一頁個人化的個人化目的地](../../ui/configure-personalization-destinations.md). 本指南會針對跨多個Experience Platform元件的相同頁面和下一頁個人化使用案例，引導您進行必要的設定步驟。

## 匯出型別和頻率 {#export-type-frequency}

**設定檔請求**  — 您正在要求已對映於單一設定檔之自訂個人化目的地的所有區段。 可以為不同的設定不同的自訂個人化目的地 [Adobe資料收集資料串流](../../../edge/datastreams/overview.md).

## 用例 {#use-cases}

此 [!DNL Custom Personalization Connection] 可讓您使用自己的個人化合作夥伴平台(例如 [!DNL Optimizely]， [!DNL Pega])以及專屬系統（例如內部CMS），同時運用Experience Platform邊緣網路資料收集和細分功能，提供更深入的客戶個人化體驗。

以下說明的使用案例包含網站個人化和目標網站上的廣告。

若要啟用這些使用案例，客戶需要一種快速且簡化的方式，從Experience Platform擷取區段資訊，並將此資訊傳送至其指定的系統，這些系統已在Experience PlatformUI中設定為自訂個人化連線。

這些系統可以是外部個人化平台、內容管理系統、廣告伺服器，以及其他在客戶的網頁和行動屬性中執行的應用程式。

### 同一页面个性化 {#same-page}

使用者造訪您網站的某個頁面。 客戶可以使用目前頁面瀏覽資訊（例如，反向連結URL、瀏覽器語言、內嵌的產品資訊）來選取下一個動作/決定（例如，個人化），對非Adobe平台使用自訂個人化連線(例如， [!DNL Pega]， [!DNL Optimizely]、等)。

### 下一頁個人化 {#next-page}

使用者造訪您網站上的頁面A。 根據此互動，使用者已符合一組區段的資格。 然後，使用者按一下連結，該連結會將使用者從頁面A帶往頁面B。使用者在頁面A的上一個互動期間符合資格的區段，加上目前網站造訪決定的設定檔更新，將用來支援下一個動作/決定（例如，要向訪客顯示哪個廣告橫幅，或在A/B測試的情況下，要顯示哪個頁面版本）。

### 下一个会话个性化 {#next-session}

使用者造訪您網站上的數個頁面。 根據這些互動，使用者已符合一組區段的資格。 然後，使用者會終止目前的瀏覽工作階段。

第二天，使用者返回相同的客戶網站。 他們之前與所有造訪的網站頁面互動期間符合資格的區段，加上目前網站造訪決定的設定檔更新，將用於選取下一個動作/決定（例如，要向訪客顯示哪個廣告橫幅，或在A/B測試的情況下，要顯示哪個頁面版本）。

## 連線到目的地 {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="关于数据流 ID"
>abstract="此选项确定区段将包含在哪个数据收集数据流中以响应页面。下拉菜单仅显示已启用目标配置的数据流。您必须先配置数据流，然后才能配置目标。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=zh-Hans" text="了解如何配置数据流"

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 連線引數 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊：

* **[!UICONTROL 名稱]**：填寫此目的地的偏好名稱。
* **[!UICONTROL 說明]**：輸入目的地的說明。 例如，您可以提及要將此目的地用於哪個行銷活動。 此欄位為選用。
* **[!UICONTROL 整合別名]**：此值會以JSON物件名稱的形式傳送至Experience PlatformWeb SDK。
* **[!UICONTROL 資料串流ID]**：這會決定區段會包含在頁面的回應中的資料收集資料串流。 下拉菜单仅显示已启用目标配置的数据流。另請參閱 [設定資料串流](../../../edge/datastreams/overview.md) 以取得更多詳細資料。

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [對設定檔請求目的地啟用設定檔和區段](../../ui/activate-profile-request-destinations.md) 以取得啟用此目的地的受眾區段的指示。

## 匯出的資料 {#exported-data}

如果您使用 [Adobe Experience Platform中的標籤](../../../tags/home.md) 若要部署Experience PlatformWeb SDK，請使用 [傳送事件完成](../../../edge/extension/event-types.md) 功能和您的自訂程式碼動作將具有 `event.destinations` 可用來檢視匯出資料的變數。

以下是的範例值 `event.destinations` 變數：

```
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         }
      ]
   }
]
```

如果您沒有使用 [標籤](../../../tags/home.md) 若要部署Experience PlatformWeb SDK，請使用 [處理來自事件的回應](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) 功能以檢視匯出的資料。

來自Adobe Experience Platform的JSON回應可加以剖析，以找出您要與Adobe Experience Platform整合之應用程式的對應整合別名。 區段ID可作為定位引數傳遞至應用程式的程式碼中。 以下是目標回應專屬內容的範例。

```
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    if(result.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = result.destinations.filter(x => x.alias == "personalizationAlias")
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### 的範例回應 [!UICONTROL 使用屬性自訂個人化]

使用時 **[!UICONTROL 使用屬性自訂個人化]**，API回應將與以下範例類似。

兩者之間的差異 **[!UICONTROL 使用屬性自訂個人化]** 和 **[!UICONTROL 自訂個人化]** 是納入 `attributes` API回應中的區段。

```json
[
    {
        "type": "profileLookup",
        "destinationId": "7bb4cb8d-8c2e-4450-871d-b7824f547130",
        "alias": "personalizationAlias",
        "attributes": {
             "countryCode": {
                   "value" : "DE"
              },
             "membershipStatus": {
                   "value" : "PREMIUM"
              }
         },         
        "segments": [
            {
                "id": "399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            },
            {
                "id": "499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            }
        ]
    }
]
```

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請閱讀 [資料控管概觀](../../../data-governance/home.md).
