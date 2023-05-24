---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
title: 檔案自助服務範本
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至YOURSOURCE。
exl-id: c6927a71-3721-461e-9752-8ebc0b7b1cca
source-git-commit: 74e9774009d086a04351c8ff04cde29348c90c09
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 1%

---

# 建立 *YOURSOURCE* 使用下列專案的連線： [!DNL Flow Service] API

*瀏覽此範本時，請取代或刪除所有斜體段落（從此段落開始）。*

*首先在頁面頂端更新中繼資料（標題和說明）。 請忽略此頁面上的所有DNL執行個體。 此標籤可協助我們的機器翻譯程式將頁面正確翻譯為我們支援的多種語言。 我們會在您提交檔案後，將標籤新增至檔案。*

## 概述

*提供貴公司的簡短概觀，包括其對客戶的價值。 加入產品檔案首頁的連結，以便進一步閱讀。*

>[!IMPORTANT]
>
>此檔案頁面是由 *YOURSOURCE* 團隊。 如有任何查詢或更新請求，請直接聯絡他們： *插入連結或電子郵件地址，您可在這裡取得更新*.

## 先决条件

*在本節中新增客戶在Adobe Experience Platform使用者介面中開始設定來源之前需要注意的任何相關資訊。 這可能與以下內容有關：*

* *需要新增至允許清單*
* *電子郵件雜湊的需求*
* *任何您這邊的帳戶細節*
* *如何取得API金鑰以連線至您的平台*

### 收集必要的認證

為了連線 *YOURSOURCE* 若要Experience Platform，您必須提供下列連線屬性的值：

| 認證 | 描述 | 示例 |
| --- | --- | --- |
| *認證一* | *請在此新增來源驗證認證的簡短說明* | *請在此新增您來源的驗證認證範例* |
| *認證二* | *請在此新增來源驗證認證的簡短說明* | *請在此新增您來源的驗證認證範例* |
| *認證三* | *請在此新增來源驗證認證的簡短說明* | *請在此新增您來源的驗證認證範例* |

如需這些認證的詳細資訊，請參閱 *YOURSOURCE* 驗證檔案。 *請在這裡新增您平台驗證檔案的連結*.

## Connect *YOURSOURCE* 至平台，使用 [!DNL Flow Service] API

下列教學課程將逐步引導您完成建立 *YOURSOURCE* 來源連線並建立資料流以帶來 *YOURSOURCE* 使用將資料傳送至Platform [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### 建立基礎連線 {#base-connection}

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 *YOURSOURCE* 要求內文中的驗證認證。

**API格式**

```https
POST /connections
```

**请求**

下列要求會建立 *YOURSOURCE*：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} base connection",
        "description": "{YOURSOURCE} base connection to authenticate to Platform",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "auth": {
            "specName": "OAuth generic-rest-connector",
            "params": {
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}",
                "expirationDate": "{EXPIRATION_DATE}"
            }
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 基礎連線的名稱。 確定基本連線的名稱是描述性的，因為您可以使用此名稱來查閱基本連線的資訊。 |
| `description` | 您可以納入的選擇性值，可提供基礎連線的詳細資訊。 |
| `connectionSpec.id` | 來源的連線規格ID。 在您的來源註冊並核准後，您便可以透過擷取此ID [!DNL Flow Service] API。 |
| `auth.specName` | 您用來向Platform驗證來源的驗證型別。 |
| `auth.params.` | 包含驗證您的來源所需的認證。 |

**响应**

成功回應會傳回新建立的基本連線，包括其唯一連線識別碼(`id`)。 在下一個步驟中探索來源的檔案結構和內容時，需要此ID。

