---
keywords: Experience Platform；首頁；熱門主題；
solution: Experience Platform
title: 使用Flow Service API將資料登陸區域連線至Adobe Experience Platform
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至資料登陸區。
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 4%

---

# Connect [!DNL Data Landing Zone] 使用Flow Service API移至Adobe Experience Platform

>[!IMPORTANT]
>
>此頁面專屬於 [!DNL Data Landing Zone] *source* Experience Platform中的聯結器。 如需有關連線至 [!DNL Data Landing Zone] *目的地* 聯結器，請參閱 [[!DNL Data Landing Zone] 目的地檔案頁面](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] 是安全的雲端型檔案儲存設施，可將檔案帶入Adobe Experience Platform。 資料會自動從 [!DNL Data Landing Zone] 7天之後。

本教學課程將逐步引導您完成如何建立 [!DNL Data Landing Zone] 來源連線使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). 本教學課程也提供如何擷取 [!DNL Data Landing Zone]以及檢視和重新整理您的認證。

## 快速入门

本指南需要您實際瞭解下列Experience Platform元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

以下小節提供成功建立所需的其他資訊 [!DNL Data Landing Zone] 來源連線使用 [!DNL Flow Service] API。

本教學課程也要求您閱讀以下專案的指南： [Platform API快速入門](../../../../../landing/api-guide.md) 瞭解如何驗證Platform API並解譯檔案中提供的呼叫範例。

## 擷取可用的登陸區域

使用API來存取的第一步 [!DNL Data Landing Zone] 是要向發出GET要求 `/landingzone` 的端點 [!DNL Connectors] API同時提供 `type=user_drop_zone` 作為請求標頭的一部分。

**API格式**

```http
GET /data/foundation/connectors/landingzone?type=user_drop_zone
```

| 标头 | 描述 |
| --- | --- |
| `user_drop_zone` | 此 `user_drop_zone` type可讓API將登陸區域容器與其他型別的容器區分開來。 |

**请求**

以下請求會擷取現有的登陸區域。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**响应**

下列回應會傳回著陸區域的資訊，包括其對應的資訊 `containerName` 和 `containerTTL`.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| 属性 | 描述 |
| --- | --- |
| `containerName` | 您擷取的登陸區域名稱。 |
| `containerTTL` | 登陸區域內套用至您資料的到期時間（以天為單位）。 指定登陸區域中的任何專案都會在七天後刪除。 |

## 擷取 [!DNL Data Landing Zone] 認證

擷取認證 [!DNL Data Landing Zone]，向發出GET要求 `/credentials` 的端點 [!DNL Connectors] API。

**API格式**

```http
GET /data/foundation/connectors/landingzone/credentials?type=user_drop_zone
```

**请求**

以下請求範例會擷取現有登陸區域的認證。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**响应**

以下回應會傳回您登陸區域的認證資訊，包括您目前的 `SASToken` 和 `SASUri`，以及 `storageAccountName` 與您的登陸區域容器相對應。

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| 属性 | 描述 |
| --- | --- |
| `containerName` | 您的登陸區域的名稱。 |
| `SASToken` | 登陸區域的共用存取權簽章權杖。 此字串包含授權請求所需的所有資訊。 |
| `SASUri` | 登陸區域的共用存取簽名URI。 此字串是URI的組合，包含您要驗證身分的登陸區域及其對應的SAS權杖。 |


## 更新 [!DNL Data Landing Zone] 認證

您可以更新 `SASToken` 向發出POST要求 `/credentials` 的端點 [!DNL Connectors] API。

**API格式**

```http
POST /data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| 标头 | 描述 |
| --- | --- |
| `user_drop_zone` | 此 `user_drop_zone` type可讓API將登陸區域容器與其他型別的容器區分開來。 |
| `refresh` | 此 `refresh` 動作可讓您重設登陸區域認證並自動產生新的 `SASToken`. |

**请求**

以下請求會更新您的登陸區域認證。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**响应**

以下回應會傳回您的的更新值 `SASToken` 和 `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## 探索登陸區域檔案結構和內容

您可以透過向以下網站發出GET請求，探索您的登陸區域的檔案結構和內容： `connectionSpecs` 的端點 [!DNL Flow Service] API。

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | 對應至的連線規格ID [!DNL Data Landing Zone]. 此固定ID為： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回在查詢的目錄中找到的檔案和資料夾陣列。 記下 `path` 要上傳之檔案的屬性，因為您必須在下一個步驟中提供它以檢查其結構。

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "dlz-user-container/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "data8.csv",
        "path": "dlz-user-container/data8.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "folder",
        "name": "userdata1",
        "path": "dlz-user-container/userdata1/",
        "canPreview": false,
        "canFetchSchema": false
    }
]
```

## 預覽登陸區域檔案結構和內容

若要檢查登入區域中的檔案結構，請在提供檔案路徑並輸入作為查詢引數的同時，執行GET要求。

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| 参数 | 描述 | 示例 |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | 對應至的連線規格ID [!DNL Data Landing Zone]. 此固定ID為： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
| `{OBJECT_TYPE}` | 您要存取的物件型別。 | `file` |
| `{OBJECT}` | 您要存取之物件的路徑和名稱。 | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | 檔案的型別。 | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | 定義是否支援檔案預覽的布林值。 | </ul><li>`true`</li><li>`false`</li></ul> |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/data8.csv&fileType=delimited&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回查詢檔案的結構，包括檔案名稱和資料型別。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "FirstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "LastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Email": "rsmith@abc.com",
            "FirstName": "Richard",
            "Phone": "111111111",
            "Id": "12345",
            "LastName": "Smith"
        },
        {
            "Email": "morgan@bac.com",
            "FirstName": "Morgan",
            "Phone": "22222222222",
            "Id": "67890",
            "LastName": "Hart"
        }
    ]
}
```

