---
keywords: Experience Platform；首頁；熱門主題；PostgreSQL；postgresql；PSQL；psql
solution: Experience Platform
title: 使用Flow Service API建立PostgreSQL基本連線
type: Tutorial
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至PostgreSQL。
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 3%

---

# 建立 [!DNL PostgreSQL] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL PostgreSQL] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL PostgreSQL] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL PostgreSQL]，您必須提供下列連線屬性：

| 認證 | 描述 |
| ---------- | ----------- |
| `connectionString` | 與您的關聯的連線字串 [!DNL PostgreSQL] 帳戶。 此 [!DNL PostgreSQL] 連線字串模式為： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL PostgreSQL] 是 `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

如需有關取得連線字串的詳細資訊，請參閱此 [[!DNL PostgreSQL] 檔案](https://www.postgresql.org/docs/9.2/app-psql.html).

#### 為您的連線字串啟用SSL加密

您可以為啟用SSL加密 [!DNL PostgreSQL] 連線字串，方法是使用以下屬性附加您的連線字串：

| 属性 | 描述 | 示例 |
| --- | --- | --- |
| `EncryptionMethod` | 可讓您對啟用SSL加密 [!DNL PostgreSQL] 資料。 | <uL><li>`EncryptionMethod=0`(已禁用)</li><li>`EncryptionMethod=1`(已启用)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | 驗證由您傳送的憑證 [!DNL PostgreSQL] 資料庫時間 `EncryptionMethod` 「 」已套用。 | <uL><li>`ValidationServerCertificate=0`(已禁用)</li><li>`ValidationServerCertificate=1`(已启用)</li></ul> |

以下範例為 [!DNL PostgreSQL] 附加了SSL加密的連線字串： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL PostgreSQL] 要求引數中的驗證認證。

**API格式**

```https
POST /connections
```

**请求**

下列要求會建立 [!DNL PostgreSQL]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for PostgreSQL",
        "description": "Test connection for PostgreSQL",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| ------------- | --------------- |
| `auth.params.connectionString` | 與您的關聯的連線字串 [!DNL PostgreSQL] 帳戶。 此 [!DNL PostgreSQL] 連線字串模式為： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | 此 [!DNL PostgreSQL] 連線規格ID： `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**响应**

成功的回應會傳回唯一識別碼(`id`)建立的基礎連線。 探索您的網站時需要此ID [!DNL PostgreSQL] 資料庫。

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL PostgreSQL] 連線基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用探索資料表格的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流以使用將資料庫資料帶到Platform [!DNL Flow Service] API](../../collect/database-nosql.md)
