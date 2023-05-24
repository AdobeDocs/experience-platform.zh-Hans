---
keywords: Experience Platform；首頁；熱門主題；串流；串流擷取；疑難排解；串流擷取疑難排解；串流擷取常見問題集；faq；
solution: Experience Platform
title: 串流擷取疑難排解指南
description: 本檔案提供有關Adobe Experience Platform串流擷取的常見問題解答。
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# 串流擷取疑難排解指南

本檔案提供有關Adobe Experience Platform串流擷取的常見問題解答。 關於其他相關問題和疑難排解 [!DNL Platform] 服務，包括所有使用者遇到的 [!DNL Platform] API，請參閱 [Experience Platform疑難排解指南](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] 提供您可用來將資料擷取至的RESTful API [!DNL Experience Platform]. 所擷取的資料會用於近乎即時更新個別客戶設定檔，好讓您跨多個管道提供個人化的相關體驗。 請閱讀 [資料擷取概觀](../home.md) 以取得有關服務和不同擷取方法的詳細資訊。 如需如何使用串流獲取API的步驟，請參閱 [串流擷取概觀](../streaming-ingestion/overview.md).

## 常见问题解答

以下是有關串流擷取的常見問題解答清單。

### 如何確認我傳送的裝載格式正確？

[!DNL Data Ingestion] 利用 [!DNL Experience Data Model] (XDM)結構描述來驗證傳入資料的格式。 傳送不符合預先定義XDM結構描述的資料將會導致擷取失敗。 如需有關XDM及其在下列專案中的使用的詳細資訊： [!DNL Experience Platform]，請參閱 [XDM系統總覽](../../xdm/home.md).

串流擷取支援兩種驗證模式：同步和非同步。 每個驗證方法處理失敗資料的方式都不同。

**同步驗證** 您應在開發程式中使用。 未通過驗證的記錄會被捨棄，並傳回失敗原因的錯誤訊息（例如：「無效的XDM訊息格式」）。

**非同步驗證** 應該用於生產環境。 任何未通過驗證的格式錯誤資料都會傳送至 [!DNL Data Lake] 作為失敗的批次檔案，稍後可從中擷取該檔案以供進一步分析。

如需同步和非同步驗證的詳細資訊，請參閱 [串流驗證概觀](../quality/streaming-validation.md). 如需如何檢視驗證失敗的批次的步驟，請參閱以下指南： [擷取失敗的批次](../quality/retrieve-failed-batches.md).

### 我可以在將請求裝載傳送至之前先驗證它嗎？ [!DNL Platform]？

請求裝載只有在傳送至後才能評估 [!DNL Platform]. 執行同步驗證時，有效裝載會傳回填入的JSON物件，而無效裝載會傳回錯誤訊息。 在非同步驗證期間，服務會偵測任何格式錯誤的資料，並將其傳送至 [!DNL Data Lake] 之後可從中擷取資料以供分析。 請參閱 [串流驗證概觀](../quality/streaming-validation.md) 以取得詳細資訊。

### 在不支援同步驗證的邊緣上請求同步驗證時，會發生什麼情況？

當要求的位置不支援同步驗證時，會傳回501錯誤回應。 請參閱 [串流驗證概觀](../quality/streaming-validation.md) 以取得同步驗證的詳細資訊。

### 如何確保僅從受信任的來源收集資料？

[!DNL Experience Platform] 支援安全資料收集。 啟用已驗證的資料彙集時，使用者端必須傳送JSON Web權杖(JWT)及其組織ID作為要求標頭。 有關如何將已驗證資料傳送至的詳細資訊 [!DNL Platform]，請參閱指南： [已驗證的資料彙集](../tutorials/create-authenticated-streaming-connection.md).

### 將資料串流至多長時間才會發生 [!DNL Real-Time Customer Profile]？

串流事件通常反映在 [!DNL Real-Time Customer Profile] 不到60秒。 實際延遲時間可能會因資料量、訊息大小和頻寬限制而異。

### 我可以在同一API請求中包含多則訊息嗎？

您可以在單一請求裝載中將多個訊息分組，並將它們串流至 [!DNL Platform]. 正確使用時，在單一請求中將多個訊息分組，是最佳化資料作業的絕佳方式。 請閱讀教學課程日期 [在請求中傳送多則訊息](../tutorials/streaming-multiple-messages.md) 以取得詳細資訊。

### 如何知道是否收到我傳送的資料？

所有傳送至的資料 [!DNL Platform] （無論成功與否）會先儲存為批次檔案，然後再保留在資料集中。 批次的處理狀態會顯示在它們被傳送到的資料集中。

您可以使用檢查資料集活動，確認是否已成功擷取資料。 [Experience Platform使用者介面](https://platform.adobe.com). 按一下 **[!UICONTROL 資料集]** 左側導覽中的「 」來顯示資料集清單。 從顯示的清單中選取您要串流到的資料集，以開啟其 **[!UICONTROL 資料集活動]** 頁面，顯示在所選時段內傳送的所有批次。 如需關於使用的詳細資訊 [!DNL Experience Platform] 若要監控資料串流，請參閱以下指南中的 [監控串流資料流程](../quality/monitor-data-ingestion.md).

如果您的資料無法擷取，而您想要從中復原資料 [!DNL Platform]，您可以將失敗批次的ID傳送至 [!DNL Data Access API]. 請參閱指南： [擷取失敗的批次](../quality/retrieve-failed-batches.md) 以取得詳細資訊。

### 為什麼我的串流資料無法在資料湖中使用？

批次擷取可能無法達到的原因有很多 [!DNL Data Lake]，例如格式無效、資料遺失或系統錯誤。 若要判斷批次失敗的原因，您必須使用 [!DNL Data Ingestion Service API] 並檢視其詳細資訊。 如需擷取失敗批次的詳細步驟，請參閱以下指南中的 [擷取失敗的批次](../quality/retrieve-failed-batches.md).

### 如何剖析針對API請求傳回的回應？

您可以先檢查伺服器回應代碼，判斷您的請求是否被接受，藉此剖析回應。 如果傳回成功的回應代碼，您就可以檢閱 `responses` 陣列物件，用來判斷擷取任務的狀態。

成功的單訊息API請求會傳回狀態碼200。 成功（或部分成功）的批次訊息API請求傳回狀態碼207。

以下JSON是API請求的範例回應物件，其中包含兩個訊息：一個成功，一個失敗。 成功串流的訊息傳回 `xactionId` 屬性。 無法串流的訊息會傳回 `statusCode` 屬性和回應 `message` 以取得更多資訊。

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a
                79b25e9421ea127f5] 
                imsOrgId: [{ORG_ID}] 
                Message has unknown xdm format"
        }
    ]
}
```

### 為什麼我傳送的訊息沒有被接收 [!DNL Real-Time Customer Profile]？

若 [!DNL Real-Time Customer Profile] 會拒絕訊息，很可能是因為不正確的身分資訊。 這可能是由於為身分識別提供無效值或名稱空間所導致。

有兩種型別的身分識別名稱空間：預設和自訂。 使用自訂名稱空間時，請確定名稱空間已在中註冊 [!DNL Identity Service]. 請參閱 [身分名稱空間總覽](../../identity-service/namespaces.md) 以取得有關使用預設和自訂名稱空間的詳細資訊。

您可以使用 [[!DNL Experience Platform UI]](https://platform.adobe.com) 以檢視訊息擷取失敗原因的詳細資訊。 按一下 **[!UICONTROL 監視]** 在左側導覽列中，然後檢視 **[!UICONTROL 端對端串流]** 索引標籤以檢視在選取的時段內串流的訊息批次。
