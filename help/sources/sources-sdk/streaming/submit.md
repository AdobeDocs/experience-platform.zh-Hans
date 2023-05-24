---
title: 測試並提交您的來源
description: 以下檔案提供如何使用Flow Service API測試及驗證新來源，以及透過Self-Serve Sources (Streaming SDK)整合新來源的步驟。
hide: true
hidefromtoc: true
exl-id: 2ae0c3ad-1501-42ab-aaaa-319acea94ec2
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 0%

---

# 測試並提交您的來源

使用自助式來源（串流SDK）將新來源整合到Adobe Experience Platform的最後步驟，是測試並提交新來源。 完成連線規格並更新串流流程規格後，您就可以透過API或UI開始測試來源的功能。 成功後，您可以連絡您的Adobe代表來提交新的來源。

以下檔案提供如何使用測試和偵錯來源的步驟 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

* 如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../landing/api-guide.md).
* 如需如何為Platform API產生認證的詳細資訊，請參閱以下教學課程： [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md).
* 如需如何設定的詳細資訊 [!DNL Postman] 若為Platform API，請參閱以下教學課程： [設定開發人員控制檯和 [!DNL Postman]](../../../landing/postman.md).
* 為協助您的測試和偵錯程式，請下載 [在此提供自助來源驗證收集與環境](../assets/sdk-verification.zip) 並依照下列步驟進行。

## 使用API測試您的來源

若要使用API測試您的來源，您必須執行 [自助來源驗證收集與環境](../assets/sdk-verification.zip) 於 [!DNL Postman] 同時提供與您的來源相關的適當環境變數。

若要開始測試，您必須先設定集合和環境 [!DNL Postman]. 接下來，指定您要測試的連線規格ID。

>[!NOTE]
>
>以下所有範例變數都是您必須更新的預留位置值，以下除外 `flowSpecificationId` 和 `targetConnectionSpecId`，為固定值。

