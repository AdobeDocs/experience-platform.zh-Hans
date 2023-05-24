---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
solution: Experience Platform
title: 使用流量服務API為Mailchimp Campaign建立資料流
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至MailChimp Campaign。
exl-id: fd4821c7-6fe1-4cad-8e13-3549dbe0ce98
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '1942'
ht-degree: 1%

---

# 建立資料流用於 [!DNL Mailchimp Campaign] 使用流量服務API

以下教學課程將逐步引導您完成建立來源連線和資料流的步驟，以便您帶入 [!DNL Mailchimp Campaign] 使用將資料傳送至Platform [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 先决条件

連線之前 [!DNL Mailchimp] 若要使用OAuth 2重新整理程式碼的Adobe Experience Platform，您必須先擷取您的存取權杖 [!DNL MailChimp.] 請參閱 [[!DNL Mailchimp] OAuth 2指南](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/) 以取得尋找存取Token的詳細指示。

## 建立基礎連線 {#base-connection}

擷取您的 [!DNL Mailchimp] 驗證認證，您現在可以開始建立資料流的程式，以帶來 [!DNL Mailchimp Campaign] 資料傳送至Platform。 建立資料流的第一步是建立基礎連線。

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

[!DNL Mailchimp] 支援基本驗證和OAuth 2重新整理程式碼。 請參閱下列範例，以取得如何使用任一驗證型別進行驗證的指引。

### 建立 [!DNL Mailchimp] 使用基本驗證的基本連線

若要建立 [!DNL Mailchimp] 使用基本驗證的基礎連線，向發出POST要求 `/connections` 端點 [!DNL Flow Service] 為API提供認證時 `authorizationTestUrl`， `username`、和 `password`.

**API格式**

```https
POST /connections
```

**请求**

下列要求會建立 [!DNL Mailchimp]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Mailchimp base connection with basic authentication",
      "description": "Mailchimp Campaign base connection with basic authentication",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
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
| `connectionSpec.id` | 來源的連線規格ID。 在您的來源註冊並核准後，您便可以透過擷取此ID [!DNL Flow Service] API。 |
| `auth.specName` | 您用來將來源連線到Platform的驗證型別。 |
| `auth.params.authorizationTestUrl` | （選用）建立基本連線時，會使用授權測試URL來驗證認證。 如果未提供，則會在來源連線建立步驟期間自動檢查認證。 |
| `auth.params.username` | 與您的對應之使用者名稱 [!DNL Mailchimp] 帳戶。 這是進行基本驗證所必需的。 |
| `auth.params.password` | 與您的對應之密碼 [!DNL Mailchimp] 帳戶。 這是進行基本驗證所必需的。 |

**响应**

成功回應會傳回新建立的基本連線，包括其唯一連線識別碼(`id`)。 在下一個步驟中探索來源的檔案結構和內容時，需要此ID。

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

### 建立 [!DNL Mailchimp] 使用OAuth 2重新整理程式碼的基礎連線

若要建立 [!DNL Mailchimp] 基礎連線使用OAuth 2重新整理程式碼，向發出POST要求 `/connections` 提供認證時的端點 `authorizationTestUrl`、和 `accessToken`.

**API格式**

```https
POST /connections
```

**请求**

下列要求會建立 [!DNL Mailchimp]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Mailchimp base connection with OAuth 2 refresh code",
      "description": "Mailchimp Campaign base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 基礎連線的名稱。 確定基本連線的名稱是描述性的，因為您可以使用此名稱來查閱基本連線的資訊。 |
| `description` | （選用）您可以包含的屬性，以提供基礎連線的詳細資訊。 |
| `connectionSpec.id` | 來源的連線規格ID。 在使用註冊來源後，可以擷取此ID [!DNL Flow Service] API。 |
| `auth.specName` | 您用來向Platform驗證來源的驗證型別。 |
| `auth.params.authorizationTestUrl` | （選用）建立基本連線時，會使用授權測試URL來驗證認證。 如果未提供，則會在來源連線建立步驟期間自動檢查認證。 |
| `auth.params.accessToken` | 用於驗證您的來源的對應存取權杖。 這是OAuth型驗證的必要專案。 |

**响应**

成功回應會傳回新建立的基本連線，包括其唯一連線識別碼(`id`)。 在下一個步驟中探索來源的檔案結構和內容時，需要此ID。

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## 探索您的來源 {#explore}

使用您在上一步中產生的基本連線ID，您可以透過執行GET請求來探索檔案和目錄。 執行GET請求以探索來源的檔案結構和內容時，您必須包括下表列出的查詢引數：

| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 在上一步中產生的基本連線ID。 |
| `{OBJECT_TYPE}` | 您要探索的物件型別。 對於REST來源，此值預設為 `rest`. |
| `{OBJECT}` | 您要探索的物件。 |
| `{FILE_TYPE}` | 只有在檢視特定目錄時才需要此引數。 其值代表您要探索的目錄路徑。 |
| `{PREVIEW}` | 定義連線內容是否支援預覽的布林值。 |
| `{SOURCE_PARAMS}` | 的base64編碼字串 `campaign_id`. |

>[!TIP]
>
>擷取接受的格式型別 `{SOURCE_PARAMS}`，您必須將整個 `campaignId` base64中的字串。 例如， `{"campaignId": "c66a200cda"}` 以base64編碼等於 `eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9`.

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&objectType={OBJECT_TYPE}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/05c595e5-edc3-45c8-90bb-fcf556b57c4b/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJjYW1wYWlnbklkIjoiYzY2YTIwMGNkYSJ9' \
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
            "emails": [
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "cff65fb4c5f5828666ad846443720efd",
                    "email_address": "kendall2134@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
                {
                    "campaign_id": "c66a200cda",
                    "list_id": "10c097ca71",
                    "list_is_active": true,
                    "email_id": "a16b82774b211afaf60902d1afd8abc5",
                    "email_address": "logan9935890967@gmail.com",
                    "_links": [
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/CollectionResponse.json"
                        },
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/reports/c66a200cda/email-activity/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Reports/EmailActivity/Response.json"
                        },
                        {
                            "rel": "member",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/a16b82774b211afaf60902d1afd8abc5",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        }
                    ]
                },
            ]
        }
    ]    
}
```

## 建立來源連線 {#source-connection}

您可以向以下發出POST要求來建立來源連線： [!DNL Flow Service] API。 來源連線由連線ID、來源資料檔案的路徑和連線規格ID組成。

若要建立來源連線，您也必須定義資料格式屬性的列舉值。

對檔案型來源使用下列列舉值：

| 資料格式 | 列舉值 |
| ----------- | ---------- |
| 已分隔 | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

對於所有以表格為基礎的來源，將值設定為 `tabular`.

**API格式**

```https
POST /sourceConnections
```

**请求**

以下請求會為建立來源連線 [!DNL Mailchimp]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp source connection to ingest campaign ID",
      "description": "MailChimp Campaign source connection to ingest campaign ID",
      "baseConnectionId": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
      "connectionSpec": {
          "id": "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "campaignId": "c66a200cda"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 來源連線的名稱。 確保來源連線的名稱是描述性的，因為您可以使用此名稱來查閱來源連線的資訊。 |
| `description` | 您可以納入的選擇性值，可提供來源連線的詳細資訊。 |
| `baseConnectionId` | 的基礎連線ID： [!DNL Mailchimp]. 此ID是在先前的步驟中產生的。 |
| `connectionSpec.id` | 與您的來源對應的連線規格ID。 |
| `data.format` | 的格式 [!DNL Mailchimp] 您要擷取的資料。 |
| `params.campaignId` | 此 [!DNL Mailchimp] 行銷活動ID可識別特定 [!DNL Mailchimp] campaign，然後可讓您傳送電子郵件給清單/對象。 |

**响应**

成功的回應會傳回唯一識別碼(`id`)。 此ID在後續步驟中是建立資料流的必要專案。

```json
{
    "id": "d6557bf1-7347-415f-964c-9316bd4cbf56",
    "etag": "\"e205c206-0000-0200-0000-615b5c070000\""
}
```

## 建立目標XDM結構描述 {#target-schema}

為了在Platform中使用來源資料，必須建立目標結構描述，以根據您的需求來建構來源資料。 然後，目標結構描述會用於建立包含來源資料的Platform資料集。

可透過對以下專案執行POST請求來建立目標XDM結構描述： [結構描述登入API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

如需建立目標XDM結構的詳細步驟，請參閱以下教學課程： [使用API建立結構描述](../../../../../xdm/api/schemas.md).

### 建立目標資料集 {#target-dataset}

您可以透過對「 」執行POST請求來建立目標資料集 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，在裝載中提供目標結構描述的ID。

如需建立目標資料集的詳細步驟，請參閱以下教學課程： [使用API建立資料集](../../../../../catalog/api/create-dataset.md).

## 建立目標連線 {#target-connection}

目標連線代表所擷取資料登陸目的地之間的連線。 若要建立目標連線，您必須提供對應至 [!DNL Data Lake]. 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

您現在將目標結構描述、目標資料集和連線規格ID視為唯一識別碼。 [!DNL Data Lake]. 使用這些識別碼，您可以使用 [!DNL Flow Service] 指定將包含傳入來源資料之資料集的API。

**API格式**

```https
POST /targetConnections
```

**请求**

以下請求會建立目標連線 [!DNL Mailchimp]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp target connection",
      "description": "MailChimp Campaign target connection",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6155e3a9bd13651949515f14"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 目標連線的名稱。 確保目標連線的名稱是描述性的，因為您可以使用此名稱來查詢目標連線的資訊。 |
| `description` | 您可以納入的選擇性值，可提供目標連線的詳細資訊。 |
| `connectionSpec.id` | 對應至的連線規格ID [!DNL Data Lake]. 此固定ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 的格式 [!DNL Mailchimp] 您要帶到Platform的資料。 |
| `params.dataSetId` | 在上一步中擷取的目標資料集ID。 |


**响应**

成功回應會傳回新目標連線的唯一識別碼(`id`)。 此ID在後續步驟中是必要的。

```json
{
    "id": "9463fe9c-027d-4347-a423-894fcd105647",
    "etag": "\"b902e822-0000-0200-0000-615b5c370000\""
}
```

>[!IMPORTANT]
>
>目前不支援資料準備功能 [!DNL Mailchimp Campaign].

<!--
## Create a mapping {#mapping}

In order for the source data to be ingested into a target dataset, it must first be mapped to the target schema that the target dataset adheres to. This is achieved by performing a POST request to Conversion Service with data mappings defined within the request payload.

**API format**

```http
POST /conversion/mappingSets
```

**Request**

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
      "xdmSchema": "_{TENANT_ID}.schemas.570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
      "xdmVersion": "1.0",
      "mappings": [
      {
        "destinationXdmPath": "person.name.firstName",
        "sourceAttribute": "merge_fields.FNAME",
        "identity": false,
        "version": 0
      },
      {
        "destinationXdmPath": "person.name.lastName",
        "sourceAttribute": "merge_fields.LNAME",
        "identity": false,
        "version": 0
      }
    ]
  }'
```

