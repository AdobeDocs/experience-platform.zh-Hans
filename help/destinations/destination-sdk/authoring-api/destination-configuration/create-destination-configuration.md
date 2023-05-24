---
description: 瞭解如何建構API呼叫，以透過Adobe Experience Platform Destination SDK建立目的地設定。
title: 建立目的地設定
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 3%

---


# 建立目的地設定

此頁面透過以下範例說明API請求和裝載，您可將其用於建立自己的目的地設定： `/authoring/destinations` api端點。

如需可透過此端點設定的功能的詳細說明，請閱讀以下文章：

* [客戶驗證設定](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth2驗證](../../functionality/destination-configuration/oauth2-authentication.md)
* [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md)
* [UI屬性](../../functionality/destination-configuration/ui-attributes.md)
* [結構描述設定](../../functionality/destination-configuration/schema-configuration.md)
* [身分名稱空間設定](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [目的地傳遞](../../functionality/destination-configuration/destination-delivery.md)
* [對象中繼資料設定](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [對象中繼資料設定](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [彙總原則](../../functionality/destination-configuration/aggregation-policy.md)
* [批次設定](../../functionality/destination-configuration/batch-configuration.md)
* [歷史設定檔資格](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值皆為 **區分大小寫**. 為避免區分大小寫錯誤，請完全按照檔案中所示使用引數名稱和值。

## 目的地設定API操作快速入門 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 如需成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 建立目的地設定 {#create}

您可以透過向發出POST請求來建立新的目的地設定 `/authoring/destinations` 端點。

>[!TIP]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/destinations`

**API格式**

```http
POST /authoring/destinations
```

以下請求會建立新的 [!DNL Amazon S3] 目的地設定，由承載中提供的引數設定。 以下裝載包含接受的檔案型目的地的所有引數 `/authoring/destinations` 端點。

請注意，您不需要將所有引數新增至API呼叫，而且裝載可以根據您的API需求自訂。

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Compression format",
         "description":"Select the desired file compression format.",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"Select a fileType",
         "description":"Select fileType",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false,
         "enum":[
            "csv",
            "json",
            "parquet"
         ],
         "default":"csv"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-amazon-s3-en",
      "category":"cloudStorage",
      "icon":{
         "key":"amazonS3"
      },
      "connectionType":"S3",
      "frequency":"Batch"
   },
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
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
      "backfillHistoricalProfileData":true
   }
}'
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `name` | 字符串 | 指示Experience Platform目錄中目的地的標題。 |
| `description` | 字符串 | 提供Adobe將用於目的地卡片Experience Platform目的地目錄的說明。 目標不超過4-5個句子。 ![顯示目的地說明的平台UI影像。](../../assets/authoring-api/destination-configuration/destination-description.png "目的地說明"){width="100" zoomable="yes"} |
| `status` | 字符串 | 表示目的地卡片的生命週期狀態。 接受的值包括 `TEST`、`PUBLISHED` 和 `DELETED`。使用 `TEST` 當您首次設定目的地時。 |
| `customerAuthenticationConfigurations.authType` | 字符串 | 表示用於向目的地伺服器驗證Experience Platform客戶的設定。 另請參閱 [客戶驗證設定](../../functionality/destination-configuration/customer-authentication.md) 以取得有關支援的驗證型別的詳細資訊。 |
| `customerDataFields.name` | 字符串 | 為您要引入的自訂欄位命名。 <br/><br/> 另請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 以取得這些設定的詳細資訊。 ![顯示客戶資料欄位的平台UI影像。](../../assets/authoring-api/destination-configuration/customer-data-fields.png "客戶資料欄位"){width="100" zoomable="yes"} |
| `customerDataFields.type` | 字符串 | 指出您要引入的自訂欄位型別。 接受的值為 `string`， `object`， `integer`. <br/><br/> 另請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 以取得這些設定的詳細資訊。 |
| `customerDataFields.title` | 字符串 | 表示欄位名稱，如客戶在Experience Platform使用者介面中所見。 <br/><br/> 另請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 以取得這些設定的詳細資訊。 |
| `customerDataFields.description` | 字符串 | 提供自訂欄位的說明。 另請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 以取得這些設定的詳細資訊。 |
| `customerDataFields.isRequired` | 布尔值 | 指出目的地設定工作流程中是否需要此欄位。 <br/><br/> 另請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 以取得這些設定的詳細資訊。 |
| `customerDataFields.enum` | 字符串 | 將自訂欄位呈現為下拉式選單，並列出使用者可用的選項。 <br/><br/> 另請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 以取得這些設定的詳細資訊。 |
| `customerDataFields.default` | 字符串 | 從下列專案定義預設值： `enum` 清單。 |
| `customerDataFields.pattern` | 字符串 | 如有需要，為自訂欄位強制執行模式。 使用規則運算式強制執行模式。 例如，如果您的客戶ID不包含數字或底線，請輸入 `^[A-Za-z]+$` 在此欄位中。 <br/><br/> 另請參閱 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 以取得這些設定的詳細資訊。 |
| `uiAttributes.documentationLink` | 字符串 | 請參閱「 」中的檔案頁面 [目的地目錄](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 以取得您的目的地。 使用 `https://www.adobe.com/go/destinations-YOURDESTINATION-en`，其中 `YOURDESTINATION` 是目的地的名稱。 針對名為Moviestar的目的地，您可以使用 `https://www.adobe.com/go/destinations-moviestar-en`. 請注意，此連結僅在Adobe將您的目的地設定為上線並發佈檔案後有效。 <br/><br/> 另請參閱 [UI屬性](../../functionality/destination-configuration/ui-attributes.md) 以取得這些設定的詳細資訊。 ![顯示檔案連結的平台UI影像。](../../assets/authoring-api/destination-configuration/documentation-url.png "檔案URL"){width="100" zoomable="yes"} |
| `uiAttributes.category` | 字符串 | 是指在Adobe Experience Platform中指派給您的目的地的類別。 如需詳細資訊，請閱讀 [目的地類別](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). 使用下列其中一個值： `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br/><br/> 另請參閱 [UI屬性](../../functionality/destination-configuration/ui-attributes.md) 以取得這些設定的詳細資訊。 |
| `uiAttributes.connectionType` | 字符串 | 連線的型別（視目的地而定）。 支援的值： <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul> |
| `uiAttributes.frequency` | 字符串 | 是指目的地支援的資料匯出型別。 設定為 `Streaming` 針對API型整合，或 `Batch` 將檔案匯出至目的地時。 |
| `identityNamespaces.externalId.acceptsAttributes` | 布尔值 | 指出客戶是否可將標準設定檔屬性對應至您正在設定的身分。 |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 布尔值 | 顯示客戶是否可以對應屬於以下類別的身分： [自訂名稱空間](/help/identity-service/namespaces.md#manage-namespaces) 至您正在設定的身分識別。 |
| `identityNamespaces.externalId.transformation` | 字符串 | _設定範例中未顯示_. 例如，用於 [!DNL Platform] 客戶使用純電子郵件地址作為屬性，而您的平台僅接受雜湊電子郵件。 您可以在此處提供需要套用的轉換（例如，將電子郵件轉換為小寫，然後使用雜湊）。 |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 指示哪一個 [標準身分名稱空間](/help/identity-service/namespaces.md#standard) （例如，IDFA）客戶可以對應至您正在設定的身分。 <br> 當您使用 `acceptedGlobalNamespaces`，您可以使用 `"requiredTransformation":"sha256(lower($))"` 至小寫及雜湊電子郵件地址或電話號碼。 |
| `destinationDelivery.authenticationRule` | 字符串 | 指示如何進行 [!DNL Platform] 客戶連線至您的目的地。 接受的值為 `CUSTOMER_AUTHENTICATION`， `PLATFORM_AUTHENTICATION`， `NONE`. <br> <ul><li>使用 `CUSTOMER_AUTHENTICATION` 如果Platform客戶透過使用者名稱和密碼、持有人權杖或其他驗證方法登入您的系統。 例如，如果您也選取了 `authType: OAUTH2` 或 `authType:BEARER` 在 `customerAuthenticationConfigurations`. </li><li> 使用 `PLATFORM_AUTHENTICATION` 如果Adobe和您的目的地之間存在全域驗證系統，並且 [!DNL Platform] 客戶不需要提供任何驗證認證即可連線至您的目的地。 在此情況下，您必須使用 [認證API](../../credentials-api/create-credential-configuration.md) 設定。 </li><li>使用 `NONE` 如果不需要驗證即可將資料傳送至您的目的地平台。 </li></ul> |
| `destinationDelivery.destinationServerId` | 字符串 | 此 `instanceId` 的 [目的地伺服器範本](../destination-server/create-destination-server.md) 用於此目的地。 |
| `backfillHistoricalProfileData` | 布尔值 | 控制將區段啟用至目的地時，是否匯出歷史設定檔資料。 一律設定為 `true`. |
| `segmentMappingConfig.mapUserInput` | 布尔值 | 控制使用者是否輸入目的地啟用工作流程中的區段對應ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 布尔值 | 控制目的地啟用工作流程中的區段對應ID是否為Experience Platform區段ID。 |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 布尔值 | 控制目的地啟用工作流程中的區段對應ID是否為Experience Platform區段名稱。 |
| `segmentMappingConfig.audienceTemplateId` | 布尔值 | 此 `instanceId` 的 [對象中繼資料範本](../../metadata-api/create-audience-template.md) 用於此目的地。 |
| `schemaConfig.profileFields` | 陣列 | 當您新增預先定義的 `profileFields` 如上述設定所示，使用者可以選擇將Experience Platform屬性對應至目的地側預先定義的屬性。 |
| `schemaConfig.profileRequired` | 布尔值 | 使用 `true` 使用者是否應該能夠將Experience Platform的設定檔屬性對應到您目的地一側的自訂屬性，如上面的設定範例所示。 |
| `schemaConfig.segmentRequired` | 布尔值 | 永遠使用 `segmentRequired:true`. |
| `schemaConfig.identityRequired` | 布尔值 | 使用 `true` 使用者是否應將身分名稱空間從Experience Platform對應至所需的結構描述。 |

{style="table-layout:auto"}

+++

+++响应

成功的回應會傳回HTTP狀態200以及您新建立的目的地組態的詳細資訊。

+++

## API錯誤處理

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤

閱讀本檔案後，您現在知道如何透過Destination SDK建立新的目的地設定 `/authoring/destinations` api端點。

若要進一步瞭解您可以使用此端點做什麼，請參閱下列文章：

* [擷取目的地設定](retrieve-destination-configuration.md)
* [更新目的地設定](update-destination-configuration.md)
* [刪除目的地設定](delete-destination-configuration.md)

若要瞭解此端點適用於目的地撰寫程式的位置，請參閱下列文章：

* [使用Destination SDK設定串流目的地](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK設定檔案型目的地](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)
