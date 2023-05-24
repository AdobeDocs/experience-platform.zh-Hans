---
description: 瞭解如何在Experience PlatformUI中建立輸入欄位，讓使用者指定與如何連線及匯出資料至目的地相關的各種資訊。
title: 客戶資料欄位
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 2%

---


# 透過客戶資料欄位設定使用者輸入

在Experience PlatformUI中連線到您的目的地時，您可能需要使用者提供特定的設定詳細資訊，或選取您提供給他們的特定選項。 在Destination SDK中，這些選項稱為客戶資料欄位。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱 [設定選項](../configuration-options.md) 說明檔案，或參閱以下目的地設定概觀頁面：

* [使用Destination SDK設定串流目的地](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK設定檔案型目的地](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

## 客戶資料欄位的使用案例 {#use-cases}

您需要使用者將資料輸入到Experience PlatformUI中的各種使用案例，都使用客戶資料欄位。 例如，當使用者需要提供以下內容時，請使用客戶資料欄位：

* 適用於檔案型目的地的雲端儲存貯體名稱和路徑。
* 客戶資料欄位接受的格式。
* 使用者可選取的可用檔案壓縮型別。
* 即時（串流）整合的可用端點清單。

您可以透過以下方式設定客戶資料欄位： `/authoring/destinations` 端點。 請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面所示的元件。

* [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目的地設定](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文說明可用於目的地的所有支援客戶資料欄位設定型別，並顯示客戶在Experience PlatformUI中會看到的內容。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值皆為 **區分大小寫**. 為避免區分大小寫錯誤，請完全按照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

請參閱下表，以取得關於哪些型別的整合支援本頁面所述功能的詳細資訊。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

## 支援的引數 {#supported-parameters}

建立您自己的客戶資料欄位時，您可以使用下表所述的引數來設定其行為。

| 参数 | 类型 | 必填/可选 | 描述 |
|---------|----------|------|---|
| `name` | 字符串 | 必需 | 為您要引入的自訂欄位命名。 此名稱不會顯示在Platform UI中，除非 `title` 欄位空白或缺失。 |
| `type` | 字符串 | 必需 | 表示您要引入的自訂欄位型別。 接受的值： <ul><li>`string`</li><li>`object`</li><li>`integer`</li></ul> |
| `title` | 字符串 | 可选 | 表示欄位名稱，如客戶在Platform UI中所見。 如果此欄位空白或缺失，UI會繼承中的欄位名稱 `name` 值。 |
| `description` | 字符串 | 可选 | 提供自訂欄位的說明。 此說明不顯示在Platform UI中。 |
| `isRequired` | 布尔值 | 可选 | 指出是否要求使用者在目的地設定工作流程中提供此欄位的值。 |
| `pattern` | 字符串 | 可选 | 如有需要，為自訂欄位強制執行模式。 使用規則運算式強制執行模式。 例如，如果您的客戶ID不包含數字或底線，請輸入 `^[A-Za-z]+$` 在此欄位中。 |
| `enum` | 字符串 | 可选 | 將自訂欄位呈現為下拉式選單，並列出使用者可用的選項。 |
| `default` | 字符串 | 可选 | 從下列專案定義預設值： `enum` 清單。 |
| `hidden` | 布尔值 | 可选 | 指出是否在UI中顯示客戶資料欄位。 |
| `unique` | 布尔值 | 可选 | 當您需要建立客戶資料欄位時，使用此引數，該欄位的值在使用者的組織設定的所有目的地資料流中必須是唯一的。 例如， **[!UICONTROL 整合別名]** 中的欄位 [自訂個人化](../../../catalog/personalization/custom-personalization.md) 目的地必須是唯一的，這表示流向此目的地的兩個獨立資料流不能在此欄位中有相同的值。 |
| `readOnly` | 布尔值 | 可选 | 指出客戶是否可以變更欄位的值。 |

{style="table-layout:auto"}

在以下範例中， `customerDataFields` 區段會定義使用者在連線至目的地時，必須在Platform UI中輸入的兩個欄位：

* `Account ID`：您目的地平台的使用者帳戶ID。
* `Endpoint region`：他們要連線的API的區域端點。 此 `enum` section會建立一個下拉式功能表，其中的值已定義，可供使用者選取。

```json
"customerDataFields":[
   {
      "name":"accountID",
      "title":"User account ID",
      "description":"User account ID for the destination platform.",
      "type":"string",
      "isRequired":true
   },
   {
      "name":"region",
      "title":"API endpoint region",
      "description":"The API endpoint region that the user should connect to.",
      "type":"string",
      "isRequired":true,
      "enum":[
         "EU"
         "US",
      ],
      "readOnly":false,
      "hidden":false
   }
]
```

產生的UI體驗如下圖所示。

![顯示客戶資料欄位範例的Ui影像。](../../assets/functionality/destination-configuration/customer-data-fields-example.png)

## 目的地連線名稱和說明 {#names-description}

建立新目的地時，Destination SDK會自動新增 **[!UICONTROL 名稱]** 和 **[!UICONTROL 說明]** Platform UI中目的地連線畫面的欄位。 如上述範例所示， **[!UICONTROL 名稱]** 和 **[!UICONTROL 說明]** 欄位會在UI中呈現，而不會包含在客戶資料欄位設定中。

>[!IMPORTANT]
>
>如果您新增 **[!UICONTROL 名稱]** 和 **[!UICONTROL 說明]** 客戶資料欄位設定中的欄位，使用者會在UI中看到重複專案。

## 訂購客戶資料欄位 {#ordering}

您在目的地設定中新增客戶資料欄位的順序會反映在Platform UI中。

例如，以下設定會相應地反映在UI中，並依順序顯示選項 **[!UICONTROL 名稱]**， **[!UICONTROL 說明]**， **[!UICONTROL 貯體名稱]**， **[!UICONTROL 資料夾路徑]**， **[!UICONTROL 檔案型別]**， **[!UICONTROL 壓縮格式]**.

```json
"customerDataFields":[
{
   "name":"bucketName",
   "title":"Bucket name",
   "description":"Amazon S3 bucket name",
   "type":"string",
   "isRequired":true,
   "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
   "readOnly":false,
   "hidden":false
},
{
   "name":"path",
   "title":"Folder path",
   "description":"Enter the path to your S3 bucket folder",
   "type":"string",
   "isRequired":true,
   "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
   "readOnly":false,
   "hidden":false
},
{
   "name":"fileType",
   "title":"File Type",
   "description":"Select the exported file type.",
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
}
]
```

![顯示Experience PlatformUI中檔案格式選項順序的影像。](../../assets/functionality/destination-configuration/customer-data-fields-order.png)

## 群組客戶資料欄位 {#grouping}

您可以在一個區段中分組多個客戶資料欄位。 在UI中設定與目的地的連線時，使用者可以看到類似欄位的視覺化分組並從中受益。

若要這麼做，請使用 `"type": "object"` 建立群組，並收集內所需的客戶資料欄位 `properties` 物件，如下圖所示，其中分組 **[!UICONTROL CSV選項]** 會反白顯示。

```json {line-numbers="true" highlight="6-28"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![此影像顯示UI中分組的客戶資料欄位。](../../assets/functionality/destination-configuration/group-customer-data-fields.png)

## 建立客戶資料欄位的下拉式清單選取器 {#dropdown-selectors}

若您希望允許使用者選取數個選項（例如應使用哪個字元來分隔CSV檔案中的欄位），您可以將下拉欄位新增至UI。

若要這麼做，請使用 `namedEnum` 物件，如下所示，並設定 `default` 使用者可選取的選項值。

```json {line-numbers="true" highlight="15-24"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![熒幕錄製，顯示使用上述設定建立的下拉式清單選擇器範例。](../../assets/functionality/destination-configuration/customer-data-fields-dropdown.gif)

## 建立條件式客戶資料欄位 {#conditional-options}

您可以建立條件式客戶資料欄位，這些欄位僅在使用者選取特定選項時才會顯示在啟動工作流程中。

例如，您可以建立條件檔案格式選項，以便在使用者選取特定檔案匯出型別時才會顯示。

以下設定會為CSV檔案格式選項建立條件式群組。 只有在使用者選取CSV作為匯出的所需檔案型別時，才會顯示CSV檔案選項。

若要將欄位設定為條件，請使用 `conditional` 引數，如下所示：

```json
"conditional": {
   "field": "fileType",
   "operator": "EQUALS",
   "value": "CSV"
}
```

在更廣闊的背景中，您可以看到 `conditional` 以下目的地設定中使用的欄位，以及 `fileType` 字串和 `csvOptions` 物件。

```json {line-numbers="true" highlight="3-15, 21-25"}
"customerDataFields":[
   {
      "name":"fileType",
      "title":"File Type",
      "description":"Select your file type",
      "type":"string",
      "isRequired":true,
      "enum":[
         "PARQUET",
         "CSV",
         "JSON"
      ],
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "conditional":{
         "field":"fileType",
         "operator":"EQUALS",
         "value":"CSV"
      },
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"quote",
            "title":"Quote Character",
            "description":"Select your Quote character",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Double Quotes (\")",
                  "value":"\""
               },
               {
                  "name":"Null Character (\u0000)",
                  "value":"\u0000"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"escape",
            "title":"Escape Character",
            "description":"Select your Escape character",
            "type":"string",
            "isRequired":false,
            "default":"\\",
            "namedEnum":[
               {
                  "name":"Back Slash (\\)",
                  "value":"\\"
               },
               {
                  "name":"Single Quote (')",
                  "value":"'"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"emptyValue",
            "title":"Empty Value",
            "description":"Select the output value of blank fields",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"nullValue",
            "title":"Null Value",
            "description":"Select the output value of 'null' fields",
            "type":"string",
            "isRequired":false,
            "default":"null",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ],
      "isRequired":false,
      "readOnly":false,
      "hidden":false
   }
]
```

在下方，您可以根據上述設定檢視產生的UI畫面。 當使用者選擇檔案型別CSV時，參考CSV檔案型別的其他檔案格式選項會顯示在UI中。

![熒幕錄製顯示CSV檔案的條件檔案格式選項。](../../assets/functionality/destination-configuration/customer-data-fields-conditional.gif)

## 存取範本化客戶資料欄位 {#accessing-templatized-fields}

當您的目的地需要使用者輸入時，您必須向使用者提供一系列客戶資料欄位，讓使用者可透過Platform UI填寫這些欄位。 然後，您必須設定目的地伺服器，以從客戶資料欄位正確讀取使用者輸入。 這是透過範本化欄位完成的。

範本化欄位使用格式 `{{customerData.fieldName}}`，其中 `fieldName` 是您從中讀取資訊的客戶資料欄位名稱。 所有範本化客戶資料欄位的前面都會加上 `customerData.` 並括在雙大括弧內 `{{ }}`.

例如，我們考慮下列Amazon S3目的地設定：

```json
"customerDataFields":[
   {
      "name":"bucketName",
      "title":"Enter the name of your Amazon S3 bucket",
      "description":"Amazon S3 bucket name",
      "type":"string",
      "isRequired":true,
      "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"path",
      "title":"Enter the path to your S3 bucket folder",
      "description":"Enter the path to your S3 bucket folder",
      "type":"string",
      "isRequired":true,
      "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
      "readOnly":false,
      "hidden":false
   }
]
```

此設定會提示您的使用者輸入其 [!DNL Amazon S3] 貯體名稱和資料夾路徑對應至其各自的客戶資料欄位。

讓Experience Platform正確連線到 [!DNL Amazon S3]，您的目的地伺服器必須設定為從這兩個客戶資料欄位讀取值，如下所示：

```json
 "fileBasedS3Destination":{
      "bucketName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucketName}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
```

範本化值 `{{customerData.bucketName}}` 和 `{{customerData.path}}` 讀取使用者提供的值，讓Experience Platform可以成功連線至目的地平台。

如需如何設定目的地伺服器以讀取範本化欄位的詳細資訊，請參閱以下檔案： [硬式編碼欄位與範本化欄位](../destination-server/server-specs.md#templatized-fields).

## 后续步骤 {#next-steps}

閱讀本文後，您應該更瞭解如何讓使用者透過客戶資料欄位在Experience PlatformUI中輸入資訊。 您現在也知道如何為使用案例選擇正確的客戶資料欄位，以及在Platform UI中設定、訂購和分組客戶資料欄位。

若要深入瞭解其他目的地元件，請參閱下列文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [UI屬性](ui-attributes.md)
* [結構描述設定](schema-configuration.md)
* [身分名稱空間設定](identity-namespace-configuration.md)
* [支援的對應設定](supported-mapping-configurations.md)
* [目的地傳遞](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [彙總原則](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)