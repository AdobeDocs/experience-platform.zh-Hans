---
description: 瞭解如何透過「/authoring/destination-servers」端點在Adobe Experience Platform Destination SDK中設定目的地伺服器規格。
title: 以Destination SDK建立的目的地的伺服器規格
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2750'
ht-degree: 3%

---


# 以Destination SDK建立的目的地的伺服器規格

目的地伺服器規格會定義從Adobe Experience Platform接收資料的目的地平台型別，以及平台和目的地之間的通訊引數。 例如：

* A [串流](#streaming-example) 目的地伺服器規格會定義從Platform接收HTTP訊息的HTTP伺服器端點。 若要瞭解如何設定端點的HTTP呼叫格式，請閱讀 [範本規格](templating-specs.md) 頁面。
* 一個 [Amazon S3](#s3-example) 目的地伺服器規格會定義 [!DNL S3] Platform將匯出檔案的時段名稱和路徑。
* 一個 [SFTP](#sftp-example) 目的地伺服器規格會定義Platform將匯出檔案之SFTP伺服器的主機名稱、根目錄、通訊連線埠及加密型別。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱 [設定選項](../configuration-options.md) 說明檔案，或參閱以下目的地設定概觀頁面：

* [使用Destination SDK設定串流目的地](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [使用Destination SDK設定檔案型目的地](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

您可以透過以下方式設定目的地伺服器規格 `/authoring/destination-servers` 端點。 請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面所示的元件。

* [建立目的地伺服器設定](../../authoring-api/destination-server/create-destination-server.md)
* [更新目的地伺服器設定](../../authoring-api/destination-server/update-destination-server.md)

此頁面顯示Destination SDK支援的所有目的地伺服器型別及其所有組態引數。 建立目的地時，請以您自己的值取代引數值。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值皆為 **區分大小寫**. 為避免區分大小寫錯誤，請完全按照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

請參閱下表，以取得關於哪些型別的整合支援本頁面所述功能的詳細資訊。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

時間 [建立](../../authoring-api/destination-server/create-destination-server.md) 或 [更新](../../authoring-api/destination-server/update-destination-server.md) 目的地伺服器，請使用此頁面中說明的其中一個伺服器型別組態。 根據您的整合需求，請務必將這些範例中的範例引數值取代為您自己的值。

## 硬式編碼欄位與範本化欄位 {#templatized-fields}

透過Destination SDK建立目的地伺服器時，您可以藉由將設定引數值硬式編碼到設定中，或使用範本化欄位來定義設定引數值。 範本化欄位可讓您從Platform UI讀取使用者提供的值。

目的地伺服器引數有兩個可設定的欄位。 這些選項會指定您是使用硬式編碼值或範本化值。

| 参数 | 类型 | 描述 |
|---|---|---|
| `templatingStrategy` | 字符串 | *必需。* 定義是否透過 `value` 欄位或UI中使用者可設定的值。 支援的值： <ul><li>`NONE`：當您透過以下方式將引數值硬式編碼時，請使用此值： `value` 引數（請參閱下一列）。 示例:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`：如果您希望使用者在UI中提供引數值，請使用此值。 示例：`"value": "{{customerData.bucket}}"`。 </li></ul> |
| `value` | 字符串 | *必需*. 定義引數值。 支援的值型別： <ul><li>**硬式編碼值**：使用硬式編碼值(例如 `"value": "my-storage-bucket"`)時，以免使用者在UI中輸入引數值。 硬式編碼值時， `templatingStrategy` 應一律設為 `NONE`.</li><li>**範本化值**：使用範本化值(例如 `"value": "{{customerData.bucket}}"`)時，以免使用者在使用者介面中提供引數值。 使用範本化值時， `templatingStrategy` 應一律設為 `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### 何時使用硬式編碼欄位或範本化欄位

硬式編碼和範本化欄位在Destination SDK中都有各自的用途，具體取決於您要建立的整合型別。

**無需使用者輸入即可連線到您的目的地**

使用者 [連線到您的目的地](../../../ui/connect-destination.md) 在Platform UI中，您可能會想要處理目的地連線程式，而不需要他們的輸入。

若要這麼做，您可以在伺服器規格中硬式編碼目的地平台連線引數。 當您在目的地伺服器設定中使用硬式編碼引數值時，Adobe Experience Platform與目的地平台之間的連線無需使用者輸入即可處理。

在以下範例中，合作夥伴會使用建立資料登陸區域目的地伺服器 `path.value` 正在硬式編碼的欄位。

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"NONE",
         "value":"Your/hardcoded/path/here"
      },
      "useCase": "Your use case"
   }
}
```

因此，當使用者透過 [目的地連線教學課程](../../../ui/connect-destination.md)，則不會看到 [驗證步驟](../../../ui/connect-destination.md#authenticate). 相反地，驗證是由Platform處理，如下圖所示。

![顯示Platform與DLZ目的地之間驗證畫面的Ui影像。](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**使用使用者輸入連線到您的目的地**

當平台UI中的特定使用者輸入（例如選取API端點或提供欄位值）之後，應該建立Platform和您的目的地之間的連線時，您可以使用伺服器規格中的範本化欄位來讀取使用者輸入並連線到您的目的地平台。

在以下範例中，合作夥伴會建立 [即時（串流）](#streaming-example) 整合與 `url.value` 欄位使用範本化引數 `{{customerData.region}}` 根據使用者輸入來個人化部分API端點。

```json
{
   "name":"Templatized API endpoint example",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.yourcompany.com/data/{{customerData.region}}/items"
      }
   }
}
```

若要讓使用者可以選擇從Platform UI選取值，請 `region` 引數也必須在以下位置定義： [目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md) 作為客戶資料欄位，如下所示：

```json
"customerDataFields":[
   {
      "name":"region",
      "title":"Region",
      "description":"Select an option",
      "type":"string",
      "isRequired":true,
      "readOnly":false,
      "enum":[
         "US",
         "EU"
      ]
   }
```

因此，當使用者透過 [目的地連線教學課程](../../../ui/connect-destination.md)，使用者必須先選取地區，才能連線至目的地平台。 當他們連線到目的地時，範本化的欄位 `{{customerData.region}}` 會取代為使用者在UI中選取的值，如下圖所示。

![顯示具有地區選擇器之目的地連線畫面的Ui影像。](../../assets/functionality/destination-server/server-spec-template-region.png)

## 即時（串流）目的地伺服器 {#streaming-example}

此目的地伺服器型別可讓您透過HTTP請求，將資料從Adobe Experience Platform匯出至您的目的地。 伺服器設定包含接收訊息的伺服器（您這邊的伺服器）的相關資訊。

此程式會以一系列HTTP訊息的形式將使用者資料傳送至您的目的地平台。 以下引數會構成HTTP伺服器規格範本。

以下範例顯示即時（串流）目的地的目的地伺服器設定範例。

```json
{
   "name":"Your destination server name",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{YOUR_API_ENDPOINT}"
      }
   }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | *必需。* 代表伺服器的易記名稱，僅對Adobe可見。 合作夥伴或客戶看不到此名稱。 示例：`Moviestar destination server`。 |