| 参数 | 描述 | 示例 |
| --- | --- | --- |
| `x-api-key` | 用於驗證Experience Platform API呼叫的唯一識別碼。 請參閱教學課程，位置如下： [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md) 以取得如何擷取 `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | 企業實體，可以擁有或授權產品及服務，並允許存取其成員。 請參閱教學課程，位置如下： [設定開發人員控制檯和 [!DNL Postman]](../../../landing/postman.md) 以取得如何擷取 `x-gw-ims-org-id` 資訊。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | 完成對Experience Platform API的呼叫所需的授權權杖。 請參閱教學課程，位置如下： [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md) 以取得如何擷取 `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | 為了在Platform中使用來源資料，必須建立目標結構描述，以根據您的需求來建構來源資料。 如需建立目標XDM結構的詳細步驟，請參閱以下教學課程： [使用API建立結構描述](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | 與您的結構描述對應的唯一版本。 | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | 此 `meta:altId` 此引數會與  `schemaId` 建立新結構描述時。 | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | 如需建立目標資料集的詳細步驟，請參閱以下教學課程： [使用API建立資料集](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | 對應集可用來定義來源結構描述中的資料如何對應到目的地結構描述。 如需如何建立對應的詳細步驟，請參閱以下教學課程： [使用API建立對應集](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | 與對應集對應的唯一ID。 | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | 與您的來源對應的連線規格ID。 這是您產生的ID [建立新的連線規格](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | 的流程規格ID `GenericStreamingAEP`. **此為固定值**. | `e77fde5a-22a8-11ed-861d-0242ac120002` |
| `targetConnectionSpecId` | 擷取資料所在的資料湖的目標連線ID。 **此為固定值**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | 檢查流程執行的完成時要遵循的指定時間間隔。 | `40` |
| `startTime` | 為資料流指定的開始時間。 開始時間的格式必須是unix時間。 | `1597784298` |

提供所有環境變數後，您就可以使用 [!DNL Postman] 介面。 在 [!DNL Postman] 介面，選取省略符號(**...**)旁邊 [!DNL Sources SSSs Verification Collection] 然後選取 **執行集合**.

![執行者](../assets/runner.png)

此 [!DNL Runner] 介面會出現，讓您設定資料流的執行順序。 選取 **執行SSS驗證集合** 以執行集合。

>[!NOTE]
>
>您可以停用 **刪除流量** 如果您偏好使用Platform UI中的來源監控儀表板，請參閱執行訂單檢查清單。 不過，測試完成後，您必須確保刪除測試流程。

![執行集合](../assets/run-collection.png)

## 使用UI測試您的來源

若要在UI中測試您的來源，請前往Platform UI中您組織沙箱的來源目錄。 從這裡，您應該會看到新來源顯示在 *串流* 類別。

由於您的沙箱中現在提供了新來源，您必須按照來源工作流程來測試功能。 若要開始，請選取 **[!UICONTROL 設定]**.

![顯示新串流來源的來源目錄。](../assets/testing/catalog-test.png)

此 [!UICONTROL 新增資料] 步驟隨即顯示。 若要測試您的來源可以串流資料，請使用介面的左側進行上傳 [JSON資料範例](../assets/testing/raw.json.zip). 上傳資料後，介面的右側會更新為資料的檔案階層預覽。 選取 **[!UICONTROL 下一個]** 以繼續進行。

![來源工作流程的新增資料步驟，您可以在其中上傳資料並在擷取前預覽。](../assets/testing/add-data-test.png)

此 [!UICONTROL 資料流詳細資料] 頁面可讓您選取要使用現有資料集還是新資料集。 在此過程中，您也可以設定要擷取至設定檔的資料，並啟用以下設定 [!UICONTROL 錯誤診斷] 和 [!UICONTROL 部分擷取].

若要進行測試，請選取「 」 **[!UICONTROL 新資料集]** 並提供輸出資料集名稱。 在此步驟中，您也可以提供選用的說明，將更多資訊新增至資料集。 接下來，使用 [!UICONTROL 進階搜尋] 選項或透過捲動下拉式選單中的現有結構描述清單的方式。 選取結構描述後，請為資料流提供名稱和說明。

完成後，選取 **[!UICONTROL 下一個]**.

![來源工作流程中的資料流詳細資料步驟。](../assets/testing/dataflow-details-test.png)

此 [!UICONTROL 對應] 步驟隨即顯示，為您提供介面，用於將來源結構描述中的來源欄位對應到目標結構描述中適當的目標XDM欄位。

Platform會根據您選取的目標結構描述或資料集，為自動對應的欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以視需要選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算值或計算值。 如需使用對應程式介面和計算欄位的完整步驟，請參閱 [資料準備UI指南](../../../data-prep/ui/mapping.md)

成功對應來源資料後，請選取 **[!UICONTROL 下一個]**.

![來源工作流程的對應步驟。](../assets/testing/mapping-test.png)

此 **[!UICONTROL 檢閱]** 步驟隨即顯示，可讓您在建立新資料流之前對其進行檢閱。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示您的帳戶名稱、來源型別，以及您使用之串流雲端儲存空間來源的其他特定資訊。
* **[!UICONTROL 指派資料集和對應欄位]**：顯示您用於資料流的目標資料集和結構描述。

檢閱資料流後，選取 **[!UICONTROL 完成]** 並留出一些時間來建立資料流。

![來源工作流程的稽核步驟。](../assets/testing/review-test.png)

最後，您必須擷取資料流的串流端點。 此端點將用於訂閱您的webhook，允許您的串流來源與Experience Platform通訊。 若要擷取您的串流端點，請前往 [!UICONTROL 資料流活動] 您剛建立之資料流的頁面，並從底部複製端點 [!UICONTROL 屬性] 面板。

![資料流活動中的串流端點。](../assets/testing/endpoint-test.png)

## 提交您的來源

您的來源能夠完成整個工作流程後，您可以繼續聯絡您的Adobe代表，並提交您的來源，以跨其他Experience Platform組織整合。