| Property | Description |
| --- | --- |
| `xdmSchema` | The ID of the [target XDM schema](#target-schema) generated in an earlier step. |
| `mappings.destinationXdmPath` | The destination XDM path where the source attribute is being mapped to. |
| `mappings.sourceAttribute` | The source attribute that needs to be mapped to a destination XDM path. |
| `mappings.identity` | A boolean value that designates whether the mapping set will be marked for [!DNL Identity Service]. |

**Response**

A successful response returns details of the newly created mapping including its unique identifier (`id`). This value is required in a later step to create a dataflow.

```json
{
    "id": "5a365b23962d4653b9d9be25832ee5b4",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

--->

## 建立流程 {#flow}

最後一步將推出 [!DNL Mailchimp] Platform的資料是用來建立資料流。 到現在為止，您已準備下列必要值：

* [來源連線ID](#source-connection)
* [目標連線ID](#target-connection)

資料流負責從來源排程及收集資料。 您可以執行POST要求，同時在裝載中提供先前提及的值，藉此建立資料流。

若要排程內嵌，您必須先將開始時間值設為以秒為單位的epoch時間。 然後，您必須將頻率值設定為下列五個選項之一： `once`， `minute`， `hour`， `day`，或 `week`. 間隔值會指定兩次連續內嵌與建立一次性內嵌之間的期間(`once`)不需要設定間隔。 對於所有其他頻率，間隔值必須設定為等於或大於 `15`.


**API格式**

```http
POST /flows
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp Campaign dataflow",
      "description": "MailChimp Campaign dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "d6557bf1-7347-415f-964c-9316bd4cbf56"
      ],
      "targetConnectionIds": [
          "9463fe9c-027d-4347-a423-894fcd105647"
      ],
      "scheduleParams": {
          "startTime": "1632809759",
          "frequency": "minute",
          "interval": 15
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 資料流的名稱。 確保資料流的名稱是描述性的，因為您可以使用此名稱來查閱資料流上的資訊。 |
| `description` | （選用）可包含的屬性，可提供資料流的詳細資訊。 |
| `flowSpec.id` | 建立資料流所需的流量規格ID。 此固定ID為： `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | 流程規格ID的對應版本。 此值預設為 `1.0`. |
| `sourceConnectionIds` | 此 [來源連線ID](#source-connection) 已在先前步驟中產生。 |
| `targetConnectionIds` | 此 [目標連線ID](#target-connection) 已在先前步驟中產生。 |
| `scheduleParams.startTime` | 第一次開始擷取資料的指定開始時間。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受的值包括： `once`， `minute`， `hour`， `day`，或 `week`. |
| `scheduleParams.interval` | 間隔會指定兩個連續資料流執行之間的期間。 間隔值應為非零整數。 當頻率設定為時，不需要間隔 `once` 和應大於或等於 `15` （其他頻率值）。 |

**响应**

成功的回應會傳回ID (`id`)。 您可以使用此ID來監視、更新或刪除資料流。

```json
{
    "id": "be2d5249-eeaf-4a74-bdbd-b7bf62f7b2da",
    "etag": "\"7e010621-0000-0200-0000-615b5c9b0000\""
}
```

## 附录

下節提供您可以監視、更新和刪除資料流的步驟相關資訊。

### 監視資料流

建立資料流後，您可以監視透過它擷取的資料，以檢視有關資料流執行、完成狀態和錯誤的資訊。 如需完整的API範例，請閱讀以下指南： [使用API監控您的來源資料流](../../monitor.md).

### 更新您的資料流

透過向以下專案發出PATCH請求，更新資料流的詳細資訊，例如其名稱和說明，及其執行排程和相關聯的對應集 `/flows` 端點 [!DNL Flow Service] API，同時提供資料流的ID。 提出PATCH請求時，您必須提供資料流的 `etag` 在 `If-Match` 標頭。 如需完整的API範例，請閱讀以下指南： [使用API更新來源資料流](../../update-dataflows.md).

### 更新您的帳戶

透過對執行PATCH請求，更新來源帳戶的名稱、說明和認證 [!DNL Flow Service] API時，提供您的基本連線ID作為查詢引數。 提出PATCH請求時，您必須提供來源帳戶的唯一值 `etag` 在 `If-Match` 標頭。 如需完整的API範例，請閱讀以下指南： [使用API更新您的來源帳戶](../../update.md).

### 刪除您的資料流

透過對執行DELETE請求來刪除您的資料流 [!DNL Flow Service] API，同時提供您要作為查詢引數的一部分刪除的資料流的ID。 如需完整的API範例，請閱讀以下指南： [使用API刪除您的資料流](../../delete-dataflows.md).

### 刪除您的帳戶

透過對執行DELETE請求來刪除您的帳戶 [!DNL Flow Service] API，同時提供您要刪除之帳戶的基本連線ID。 如需完整的API範例，請閱讀以下指南： [使用API刪除您的來源帳戶](../../delete.md).