### 使用 `determineProperties` 自動偵測的檔案屬性資訊 [!DNL Data Landing Zone]

您可以使用 `determineProperties` 用於自動偵測檔案內容之屬性資訊的引數， [!DNL Data Landing Zone] 進行GET呼叫以探索來源的內容和結構時。

#### `determineProperties` 使用案例

下表概述您使用時可能會遇到的不同情境 `determineProperties` 查詢引數或手動提供檔案資訊。

| `determineProperties` | `queryParams` | 响应 |
| --- | --- | --- |
| True | 不适用 | 若 `determineProperties` 會提供作為查詢引數，然後就會進行檔案屬性偵測，而且回應會傳回新的 `properties` 包含檔案型別、壓縮型別和欄分隔符號相關資訊的金鑰。 |
| 不适用 | True | 如果檔案型別、壓縮型別和欄分隔符號的值是手動提供的，則為的一部分 `queryParams`，然後會用來產生結構，而相同的屬性會作為回應的一部分傳回。 |
| True | True | 如果兩個選項同時完成，則會傳回錯誤。 |
| 不适用 | 不适用 | 如果兩個選項均未提供，則會傳回錯誤，因為無法取得回應的屬性。 |

**API格式**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| 参数 | 描述 | 示例 |
| --- | --- | --- |
| `determineProperties` | 此查詢引數允許 [!DNL Flow Service] 偵測檔案屬性相關資訊的API，包括檔案型別、壓縮型別和欄分隔符號的相關資訊。 | `true` |

**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/garageWeek/file1&preview=true&determineProperties=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回查詢檔案的結構，包括檔案名稱和資料型別，以及 `properties` 索引鍵，包含相關資訊 `fileType`， `compressionType`、和 `columnDelimiter`.

+++单击这里

```json
{
    "properties": {
        "fileType": "delimited",
        "compressionType": "tarGzip",
        "columnDelimiter": "~"
    },
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "firstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "lastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "birthday",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "birthday": "1313-0505-19731973",
            "firstName": "Yvonne",
            "lastName": "Thilda",
            "id": "100",
            "email": "Yvonne.Thilda@yopmail.com"
        },
        {
            "birthday": "1515-1212-19731973",
            "firstName": "Mary",
            "lastName": "Pillsbury",
            "id": "101",
            "email": "Mary.Pillsbury@yopmail.com"
        },
        {
            "birthday": "0505-1010-19751975",
            "firstName": "Corene",
            "lastName": "Joeann",
            "id": "102",
            "email": "Corene.Joeann@yopmail.com"
        },
        {
            "birthday": "2727-0303-19901990",
            "firstName": "Dari",
            "lastName": "Greenwald",
            "id": "103",
            "email": "Dari.Greenwald@yopmail.com"
        },
        {
            "birthday": "1717-0404-19651965",
            "firstName": "Lucy",
            "lastName": "Magdalen",
            "id": "199",
            "email": "Lucy.Magdalen@yopmail.com"
        }
    ]
}
```

+++

| 属性 | 描述 |
| --- | --- |
| `properties.fileType` | 查詢檔案的對應檔案型別。 支援的檔案型別為： `delimited`， `json`、和 `parquet`. |
| `properties.compressionType` | 用於查詢檔案的對應壓縮型別。 支援的壓縮型別包括： <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | 用於查詢檔案的對應欄分隔符號。 任何單一字元值都是允許的欄分隔符號。 預設值為逗號 `(,)`. |


## 建立來源連線

來源連線會建立和管理與擷取資料之外部來源的連線。 來源連線包含資料來源、資料格式及建立資料流所需的來源連線ID等資訊。 租使用者和組織專屬的來源連線例項。

POST若要建立來源連線，請向 `/sourceConnections` 的端點 [!DNL Flow Service] API。


**API格式**

```http
POST /sourceConnections
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Data Landing Zone source connection",
        "data": {
            "format": "delimited"
        },
        "params": {
            "path": "dlz-user-container/data8.csv"
        },
        "connectionSpec": {
            "id": "26f526f2-58f4-4712-961d-e41bf1ccc0e8",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 您的名稱 [!DNL Data Landing Zone] 來源連線。 |
| `data.format` | 您要帶到Platform的資料格式。 |
| `params.path` | 您要帶到Platform的檔案路徑。 |
| `connectionSpec.id` | 對應至的連線規格ID [!DNL Data Landing Zone]. 此固定ID為： `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**响应**

成功的回應會傳回唯一識別碼(`id`)。 在下個教學課程中，需要此ID才能建立資料流。

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## 后续步骤

依照本教學課程，您已擷取 [!DNL Data Landing Zone] 認證，探索其檔案結構以尋找您要帶到Platform的檔案，並建立來源連線以開始將您的資料帶到Platform。 您現在可以繼續進行下一個教學課程，瞭解如何 [建立資料流，以使用將雲端儲存空間資料帶入Platform [!DNL Flow Service] API](../../collect/cloud-storage.md).