| `destinationServerType` | 字符串 | *必需。* 將此專案設為 `URL_BASED` 適用於串流目的地。 |
| `templatingStrategy` | 字符串 | *必需.* <ul><li>使用 `PEBBLE_V1` 如果您在「 」中使用的是範本化欄位，而不是硬式編碼值 `value` 欄位。 如果您有類似以下的端點，請使用此選項： `https://api.moviestar.com/data/{{customerData.region}}/items`，使用者必須從Platform UI中選取端點區域。 </li><li> 使用 `NONE` 如果Adobe端不需要範本化轉換，例如，如果您有一個端點，例如： `https://api.moviestar.com/data/items` </li></ul> |
| `value` | 字符串 | *必需。* 填入Experience Platform應連線的API端點位址。 |

{style="table-layout:auto"}

## [!DNL Amazon S3] 目的地伺服器 {#s3-example}

此目的地伺服器可讓您將包含Adobe Experience Platform資料的檔案匯出至Amazon S3儲存空間。

以下範例顯示Amazon S3目的地的目的地伺服器設定範例。

```json
{
   "name":"Amazon S3 destination",
   "destinationServerType":"FILE_BASED_S3",
   "fileBasedS3Destination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目的地伺服器的名稱。 |
| `destinationServerType` | 字符串 | 根據您的目的地平台設定此值。 若要將檔案匯出至 [!DNL Amazon S3] 值區，設定為 `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | 字符串 | *必需*. 根據值型別設定此值 `bucket.value` 欄位。<ul><li>如果您希望使用者在Experience PlatformUI中輸入自己的貯體名稱，請將此值設為 `PEBBLE_V1`. 在此情況下，您必須將 `value` 欄位以讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼貯體名稱進行整合，例如 `"bucket.value":"MyBucket"`，然後將此值設定為 `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | 字符串 | 的名稱 [!DNL Amazon S3] 要由此目的地使用的貯體。 這可以是範本化欄位，其將讀取以下欄位的值： [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入（如上述範例所示）或硬式編碼值(例如 `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | 字符串 | *必需*. 根據值型別設定此值 `path.value` 欄位。<ul><li>如果您希望使用者在Experience PlatformUI中輸入自己的路徑，請將此值設為 `PEBBLE_V1`. 在此情況下，您必須將 `path.value` 欄位以讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼路徑進行整合，例如 `"bucket.value":"/path/to/MyBucket"`，然後將此值設定為 `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | 字符串 | 的路徑 [!DNL Amazon S3] 要由此目的地使用的貯體。 這可以是範本化欄位，其將讀取以下欄位的值： [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入（如上述範例所示）或硬式編碼值(例如 `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] 目的地伺服器 {#sftp-example}

此目的地伺服器可讓您將包含Adobe Experience Platform資料的檔案匯出至 [!DNL SFTP] 儲存伺服器。

以下範例顯示SFTP目的地的目的地伺服器設定範例。

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSFTPDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port":22,
      "encryptionMode":"PGP"
   }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目的地伺服器的名稱。 |
