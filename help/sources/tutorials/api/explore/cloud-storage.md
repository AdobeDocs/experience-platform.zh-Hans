---
keywords: Experience Platform；首頁；熱門主題；雲端儲存；雲端儲存
title: 使用流量服務API探索雲端儲存資料夾
description: 本教學課程使用流量服務API來探索協力廠商雲端儲存系統。
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: 88e6f084ce1b857f785c4c1721d514ac3b07e80b
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 2%

---

# 使用探索您的雲端儲存資料夾 [!DNL Flow Service] API

本教學課程提供如何使用，探索及預覽雲端儲存空間的結構與內容的步驟。 [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API。

>[!NOTE]
>
>為了探索您的雲端儲存空間，您必須擁有雲端儲存空間來源的有效基本連線ID。 如果您沒有此ID，請參閱 [來源概觀](../../../home.md#cloud-storage) 以取得您可以用來建立基本連線的雲端儲存空間來源清單。

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../landing/api-guide.md).

## 探索您的雲端儲存資料夾

您可以透過向以下發出GET請求，擷取有關雲端儲存資料夾結構的資訊： [!DNL Flow Service] API，同時提供來源的基本連線ID。

執行GET請求以探索您的雲端儲存空間時，您必須包含下表列出的查詢引數：

| 参数 | 描述 |
| --------- | ----------- |
| `objectType` | 您要探索的物件型別。 將此值設定為： <ul><li>`folder`：探索特定目錄</li><li>`root`：探索根目錄。</li></ul> |
| `object` | 只有在檢視特定目錄時才需要此引數。 其值代表您要探索的目錄路徑。 |


**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 雲端儲存空間來源的基本連線ID。 |
| `{PATH}` | 目錄的路徑。 |

**请求**

```shell
curl -X GET \
  'http://platform.adobe.io/data/foundation/flowservice/connections/dc3c0646-5e30-47be-a1ce-d162cb8f1f07/explore?objectType=folder&object=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回在查詢的目錄中找到的檔案和資料夾陣列。 記下 `path` 要上傳之檔案的屬性，因為您必須在下一個步驟中提供該屬性，以檢查其結構。

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "/test-connectors/testFolder-fileIngestion/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "profileData.json",
        "path": "/test-connectors/testFolder-fileIngestion/profileData.json",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "sampleprofile--3.parquet",
        "path": "/test-connectors/testFolder-fileIngestion/sampleprofile--3.parquet",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect檔案的結構

若要從雲端儲存空間檢查資料檔案的結構，請在提供檔案路徑和型別作為查詢引數的同時執行GET請求。

您可以在提供檔案的路徑和型別的同時執行GET請求，從雲端儲存空間來源檢查資料檔案的結構。 您也可以透過指定查詢引數中的檔案型別來檢查不同的檔案型別（例如CSV、TSV或壓縮的JSON和分隔檔案）。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=FILE&object={FILE_PATH}&preview=true&ileType=delimited&encoding=ISO-8859-1;
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 您的雲端儲存空間來源聯結器的連線ID。 |
| `{FILE_PATH}` | 您要檢查的檔案路徑。 |
| `{FILE_TYPE}` | 檔案的型別。 支援的檔案型別包括：<ul><li>已分隔</code>：以分隔符號分隔的值。 DSV檔案必須以逗號分隔。</li><li>JSON</code>：JavaScript物件標籤法。 JSON檔案必須符合XDM規範</li><li>PARQUET</code>：Apache Parquet。 Parquet檔案必須符合XDM標準。</li></ul> |
| `{QUERY_PARAMS}` | 可用來篩選結果的可選查詢引數。 請參閱以下小節： [查詢引數](#query) 以取得詳細資訊。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回查詢檔案的結構，包括表格名稱和資料型別。

```json
[
    {
        "name": "Id",
        "type": "String"
    },
    {
        "name": "FirstName",
        "type": "String"
    },
    {
        "name": "LastName",
        "type": "String"
    },
    {
        "name": "Email",
        "type": "String"
    },
    {
        "name": "Phone",
        "type": "String"
    }
]
```

## 使用查詢引數 {#query}

此 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 支援使用查詢引數來預覽和檢查不同的檔案型別。

| 参数 | 描述 |
| --------- | ----------- |
| `columnDelimiter` | 您指定為欄分隔字元的單一字元值，用於檢查CSV或TSV檔案。 如果未提供引數，則值預設為逗號 `(,)`. |
| `compressionType` | 預覽壓縮分隔或JSON檔案所需的查詢引數。 支援的壓縮檔案包括： <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | 定義呈現預覽時要使用的編碼型別。 支援的編碼型別為： `UTF-8` 和 `ISO-8859-1`. **注意**：此 `encoding` 只有在擷取分隔的CSV檔案時，引數才可用。 其他檔案型別將會以預設編碼擷取。 `UTF-8`. |

## 后续步骤

依照本教學課程，您已探索雲端儲存系統，找到您要帶入的檔案路徑 [!DNL Platform]，並檢視其結構。 您可以在下一個教學課程中使用此資訊來 [從雲端儲存空間收集資料，並將其帶入Platform](../collect/cloud-storage.md).
