---
description: 瞭解如何為目的地設定驗證機制，並根據您選取的驗證方法，深入瞭解使用者會在UI中看到的內容。
title: 客戶驗證設定
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 0%

---


# 客戶驗證設定

Experience Platform在提供給合作夥伴和客戶的驗證通訊協定方面提供極大的彈性。 您可以將目的地設定為支援任何業界標準的驗證方法，例如 [!DNL OAuth2]、持有人權杖驗證、密碼驗證等等。

此頁面說明如何使用您偏好的驗證方法來設定目的地。 根據您在建立目的地時使用的驗證設定，客戶在Experience PlatformUI中連線到目的地時會看到不同型別的驗證頁面。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱 [設定選項](../configuration-options.md) 說明檔案，或參閱以下目的地設定概觀頁面：

* [使用Destination SDK設定串流目的地](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK設定檔案型目的地](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

客戶必須先依照「 」中所述的步驟，在Experience Platform和您的目的地之間建立新連線，才能將資料從Platform匯出至您的目的地。 [目的地連線](../../../ui/connect-destination.md) 教學課程。

時間 [建立目的地](../../authoring-api/destination-configuration/create-destination-configuration.md) 透過Destination SDK， `customerAuthenticationConfigurations` 區段會定義客戶在中看到的內容 [驗證畫面](../../../ui/connect-destination.md#authenticate). 根據目的地驗證型別，客戶必須提供各種驗證詳細資訊，例如：

* 針對目的地，使用 [基本驗證](#basic)，使用者必須直接在Experience PlatformUI驗證頁面中提供使用者名稱和密碼。
* 針對目的地，使用 [持有人驗證](#bearer)，使用者必須提供持有人權杖。
* 針對目的地，使用 [OAuth2驗證](#oauth2)，系統會將使用者重新導向至您目的地的登入頁面，以便他們使用其憑證登入。
* 對象 [Amazon S3](#s3) 目的地，使用者必須提供 [!DNL Amazon S3] 存取金鑰和秘密金鑰。
* 對象 [Azure Blob](#blob) 目的地，使用者必須提供 [!DNL Azure Blob] 連線字串。

您可以透過以下方式設定客戶驗證詳細資料： `/authoring/destinations` 端點。 請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面所示的元件。

* [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目的地設定](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文說明可用於目的地的所有支援客戶驗證設定，並顯示根據您為目的地設定的驗證方法，客戶將在Experience PlatformUI中看到的內容。

>[!IMPORTANT]
>
>客戶驗證設定不需要您設定任何引數。 您可以在發生下列情況時，複製並貼上此頁面中顯示的程式碼片段： [建立](../../authoring-api/destination-configuration/create-destination-configuration.md) 或 [更新](../../authoring-api/destination-configuration/update-destination-configuration.md) 目的地設定，您的使用者就會在Platform UI中看到對應的驗證畫面。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值皆為 **區分大小寫**. 為避免區分大小寫錯誤，請完全按照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

請參閱下表，以取得關於哪些型別的整合支援本頁面所述功能的詳細資訊。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

## 驗證規則設定 {#authentication-rule}

使用本頁面所述的任何客戶驗證設定時，請一律設定 `authenticationRule` 中的引數 [目的地傳遞](destination-delivery.md) 至 `"CUSTOMER_AUTHENTICATION"`，如下所示。

```json {line-numbers="true" highlight="4"
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

## 基本驗證 {#basic}

Experience Platform中的即時（串流）整合支援基本驗證。

當您設定基本驗證型別時，使用者必須輸入使用者名稱和密碼才能連線到您的目的地。

![具有基本驗證的UI轉譯](../../assets/functionality/destination-configuration/basic-authentication-ui.png)

若要設定目的地的基本驗證，請設定 `customerAuthenticationConfigurations` 區段透過 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## 持有人驗證 {#bearer}

當您設定持有者驗證型別時，使用者必須輸入他們從您的目的地取得的持有者權杖。

![具有承載者驗證的UI轉譯](../../assets/functionality/destination-configuration/bearer-authentication-ui.png)

若要設定目的地的持有者型別驗證，請設定 `customerAuthenticationConfigurations` 區段透過 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## OAuth 2驗證 {#oauth2}

使用者選取 **[!UICONTROL 連線到目的地]** 以觸發OAuth 2驗證流程至您的目的地，如以下針對Twitter自訂對象目的地的範例所示。 如需有關設定目的地端點的OAuth 2驗證的詳細資訊，請閱讀專屬的 [Destination SDKOAuth 2驗證頁面](oauth2-authentication.md).

![使用OAuth 2驗證呈現UI](../../assets/functionality/destination-configuration/oauth2-authentication-ui.png)

若要設定 [!DNL OAuth2] 驗證您的目的地，設定 `customerAuthenticationConfigurations` 區段透過 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"OAUTH2"
   }
]
```

## Amazon S3驗證 {#s3}

[!DNL Amazon S3] Experience Platform中以檔案為基礎的目的地支援驗證。

設定Amazon S3驗證型別時，使用者必須輸入其S3認證。

![以S3驗證呈現UI](../../assets/functionality/destination-configuration/s3-authentication-ui.png)

若要設定 [!DNL Amazon S3] 驗證您的目的地，設定 `customerAuthenticationConfigurations` 區段透過 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## Azure Blob驗證  {#blob}

[!DNL Azure Blob Storage] Experience Platform中以檔案為基礎的目的地支援驗證。

設定Azure Blob驗證型別時，使用者必須輸入連線字串。

![以Blob驗證呈現UI](../../assets/functionality/destination-configuration/blob-authentication-ui.png)

若要設定 [!DNL Azure Blob] 驗證您的目的地，設定 `customerAuthenticationConfigurations` 中的引數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] 驗證 {#adls}

[!DNL Azure Data Lake Storage] Experience Platform中以檔案為基礎的目的地支援驗證。

當您設定 [!DNL Azure Data Lake Storage] 驗證型別，使用者必須輸入Azure服務主體憑證及其租使用者資訊。

![UI呈現方式 [!DNL Azure Data Lake Storage] 驗證](../../assets/functionality/destination-configuration/adls-authentication-ui.png)

若要設定 [!DNL Azure Data Lake Storage] (ADLS)驗證目的地，請設定 `customerAuthenticationConfigurations` 中的引數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## 具有密碼驗證的SFTP

[!DNL SFTP] Experience Platform中以檔案為基礎的目的地支援使用密碼的驗證。

當您使用密碼驗證型別設定SFTP時，使用者需要輸入SFTP使用者名稱和密碼，以及SFTP網域和連線埠（預設連線埠為22）。

![透過具有密碼驗證的SFTP呈現UI](../../assets/functionality/destination-configuration/sftp-password-authentication-ui.png)

若要以密碼設定目的地的SFTP驗證，請設定 `customerAuthenticationConfigurations` 中的引數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## 具有SSH金鑰驗證的SFTP

[!DNL SFTP] 驗證方式 [!DNL SSH] Experience Platform中以檔案為基礎的目的地支援金鑰。

當您設定具有SSH金鑰驗證型別的SFTP時，使用者需要輸入SFTP使用者名稱和SSH金鑰，以及SFTP網域和連線埠（預設連線埠為22）。

![透過SSH金鑰驗證的SFTP呈現UI](../../assets/functionality/destination-configuration/sftp-key-authentication-ui.png)

若要使用SSH金鑰設定目的地的SFTP驗證，請設定 `customerAuthenticationConfigurations` 中的引數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL Google Cloud Storage] 驗證 {#gcs}

[!DNL Google Cloud Storage] Experience Platform中以檔案為基礎的目的地支援驗證。

當您設定 [!DNL Google Cloud Storage] 驗證型別，使用者必須輸入其 [!DNL Google Cloud Storage] [!UICONTROL 存取金鑰ID] 和 [!UICONTROL 秘密存取金鑰].

![使用Google Cloud Storage驗證呈現UI](../../assets/functionality/destination-configuration/google-cloud-storage-ui.png)

若要設定 [!DNL Google Cloud Storage] 驗證您的目的地，設定 `customerAuthenticationConfigurations` 中的引數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```

## 后续步骤 {#next-steps}

閱讀本文章後，您應該更瞭解如何設定目的地平台的使用者驗證。

若要深入瞭解其他目的地元件，請參閱下列文章：

* [OAuth2驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [結構描述設定](schema-configuration.md)
* [身分名稱空間設定](identity-namespace-configuration.md)
* [支援的對應設定](supported-mapping-configurations.md)
* [目的地傳遞](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [彙總原則](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)