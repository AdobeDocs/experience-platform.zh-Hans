---
description: 此頁面是用來建立認證設定Adobe Experience Platform Destination SDK的API呼叫的範例。
title: 建立認證設定
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 8%

---


# 建立認證設定

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/credentials`

此頁面是您用來建立認證設定的API要求與裝載的範例，使用 `/authoring/credentials` api端點。

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

## 建立認證設定 {#create}

您可以透過以下方式建立新的認證設定： `POST` 向以下專案提出的請求： `/authoring/credentials` 端點。

**API格式**

```http
POST /authoring/credentials
```

以下要求會建立新的認證設定，由承載中提供的引數定義。

選取下方的每個索引標籤以檢視對應的裝載。

>[!BEGINTABS]

>[!TAB 基本]

**建立基本認證設定**

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| 参数 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `url` | 字符串 | 授權提供者的URL |
| `username` | 字符串 | 認證設定登入使用者名稱 |
| `password` | 字符串 | 認證組態登入密碼 |

{style="table-layout:auto"}

+++

+++响应

成功的回應會傳回HTTP狀態200，其中包含您新建立的認證組態的詳細資訊。

+++

>[!TAB Amazon S3]

**建立 [!DNL Amazon S3] 認證設定**

+++**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

| 参数 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `accessId` | 字符串 | [!DNL Amazon S3] 存取識別碼 |
| `secretKey` | 字符串 | [!DNL Amazon S3] 秘密金鑰 |

{style="table-layout:auto"}

+++

+++响应

成功的回應會傳回HTTP狀態200，其中包含您新建立的認證組態的詳細資訊。

+++

>[!TAB SSH]

**建立SSH認證設定**

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   }
}
```

| 参数 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `username` | 字符串 | 認證設定登入使用者名稱 |
| `sshKey` | 字符串 | 使用SSH驗證的SFTP的SSH金鑰 |

{style="table-layout:auto"}

+++

+++响应

成功的回應會傳回HTTP狀態200，其中包含您新建立的認證組態的詳細資訊。

+++

>[!TAB Azure Data Lake儲存]

**建立 [!DNL Azure Data Lake Storage] 認證設定**

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   }
}
```

| 参数 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `url` | 字符串 | 授權提供者的URL |
| `tenant` | 字符串 | Azure Data Lake儲存體租使用者 |
| `servicePrincipalId` | 字符串 | Azure資料湖儲存體的Azure服務主體ID |
| `servicePrincipalKey` | 字符串 | Azure Data Lake儲存體的Azure服務主體金鑰 |

{style="table-layout:auto"}

+++

+++响应

成功的回應會傳回HTTP狀態200，其中包含您新建立的認證組態的詳細資訊。

+++

>[!TAB Azure Blob 存储]

**建立 [!DNL Azure Blob Storage] 認證設定**

+++请求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureConnectionStringAuthentication":{
      "connectionString":"string"
   }
}
```

| 参数 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `connectionString` | 字符串 | [!DNL Azure Blob Storage] 連線字串 |

{style="table-layout:auto"}

+++

+++响应

成功的回應會傳回HTTP狀態200，其中包含您新建立的認證組態的詳細資訊。

+++

>[!ENDTABS]

## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤 {#next-steps}

閱讀本檔案後，您現在知道何時該使用認證端點，以及如何使用設定認證設定 `/authoring/credentials` API端點讀取 [如何使用Destination SDK設定您的目的地](../guides/configure-destination-instructions.md) 以瞭解此步驟在設定目的地的程式中的適用位置。
