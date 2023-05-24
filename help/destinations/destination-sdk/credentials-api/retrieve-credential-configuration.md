---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK擷取認證設定的API呼叫的範例。
title: 擷取認證設定
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 1%

---


# 擷取認證設定

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/credentials`

此頁面以範例說明API請求和裝載，您可使用這些API請求和裝載來擷取認證設定， `/authoring/credentials` api端點。

## 何時使用 `/credentials` API端點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，您 ***不要*** 需要使用 `/credentials` api端點。 您可以改為透過以下方式設定目的地的驗證資訊： `customerAuthenticationConfigurations` 的引數 `/destinations` 端點。
> 
>讀取 [客戶驗證設定](../functionality/destination-configuration/customer-authentication.md) 以取得支援驗證型別的詳細資訊。

只有在Adobe和您的目的地平台之間存在全域驗證系統，而且 [!DNL Platform] 客戶不需要提供任何驗證認證即可連線至您的目的地。 在此情況下，您必須使用 `/credentials` api端點。

使用全域驗證系統時，您必須設定 `"authenticationRule":"PLATFORM_AUTHENTICATION"` 在 [目的地傳遞](../functionality/destination-configuration/destination-delivery.md) 設定，當 [建立新的目的地組態](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值皆為 **區分大小寫**. 為避免區分大小寫錯誤，請完全按照檔案中所示使用引數名稱和值。

## 認證API操作快速入門 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 如需成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 擷取認證設定 {#retrieve}

您可以擷取 [現有](create-credential-configuration.md) 認證設定，透過發出 `GET` 向以下專案提出的請求： `/authoring/credentials` 端點。

**API格式**

使用以下API格式來擷取您帳戶的所有認證設定。

```http
GET /authoring/credentials
```

使用以下API格式來擷取特定的認證設定，其定義為 `{INSTANCE_ID}` 引數。

```http
GET /authoring/credentials/{INSTANCE_ID}
```

以下兩個請求會擷取您IMS組織的所有認證設定，或特定的認證設定，具體取決於您是否傳遞 `INSTANCE_ID` 請求中的引數。

選取下方的每個索引標籤以檢視對應的裝載。

>[!BEGINTABS]

>[!TAB 擷取所有認證設定]

+++请求

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++响应

成功的回應會傳回HTTP狀態200，其中包含您可存取的認證設定清單，根據 [!DNL IMS Org ID] 以及您使用的沙箱名稱。 一 `instanceId` 對應至一個認證設定。

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
},
{
   "instanceId":"a25bffa0-3127-4030-895d-1d1236bb3680",
   "createdDate":"2022-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2022-08-07T06:41:48.641943Z",
   "type":"basic",
   "name":"yourdestination",
   "s3Authentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

+++

>[!TAB 擷取特定的認證設定]

+++请求

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 参数 | 描述 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 您要擷取的認證設定ID。 |

+++

+++响应

成功的回應會傳回HTTP狀態200，其中包含與對應的認證設定詳細資訊。 `instanceId` 請求時提供。

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

+++

>[!ENDTABS]

## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤 {#next-steps}

閱讀本檔案後，您現在知道如何使用 `/authoring/credentials` api端點。 讀取 [如何使用Destination SDK設定您的目的地](../guides/configure-destination-instructions.md) 以瞭解此步驟在設定目的地的程式中的適用位置。