| `destinationServerType` | 字符串 | 根據您的目的地平台設定此值。 若要將檔案匯出至 [!DNL SFTP] 目的地，設定為 `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | 字符串 | *必需*. 根據值型別設定此值 `rootDirectory.value` 欄位。<ul><li>如果您希望使用者在Experience PlatformUI中輸入自己的根目錄路徑，請將此值設為 `PEBBLE_V1`. 在此情況下，您必須將 `rootDirectory.value` 欄位，用以讀取使用者提供的值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼的根目錄路徑進行整合，例如 `"rootDirectory.value":"Storage/MyDirectory"`，然後將此值設定為 `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | 字符串 | 存放匯出檔案的目錄路徑。 這可以是範本化欄位，其將讀取以下欄位的值： [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入（如上述範例所示）或硬式編碼值(例如 `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | 字符串 | *必需*. 根據值型別設定此值 `hostName.value` 欄位。<ul><li>如果您希望使用者在Experience PlatformUI中輸入自己的主機名稱，請將此值設為 `PEBBLE_V1`. 在此情況下，您必須將 `hostName.value` 欄位，用以讀取使用者提供的值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼主機名稱進行整合，例如 `"hostName.value":"my.hostname.com"`，然後將此值設定為 `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | 字符串 | SFTP伺服器的主機名稱。 這可以是範本化欄位，其將讀取以下欄位的值： [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入（如上述範例所示）或硬式編碼值(例如 `"hostName.value":"my.hostname.com"`. |
| `port` | 整数 | SFTP檔案伺服器連線埠。 |
| `encryptionMode` | 字符串 | 指示是否使用檔案加密。 支援的值： <ul><li>PGP</li><li>None</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS])目的地伺服器 {#adls-example}

此目的地伺服器可讓您將包含Adobe Experience Platform資料的檔案匯出至 [!DNL Azure Data Lake Storage] 帳戶。

以下範例顯示「 」的目的地伺服器設定範例 [!DNL Azure Data Lake Storage] 目的地。

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目的地連線的名稱。 |
| `destinationServerType` | 字符串 | 根據您的目的地平台設定此值。 對象 [!DNL Azure Data Lake Storage] 目的地，設定為 `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 字符串 | *必需*. 根據值型別設定此值 `path.value` 欄位。<ul><li>如果您希望使用者輸入其 [!DNL ADLS] 在Experience PlatformUI中的資料夾路徑，將此值設定為 `PEBBLE_V1`. 在此情況下，您必須將 `path.value` 欄位以讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼路徑進行整合，例如 `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`，然後將此值設定為 `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | 字符串 | 您的 [!DNL ADLS] 儲存資料夾。 這可以是範本化欄位，其將讀取以下欄位的值： [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入（如上述範例所示）或硬式編碼值(例如 `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] 目的地伺服器 {#blob-example}

此目的地伺服器可讓您將包含Adobe Experience Platform資料的檔案匯出至 [!DNL Azure Blob Storage] 容器。

以下範例顯示「 」的目的地伺服器設定範例 [!DNL Azure Blob Storage] 目的地。

```json
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目的地連線的名稱。 |
| `destinationServerType` | 字符串 | 根據您的目的地平台設定此值。 對象 [!DNL Azure Blob Storage] 目的地，設定為 `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 字符串 | *必需*. 根據值型別設定此值 `path.value` 欄位。<ul><li>如果您希望使用者自行輸入 [!DNL Azure Blob] [儲存體帳戶URI](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) 在Experience PlatformUI中，將此值設定為 `PEBBLE_V1`. 在此情況下，您必須將 `path.value` 從中讀取值的欄位 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼路徑進行整合，例如 `"path.value": "https://myaccount.blob.core.windows.net/"`，然後將此值設定為 `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | 字符串 | 您的 [!DNL Azure Blob] 儲存。 這可以是範本化欄位，其將讀取以下欄位的值： [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入（如上述範例所示）或硬式編碼值(例如 `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 字符串 | *必需*. 根據值型別設定此值 `container.value` 欄位。<ul><li>如果您希望使用者自行輸入 [!DNL Azure Blob] [容器名稱](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) 在Experience PlatformUI中，將此值設定為 `PEBBLE_V1`. 在此情況下，您必須將 `container.value` 從中讀取值的欄位 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼的容器名稱進行整合，例如 `"path.value: myContainer"`，然後將此值設定為 `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | 字符串 | 用於此目的地的Azure Blob儲存體容器的名稱。 這可以是範本化欄位，其將讀取以下欄位的值： [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入（如上述範例所示）或硬式編碼值(例如 `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ])目的地伺服器 {#dlz-example}

此目的地伺服器可讓您將包含Platform資料的檔案匯出至 [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md) 儲存。

以下範例顯示的目標伺服器設定範例。 [!DNL Data Landing Zone] ([!DNL DLZ])目的地。

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目的地連線的名稱。 |
| `destinationServerType` | 字符串 | 根據您的目的地平台設定此值。 對象 [!DNL Data Landing Zone] 目的地，設定為 `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | 字符串 | *必需*. 根據值型別設定此值 `path.value` 欄位。<ul><li>如果您希望使用者自行輸入 [!DNL Data Landing Zone] Experience Platform帳戶時，將此值設為 `PEBBLE_V1`. 在此情況下，您必須將 `path.value` 欄位以讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼路徑進行整合，例如 `"path.value": "https://myaccount.blob.core.windows.net/"`，然後將此值設定為 `NONE`. |
| `fileBasedDlzDestination.path.value` | 字符串 | 存放匯出檔案的目標資料夾路徑。 |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] 目的地伺服器 {#gcs-example}

此目的地伺服器可讓您將包含Platform資料的檔案匯出至 [!DNL Google Cloud Storage] 帳戶。

以下範例顯示的目標伺服器設定範例。 [!DNL Google Cloud Storage] 目的地。

```json
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| 参数 | 类型 | 描述 |
|---|---|---|
| `name` | 字符串 | 目的地連線的名稱。 |
| `destinationServerType` | 字符串 | 根據您的目的地平台設定此值。 對象 [!DNL Google Cloud Storage] 目的地，設定為 `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 字符串 | *必需*. 根據值型別設定此值 `bucket.value` 欄位。<ul><li>如果您希望使用者自行輸入 [!DNL Google Cloud Storage] 值區名稱(在Experience PlatformUI中)，將此值設定為 `PEBBLE_V1`. 在此情況下，您必須將 `bucket.value` 欄位以讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼貯體名稱進行整合，例如 `"bucket.value": "my-bucket"`，然後將此值設定為 `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 字符串 | 的名稱 [!DNL Google Cloud Storage] 要由此目的地使用的貯體。 這可以是範本化欄位，其將讀取以下欄位的值： [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入（如上述範例所示）或硬式編碼值(例如 `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 字符串 | *必需*. 根據值型別設定此值 `path.value` 欄位。<ul><li>如果您希望使用者自行輸入 [!DNL Google Cloud Storage] Experience PlatformUI中的貯體路徑，將此值設定為 `PEBBLE_V1`. 在此情況下，您必須將 `path.value` 欄位以讀取值 [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入。 此使用案例如上述範例所示。</li><li>如果您使用硬式編碼路徑進行整合，例如 `"path.value": "/path/to/my-bucket"`，然後將此值設定為 `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | 字符串 | 的路徑 [!DNL Google Cloud Storage] 此目的地要使用的資料夾。 這可以是範本化欄位，其將讀取以下欄位的值： [客戶資料欄位](../destination-configuration/customer-data-fields.md) 由使用者填入（如上述範例所示）或硬式編碼值(例如 `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## 后续步骤 {#next-steps}

閱讀本文章後，您應該更瞭解什麼是目的地伺服器規格，以及如何進行設定。

若要深入瞭解其他目的地伺服器元件，請參閱下列文章：

* [範本規格](templating-specs.md)
* [消息格式](message-format.md)
* [檔案格式設定](file-formatting.md)