```json
{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### 探索您的來源 {#explore}

使用您在上一步中產生的基本連線ID，您可以透過執行GET請求來探索檔案和目錄。
使用以下呼叫來尋找您要帶入的檔案路徑 [!DNL Platform]：

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

執行GET請求以探索來源的檔案結構和內容時，您必須包括下表列出的查詢引數：


| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 在上一步中產生的基本連線ID。 |
| `objectType=rest` | 您要探索的物件型別。 目前，此值一律設為 `rest`. |
| `{OBJECT}` | 只有在檢視特定目錄時才需要此引數。 其值代表您要探索的目錄路徑。 |
| `fileType=json` | 您要帶到Platform的檔案型別。 目前， `json` 是唯一支援的檔案型別。 |
| `{PREVIEW}` | 定義連線內容是否支援預覽的布林值。 |
| `{SOURCE_PARAMS}` | 定義您要帶到Platform之來源檔案的引數。 擷取接受的格式型別 `{SOURCE_PARAMS}`，您必須將整個 `list_id` base64中的字串。 在以下範例中， `"list_id": "10c097ca71"` 以base64編碼等於 `eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=`. |


**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/70383d02-2777-4be7-a309-9dd6eea1b46d/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回查詢檔案的結構。

```json
{
  "data": [
    {
      "members": [
        {
          "id": "cff65fb4c5f5828666ad846443720efd",
          "email_address": "roykent@gmail.com",
          "unique_email_id": "72c758cbf1",
          "full_name": "Roy Kent",
          "web_id": 547094062,
          "email_type": "html",
          "status": "subscribed",
          "merge_fields": {
            "FNAME": "Roy",
            "LNAME": "Kent",
            "ADDRESS": {
              "addr1": "",
              "addr2": "",
              "city": "Richmond",
              "state": "Virginia",
              "zip": "",
              "country": "US"
            },
            "PHONE": "",
            "BIRTHDAY": ""
          },
          "stats": {
            "avg_open_rate": 0,
            "avg_click_rate": 0
          },
          "ip_signup": "",
          "timestamp_signup": "",
          "ip_opt": "103.43.112.97",
          "timestamp_opt": "2021-06-01T15:31:36+00:00",
          "member_rating": 2,
          "last_changed": "2021-06-01T15:31:36+00:00",
          "language": "",
          "vip": false,
          "email_client": "",
          "location": {
            "latitude": 0,
            "longitude": 0,
            "gmtoff": 0,
            "dstoff": 0,
            "country_code": "",
            "timezone": ""
          },
          "source": "Admin Add",
          "tags_count": 0,
          "tags": [
             
          ],
          "list_id": "10c097ca71"
        }
      ],
      "list_id": "10c097ca71",
      "total_items": 2,
      "_links": [
        {
          "rel": "self",
          "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
          "method": "GET",
          "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/CollectionResponse.json",
          "schema": "https://us6.api.mailchimp.com/schema/3.0/Paths/Lists/Members/Collection.json"
        },
        {
          "rel": "parent",
          "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71",
          "method": "GET",
          "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
        },
        {
          "rel": "create",
          "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
          "method": "POST",
          "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
          "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/POST.json"
        }
      ]
    }
  ]
}
```

### 建立來源連線 {#source-connection}

您可以向以下發出POST要求來建立來源連線： [!DNL Flow Service] API。 來源連線由連線ID、來源資料檔案的路徑和連線規格ID組成。

**API格式**

```https
POST /sourceConnections
```

**请求**

以下請求會為建立來源連線 *YOURSOURCE*：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} Source Connection",
        "description": "{YOURSOURCE} Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "server": "us6",
            "listId": "10c097ca71"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 來源連線的名稱。 確保來源連線的名稱是描述性的，因為您可以使用此名稱來查閱來源連線的資訊。 |
| `description` | 您可以納入的選擇性值，可提供來源連線的詳細資訊。 |
| `baseConnectionId` | 的基礎連線ID： *YOURSOURCE*. 此ID是在先前的步驟中產生的。 |
| `connectionSpec.id` | 與您的來源對應的連線規格ID。 |
| `data.format` | 的格式 *YOURSOURCE* 您要擷取的資料。 目前唯一支援的資料格式為 `json`. |

**响应**

成功的回應會傳回唯一識別碼(`id`)。 此ID在後續步驟中是建立資料流的必要專案。

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### 建立目標XDM結構描述 {#target-schema}

為了在Platform中使用來源資料，必須建立目標結構描述，以根據您的需求來建構來源資料。 然後，目標結構描述會用於建立包含來源資料的Platform資料集。

可透過對以下專案執行POST請求來建立目標XDM結構描述： [結構描述登入API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

如需建立目標XDM結構的詳細步驟，請參閱以下教學課程： [使用API建立結構描述](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=en#create).

### 建立目標資料集 {#target-dataset}

您可以透過對「 」執行POST請求來建立目標資料集 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，在裝載中提供目標結構描述的ID。

如需建立目標資料集的詳細步驟，請參閱以下教學課程： [使用API建立資料集](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=en).

### 建立目標連線 {#target-connection}

目標連線代表與要儲存所擷取資料的目的地之間的連線。 若要建立目標連線，您必須提供對應至 [!DNL Data Lake]. 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

您現在將目標結構描述、目標資料集和連線規格ID視為唯一識別碼。 [!DNL Data Lake]. 使用這些識別碼，您可以使用 [!DNL Flow Service] 指定將包含傳入來源資料之資料集的API。

**API格式**

```https
POST /targetConnections
```

**请求**

以下請求會建立目標連線 *YOURSOURCE*：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} Target Connection",
        "description": "{YOURSOURCE} Target Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "dataSetId": "5ef4551c52e054191a61a99f"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 目標連線的名稱。 確保目標連線的名稱是描述性的，因為您可以使用此名稱來查詢目標連線的資訊。 |
| `description` | 您可以納入的選擇性值，可提供目標連線的詳細資訊。 |
| `connectionSpec.id` | 對應至的連線規格ID [!DNL Data Lake]. 此固定ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 的格式 *YOURSOURCE* 您要帶到Platform的資料。 |
| `params.dataSetId` | 在上一步中擷取的目標資料集ID。 |


**响应**

成功回應會傳回新目標連線的唯一識別碼(`id`)。 此ID在後續步驟中是必要的。

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### 建立對應 {#mapping}

為了將來源資料內嵌到目標資料集中，必須先將其對應到目標資料集所遵守的目標結構描述。 這是透過向執行POST請求來達成 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) 要求裝載中定義資料對應。

**API格式**

```http
POST /conversion/mappingSets
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| 属性 | 描述 |
| --- | --- |
| `xdmSchema` | 的ID [目標XDM結構描述](#target-schema) 已在先前步驟中產生。 |
| `mappings.destinationXdmPath` | 來源屬性對應到的目的地XDM路徑。 |
| `mappings.sourceAttribute` | 需要對映至目的地XDM路徑的來源屬性。 |
| `mappings.identity` | 布林值，指定是否將對應集標示為 [!DNL Identity Service]. |

**响应**

成功回應會傳回新建立對應的詳細資料，包括其唯一識別碼(`id`)。 在後續步驟中需要此值，才能建立資料流。

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 建立流程 {#flow}

從以下來源取得資料的最後一步 *YOURSOURCE* 對Platform而言，就是建立資料流。 到現在為止，您已準備下列必要值：

* [來源連線ID](#source-connection)
* [目標連線ID](#target-connection)
* [映射 ID](#mapping)

資料流負責從來源排程及收集資料。 您可以執行POST要求，同時在裝載中提供先前提及的值，藉此建立資料流。

若要排程內嵌，您必須先將開始時間值設為以秒為單位的epoch時間。 然後，您必須將頻率值設定為下列五個選項之一： `once`， `minute`， `hour`， `day`，或 `week`. 間隔值會指定兩個連續內嵌之間的期間，但是建立一次性內嵌不需要設定間隔。 對於所有其他頻率，間隔值必須設定為等於或大於 `15`.


**API格式**

```http
POST /flows
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} dataflow",
        "description": "{YOURSOURCE} dataflow",
        "flowSpec": {
            "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "246d052c-da4a-494a-937f-a0d17b1c6cf5"
        ],
        "targetConnectionIds": [
            "7c96c827-3ffd-460c-a573-e9558f72f263"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1625040887",
            "frequency": "minute",
            "interval": 15
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 資料流的名稱。 確保資料流的名稱是描述性的，因為您可以使用此名稱來查閱資料流上的資訊。 |
| `description` | 您可以納入的選用值，可提供資料流的詳細資訊。 |
| `flowSpec.id` | 建立資料流所需的流量規格ID。 此固定ID為： `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | 流程規格ID的對應版本。 此值預設為 `1.0`. |
| `sourceConnectionIds` | 此 [來源連線ID](#source-connection) 已在先前步驟中產生。 |
| `targetConnectionIds` | 此 [目標連線ID](#target-connection) 已在先前步驟中產生。 |
| `transformations` | 此屬性包含套用至您的資料所需的各種轉換。 將非XDM相容的資料引進Platform時，需要此屬性。 |
| `transformations.name` | 指定給轉換的名稱。 |
| `transformations.params.mappingId` | 此 [對應ID](#mapping) 已在先前步驟中產生。 |
| `transformations.params.mappingVersion` | 對應ID的對應版本。 此值預設為 `0`. |
| `scheduleParams.startTime` | 此屬性包含資料流擷取排程的相關資訊。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受的值包括： `once`， `minute`， `hour`， `day`，或 `week`. |
| `scheduleParams.interval` | 間隔會指定兩個連續資料流執行之間的期間。 間隔值應為非零整數。 當頻率設定為時，不需要間隔 `once` 和應大於或等於 `15` （其他頻率值）。 |

**响应**

成功的回應會傳回ID (`id`)。 您可以使用此ID來監視、更新或刪除資料流。

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

## 附录

下節提供您可以監視、更新和刪除資料流的步驟相關資訊。

### 監視資料流

建立資料流後，您可以監視透過它擷取的資料，以檢視有關資料流執行、完成狀態和錯誤的資訊。 如需完整的API範例，請閱讀以下指南： [使用API監控您的來源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### 更新您的資料流

透過向以下專案發出PATCH請求，更新資料流的詳細資訊，例如其名稱和說明，及其執行排程和相關聯的對應集 `/flows` 端點 [!DNL Flow Service] API，同時提供資料流的ID。 提出PATCH請求時，您必須提供資料流的 `etag` 在 `If-Match` 標頭。 如需完整的API範例，請閱讀以下指南： [使用API更新來源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 更新您的帳戶

透過對執行PATCH請求，更新來源帳戶的名稱、說明和認證 [!DNL Flow Service] API時，提供您的基本連線ID作為查詢引數。 提出PATCH請求時，您必須提供來源帳戶的唯一值 `etag` 在 `If-Match` 標頭。 如需完整的API範例，請閱讀以下指南： [使用API更新您的來源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### 刪除您的資料流

透過對執行DELETE請求來刪除您的資料流 [!DNL Flow Service] API，同時提供您要作為查詢引數的一部分刪除的資料流的ID。 如需完整的API範例，請閱讀以下指南： [使用API刪除您的資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### 刪除您的帳戶

透過對執行DELETE請求來刪除您的帳戶 [!DNL Flow Service] API，同時提供您要刪除之帳戶的基本連線ID。 如需完整的API範例，請閱讀以下指南： [使用API刪除您的來源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).