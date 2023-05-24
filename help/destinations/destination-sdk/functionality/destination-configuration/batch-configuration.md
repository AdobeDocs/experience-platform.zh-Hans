---
description: 瞭解如何為使用Destination SDK建立的目的地設定檔案匯出設定。
title: 批次設定
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 4%

---


# 批次設定 {#batch-configuration}

使用Destination SDK中的批次設定選項可讓使用者自訂匯出的檔案名稱，並根據其偏好設定匯出排程。

當您透過Destination SDK建立以檔案為基礎的目的地時，可以設定預設檔案命名和匯出排程，也可以讓使用者選擇從Platform UI設定這些設定。 例如，您可以設定行為，例如：

* 在檔案名稱中包含特定資訊，例如區段ID、目的地ID或自訂資訊。
* 允許使用者從Platform UI自訂檔案命名。
* 設定檔案匯出在設定的時間間隔發生。
* 定義使用者可在Platform UI中看到的檔案命名和匯出排程自訂選項。

批次組態設定是以檔案為基礎的目的地的目的地組態的一部分。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱 [設定選項](../configuration-options.md) 檔案或參閱操作說明指南 [使用Destination SDK設定以檔案為基礎的目的地](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

您可以透過以下方式設定檔案命名和匯出排程設定： `/authoring/destinations` 端點。 請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面所示的元件。

* [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目的地設定](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文會說明您可用於目的地的所有支援批次設定選項，並顯示客戶會在Platform UI中看到的內容。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值皆為 **區分大小寫**. 為避免區分大小寫錯誤，請完全按照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

請參閱下表，以取得關於哪些型別的整合支援本頁面所述功能的詳細資訊。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 否 |
| 檔案式（批次）整合 | 是 |

## 支援的引數 {#supported-parameters}

您在此設定的值會顯示在 [排程區段匯出](../../../ui/activate-batch-profile-destinations.md#scheduling) 檔案型目的地啟用工作流程的步驟。

```json
"batchConfig":{
   "allowMandatoryFieldSelection":true,
   "allowDedupeKeyFieldSelection":true,
   "defaultExportMode":"DAILY_FULL_EXPORT",
   "allowedExportMode":[
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
   ],
   "allowedScheduleFrequency":[
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
   ],
   "defaultFrequency":"DAILY",
   "defaultStartTime":"00:00",
   "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
   }
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `allowMandatoryFieldSelection` | 布尔值 | 設定為 `true` 讓客戶指定哪些設定檔屬性是強制性的。 默认值为 `false`。另請參閱 [必要屬性](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes) 以取得詳細資訊。 |
| `allowDedupeKeyFieldSelection` | 布尔值 | 設定為 `true` 允許客戶指定重複資料刪除索引鍵。 默认值为 `false`。另請參閱 [重複資料刪除索引鍵](../../../ui/activate-batch-profile-destinations.md#deduplication-keys) 以取得詳細資訊。 |
| `defaultExportMode` | 列舉 | 定義預設檔案匯出模式。 支援的值：<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> 默认值为 `DAILY_FULL_EXPORT`。請參閱 [批次啟用檔案](../../../ui/activate-batch-profile-destinations.md#scheduling) 以取得檔案匯出排程的詳細資訊。 |
| `allowedExportModes` | 列表 | 定義客戶可用的檔案匯出模式。 支援的值：<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | 列表 | 定義可供客戶使用的檔案匯出頻率。 支援的值：<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | 列舉 | 定義預設檔案匯出頻率。支援的值：<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> 默认值为 `DAILY`。 |
| `defaultStartTime` | 字符串 | 定義檔案匯出的預設開始時間。 使用24小時檔案格式。 預設值為「00:00」。 |
| `filenameConfig.allowedFilenameAppendOptions` | 字符串 | *必需*. 可供使用者選擇的可用檔案名稱巨集清單。 這會決定要將哪些專案附加至匯出的檔案名稱（區段ID、組織名稱、匯出的日期和時間等）。 設定時 `defaultFilename`，請務必避免複製巨集。 <br><br>支援的值： <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>無論定義巨集的順序為何，Experience PlatformUI一律會依此處顯示的順序顯示巨集。 <br><br> 若 `defaultFilename` 為空，則 `allowedFilenameAppendOptions` 清單必須至少包含一個巨集。 |
| `filenameConfig.defaultFilenameAppendOptions` | 字符串 | *必需*. 預先選取的預設檔案名稱巨集，使用者可取消核取。<br><br> 此清單中的巨集是中定義巨集的子集 `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | 字符串 | *可选*. 定義匯出檔案的預設檔案名稱巨集。 使用者無法覆寫這些專案。 <br><br>任何巨集定義者 `allowedFilenameAppendOptions` 將會附加在 `defaultFilename` 巨集。 <br><br>若 `defaultFilename` 空白，您必須在中至少定義一個巨集 `allowedFilenameAppendOptions`. |

{style="table-layout:auto"}

## 檔案名稱設定 {#file-name-configuration}

使用檔案名稱組態巨集來定義匯出的檔案名稱應包含的內容。 下表中的巨集說明在UI中找到的元素 [檔案名稱設定](../../../ui/activate-batch-profile-destinations.md#file-names) 畫面。

>[!TIP]
> 
>作為最佳實務，您應一律包含 `SEGMENT_ID` 匯出檔案名稱中的巨集。 區段ID是唯一的，因此將區段ID包含在檔案名稱中也是確保檔案名稱唯一的最佳方式。

| 巨集 | UI標籤 | 描述 | 示例 |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL 目标] | ui中的目的地名稱。 | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL 區段ID] | 平台產生的唯一區段ID | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL 區段名稱] | 使用者定義的區段名稱 | VIP訂閱者 |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL 目的地ID] | 目的地執行個體的唯一Platform產生ID | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL 目的地名稱] | 目的地執行個體的使用者定義名稱。 | 我的2022年廣告目的地 |
| `ORGANIZATION_NAME` | [!UICONTROL 組織名稱] | Adobe Experience Platform中的客戶組織名稱。 | 我的組織名稱 |
| `SANDBOX_NAME` | [!UICONTROL 沙盒名称] | 客戶使用的沙箱名稱。 | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL 日期和时间] | `DATETIME` 和 `TIMESTAMP` 兩者都會定義產生檔案的時間，但格式不同。 <br><br><ul><li>`DATETIME` 會使用以下格式： YYYYMMDD_HHMMSS。</li><li>`TIMESTAMP` 使用10位數Unix格式。 </li></ul> `DATETIME` 和 `TIMESTAMP` 互斥，不能同時使用。 | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL 自訂文字] | 要包含在檔案名稱中的使用者定義自訂文字。 無法用於 `defaultFilename`. | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL 日期和时间] | 檔案產生時間的10位數時間戳記，以Unix格式顯示。 | 1652131584 |

{style="table-layout:auto"}

### 檔案名稱設定範例

以下設定範例顯示API呼叫中使用的設定與UI中顯示的選項之間的對應。

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```

![顯示具有預先選取之巨集的檔案名稱組態畫面的UI影像](../../assets/functionality/destination-configuration/file-name-configuration.png)

## 后续步骤 {#next-steps}

閱讀本文章後，您應該更瞭解如何為檔案型目的地設定檔案命名和匯出排程。

若要深入瞭解其他目的地元件，請參閱下列文章：

* [客戶驗證設定](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [結構描述設定](schema-configuration.md)
* [身分名稱空間設定](identity-namespace-configuration.md)
* [支援的對應設定](supported-mapping-configurations.md)
* [目的地傳遞](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [彙總原則](aggregation-policy.md)
* [歷史設定檔資格](historical-profile-qualifications.md)