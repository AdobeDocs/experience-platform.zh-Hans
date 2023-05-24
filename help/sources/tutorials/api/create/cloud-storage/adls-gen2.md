---
keywords: Experience Platform；首頁；熱門主題；Azure Data Lake Storage Gen2；Azure Data Lake儲存；Azure
solution: Experience Platform
title: 使用Flow Service API建立Azure Data Lake Storage Gen2基本連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至Azure Data Lake Storage Gen2。
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 1%

---

# 建立 [!DNL Azure Data Lake Storage Gen2] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Azure Data Lake Storage Gen2] （以下稱「ADLS Gen2」）使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下小節提供您成功建立ADLS Gen2來源連線所需的其他資訊，使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 若要連線到ADLS Gen2，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `url` | ADLS Gen2的端點。 端點模式為： `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | 應用程式的使用者端ID。 |
| `servicePrincipalKey` | 應用程式的金鑰。 |
| `tenant` | 包含您應用程式的租使用者資訊。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 ADLS Gen2的連線規格ID為： `b3ba5556-48be-44b7-8b85-ff2b69b46dc4`. |

如需這些值的詳細資訊，請參閱 [此ADLS Gen2檔案](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供ADLS Gen2驗證認證作為請求引數的一部分。

**API格式**

```http
POST /connections
```

**请求**

下列要求會建立ADLS Gen2的基本連線：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.url` | ADLS Gen2帳戶的URL端點。 |
| `auth.params.servicePrincipalId` | ADLS Gen2帳戶的服務主體ID。 |
| `auth.params.servicePrincipalKey` | ADLS Gen2帳戶的服務主體金鑰。 |
| `auth.params.tenant` | 您ADLS Gen2帳戶的租使用者資訊。 |
| `connectionSpec.id` | ADLS Gen2連線規格ID： `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`. |

**响应**

成功回應會傳回新建立的基本連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## 后续步骤

依照本教學課程所述，您已使用API建立ADLS Gen2連線，且已取得唯一ID作為回應本文的一部分。 您可以使用此連線ID來 [使用流量服務API探索雲端儲存空間](../../explore/cloud-storage.md).
