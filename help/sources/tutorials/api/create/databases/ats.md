---
keywords: Experience Platform；首頁；熱門主題；[!DNL Azure Table Storage]；[!DNL Azure Table Storage]；Azure資料表儲存體
solution: Experience Platform
title: 使用Flow Service API建立Azure資料表儲存基礎連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Azure Table Storage連線至Adobe Experience Platform。
exl-id: 8ebd5d77-ed1f-47e1-8212-efb6c5e84ec1
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 1%

---

# 建立 [!DNL Azure Table Storage] 基礎連線使用 [!DNL Flow Service] API

>[!NOTE]
>
>此 [!DNL Azure Table Storage] 聯結器為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用Beta標籤聯結器的詳細資訊。

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Azure Table Storage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL Azure Table Storage] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Azure Table Storage]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用來連線至的連線字串 [!DNL Azure Table Storage] 執行個體。 的連線字串模式 [!DNL Azure Table Storage] 為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Azure Table Storage] 是 `ecde33f2-c56f-46cc-bdea-ad151c16cd69`. |

如需有關取得連線字串的詳細資訊，請參閱 [此 [!DNL Azure Table Storage] 檔案](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Azure Table Storage] 要求引數中的驗證認證。

**API格式**

```http
POST /connections
```

**请求**

下列要求會建立 [!DNL Azure Table Storage]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Table Storage connection",
        "description": "Azure Table Storage connection",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.connectionString` | 用來連線至的連線字串 [!DNL Azure Table Storage] 執行個體。 的連線字串模式 [!DNL Azure Table Storage] 為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | 此 [!DNL Azure Table Storage] 連線規格ID： `ecde33f2-c56f-46cc-bdea-ad151c16cd69`. |

**响应**

成功回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "82abddb3-d59a-436c-abdd-b3d59a436c21",
    "etag": "\"7d00fde3-0000-0200-0000-5e84d9430000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Azure Table Storage] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用探索資料表格的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流以使用將資料庫資料帶到Platform [!DNL Flow Service] API](../../collect/database-nosql.md)
