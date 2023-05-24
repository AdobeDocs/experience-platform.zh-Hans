---
keywords: Experience Platform；首頁；熱門主題；一般REST；一般rest
solution: Experience Platform
title: 使用流程服務API建立一般REST API基本連線
type: Tutorial
description: 瞭解如何使用流量服務API將Generic REST API連線到Adobe Experience Platform。
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 1%

---

# 使用建立一般REST API基本連線 [!DNL Flow Service] API

>[!NOTE]
>
>此 [!DNL Generic REST API] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用Beta標籤聯結器的詳細資訊。

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Generic REST API] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Generic REST API]，您必須提供所選驗證型別的有效認證。 [!DNL Generic REST API] 支援OAuth 2重新整理程式碼和基本驗證。 請參閱下清單格，瞭解兩種支援的驗證型別之證明資料的資訊。

#### OAuth 2重新整理程式碼

| 認證 | 描述 |
| --- | --- |
| `host` | 您向其提出請求的來源的主機URL。 此值為必填，不能使用略過 `requestParameterOverride`. |
| `authorizationTestUrl` | （選用）建立基本連線時，會使用授權測試URL來驗證認證。 如果未提供，則會在來源連線建立步驟期間自動檢查認證。 |
| `clientId` | （選用）與您的使用者帳戶相關聯的使用者端ID。 |
| `clientSecret` | （選用）與您的使用者帳戶相關聯的使用者端密碼。 |
| `accessToken` | 用來存取您的應用程式的主要驗證認證。 存取權杖代表應用程式的授權，可存取使用者資料的特定方面。 此值為必填，不能使用略過 `requestParameterOverride`. |
| `refreshToken` | （選用）當存取權杖過期時，用來產生新存取權杖的權杖。 |
| `expirationDate` | （選用）定義存取Token到期日的隱藏值。 |
| `accessTokenUrl` | （選用）用來擷取存取權杖的URL端點。 |
| `requestParameterOverride` | （選用）屬性，可讓您指定要覆寫哪些認證引數。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Generic REST API] 為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

#### 基本驗證

| 認證 | 描述 |
| --- | --- |
| `host` | 您向其提出請求的來源的主機URL。 |
| `username` | 與您的使用者帳戶對應的使用者名稱。 |
| `password` | 與您的使用者帳戶對應的密碼。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Generic REST API] 為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

[!DNL Generic REST API] 支援基本驗證和OAuth 2重新整理程式碼。 請參閱下列範例，以取得如何使用任一驗證型別進行驗證的指引。

### 建立 [!DNL Generic REST API] 使用OAuth 2重新整理程式碼的基礎連線

POST若要使用OAuth 2重新整理程式碼建立基本連線ID，請向 `/connections` 端點，同時提供您的OAuth 2認證。

**API格式**

```http
POST /connections
```

**请求**

下列要求會建立 [!DNL Generic REST API]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Generic REST API base connection with OAuth 2 refresh code",
      "description": "Generic REST API base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `name` | 基礎連線的名稱。 確定基本連線的名稱是描述性的，因為您可以使用此名稱來查閱基本連線的資訊。 |
| `description` | （選用）您可以包含的屬性，以提供基礎連線的詳細資訊。 |
| `connectionSpec.id` | 關聯的連線規格ID [!DNL Generic REST API]. 此固定ID為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | 您用來向Platform驗證來源的驗證型別。 |
| `auth.params.host` | 用來連線至您的網站的根URL [!DNL Generic REST API] 來源。 |
| `auth.params.accessToken` | 用於驗證您的來源的對應存取權杖。 這是OAuth型驗證的必要專案。 |

**响应**

成功回應會傳回新建立的連線，包括其唯一連線識別碼(`id`)。 在下一個教學課程中探索您的資料時，需要此ID。

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### 建立 [!DNL Generic REST API] 使用基本驗證的基本連線

若要建立 [!DNL Generic REST API] 使用基本驗證的基礎連線，向發出POST要求 `/connections` 端點 [!DNL Flow Service] API，同時提供您的基本驗證認證。

**API格式**

```https
POST /connections
```

**请求**

下列要求會建立 [!DNL Generic REST API]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Generic REST API base connection with basic authentication",
      "description": "Generic REST API base connection with basic authentication",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 基礎連線的名稱。 確定基本連線的名稱是描述性的，因為您可以使用此名稱來查閱基本連線的資訊。 |
| `description` | （選用）您可以包含的屬性，以提供基礎連線的詳細資訊。 |
| `connectionSpec.id` | 關聯的連線規格ID [!DNL Generic REST API]. 此固定ID為： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | 您用來將來源連線到Platform的驗證型別。 |
| `auth.params.host` | 用來連線至您的網站的根URL [!DNL Generic REST API] 來源。 |
| `auth.params.username` | 與您的對應之使用者名稱 [!DNL Generic REST API] 來源。 這是進行基本驗證所必需的。 |
| `auth.params.password` | 與您的對應之密碼 [!DNL Generic REST API] 來源。 這是進行基本驗證所必需的。 |

**响应**

成功回應會傳回新建立的基本連線，包括其唯一連線識別碼(`id`)。 在下一個步驟中探索來源的檔案結構和內容時，需要此ID。

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Generic REST API] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用探索資料表格的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，以使用將通訊協定資料帶入Platform [!DNL Flow Service] API](../../collect/protocols.md)
