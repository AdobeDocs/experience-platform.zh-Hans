---
keywords: Experience Platform；首頁；熱門主題；資料準備；api指南；範例資料；
solution: Experience Platform
title: 範例資料API端點
description: 您可以使用Adobe Experience Platform API中的「/samples」端點，以程式設計方式擷取、建立、更新及驗證對應範例資料。
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---


# 範例資料端點

為對應集建立結構描述時，可以使用範例資料。 您可以使用 `/samples` 「資料準備API」中的端點，以程式設計方式擷取、建立和更新範例資料。

## 列出範例資料

您可以透過向以下專案發出GET請求，擷取貴組織的所有對應範例資料清單： `/samples` 端點。

**API格式**

此 `/samples` 端點支援數個查詢引數，以協助篩選結果。 目前，您必須同時包含 `start` 和 `limit` 請求中的引數。

```http
GET /samples?limit={LIMIT}&start={START}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{LIMIT}` | **必需**. 指定傳回的對應範例資料數目。 |
| `{START}` | **必需**. 指定結果頁面的位移。 若要取得結果的第一頁，請將值設為 `start=0`. |

**请求**

以下請求將擷取您組織內最後兩個對應範例資料。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含對應範例資料的最後兩個物件的相關資訊。

```json
{
    "data": [
        {
            "id": "2a429a0057ce47109a4b3e2bc256d755",
            "version": 0,
            "createdDate": 1582250863000,
            "modifiedDate": 1582250863000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        },
        {
            "id": "0248bfb352214f908bdd6cf9c19447e1",
            "version": 0,
            "createdDate": 1582250892000,
            "modifiedDate": 1582250892000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `sampleData` |  |
| `sampleType` |  |

## 建立範例資料

您可以透過向以下發出POST請求來建立範例資料： `/samples` 端點。

```http
POST /samples
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Smith\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含您新建立範例資料的相關資訊。

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## 上傳檔案以建立範例資料

您可以透過向以下網站發出POST請求，使用檔案建立範例資料： `/samples/upload` 端點。

**API格式**

```http
POST /samples/upload
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'file=@{PATH_TO_FILE}.json'
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含您新建立範例資料的相關資訊。

```json
{
    "id": "1fb33209ed126bdcdc0b6c20bae49d8a",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## 查詢特定範例資料物件

您可以在GET請求的路徑中提供其ID，以查詢範例資料的特定物件。 `/samples` 端點。

**API格式**

```http
GET /samples/{SAMPLE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SAMPLE_ID}` | 您要擷取的範例資料物件的ID。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含您要擷取之範例資料物件的資訊。

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404000,
    "modifiedDate": 1615335404000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## 更新範例資料

您可以在PUT請求的路徑中提供特定範例資料物件的ID，以更新該物件。 `/samples` 端點。

**API格式**

```http
PUT /samples/{SAMPLE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SAMPLE_ID}` | 您要更新的範例資料物件的ID。 |

**请求**

以下請求會更新指定的範例資料。 具體來說，它會把姓氏從「Smith」更新為「Lee」。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含更新後範例資料的相關資訊。

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 1,
    "createdDate": 1615335404000,
    "modifiedDate": 1615337870375,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```
