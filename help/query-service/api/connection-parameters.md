---
keywords: Experience Platform；首頁；熱門主題；查詢服務；API指南；連線引數；查詢服務；
solution: Experience Platform
title: 連線引數API端點
description: 您可以向/connection_parameters端點發出GET要求，擷取使用互動式服務的連線引數。
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 1%

---

# 連線引數端點

## API呼叫範例

下節會逐步引導您使用完成可用的API呼叫。 [!DNL Query Service] API。 此呼叫包含一般API格式、顯示必要標題的範例要求以及範例回應。

### 要求連線引數

您可以向以下網址發出GET要求，以擷取您的連線引數： `/connection_parameters` 端點。 如需使用連線引數透過互動式服務連線的使用者端詳細資訊，請參閱以下檔案： [查詢服務使用者端](../clients/overview.md).

**API格式**

```http
GET /connection_parameters
```

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態200和您的連線引數。

```json
{
    "username": "{USERNAME}",
    "dbName": "prod:all",
    "host": "{HOSTNAME}",
    "version": 1,
    "port": 80,
    "token": "{TOKEN}",
    "compressedToken": "{COMPRESSED_TOKEN}",
    "websocketHost": "{WEBSOCKET_HOSTNAME}"
}
```
