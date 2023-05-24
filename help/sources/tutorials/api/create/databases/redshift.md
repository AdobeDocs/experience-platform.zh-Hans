---
keywords: Experience Platform；首頁；熱門主題；Redshift；Redshift；Amazon Redshift；amazon redshift
solution: Experience Platform
title: 使用流量服務API建立Amazon Redshift基本連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至Amazon Redshift。
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# 建立 [!DNL Amazon Redshift] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Amazon Redshift] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL Amazon Redshift] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Amazon Redshift]，您必須提供下列連線屬性：

| **認證** | **描述** |
| -------------- | --------------- |
| `server` | 與您的關聯的伺服器 [!DNL Amazon Redshift] 帳戶。 |
| `username` | 與您的相關聯的使用者名稱 [!DNL Amazon Redshift] 帳戶。 |
| `password` | 與您的關聯的密碼 [!DNL Amazon Redshift] 帳戶。 |
| `database` | 此 [!DNL Amazon Redshift] 您正在存取的資料庫。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Amazon Redshift] 是 `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

如需入門的詳細資訊，請參閱此 [[!DNL Amazon Redshift] 檔案](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

>[!NOTE]
>
>預設編碼標準 [!DNL Redshift] 是Unicode。 無法變更。

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Amazon Redshift] 要求引數中的驗證認證。

**API格式**

```https
POST /connections
```

**请求**

下列要求會建立 [!DNL Amazon Redshift]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
            }
        },
        "connectionSpec": {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| ------------- | --------------- |
| `auth.params.server` | 您的 [!DNL Amazon Redshift] 伺服器。 |
| `auth.params.database` | 與您的關聯的資料庫 [!DNL Amazon Redshift] 帳戶。 |
| `auth.params.password` | 與您的關聯的密碼 [!DNL Amazon Redshift] 帳戶。 |
| `auth.params.username` | 與您的相關聯的使用者名稱 [!DNL Amazon Redshift] 帳戶。 |
| `connectionSpec.id` | 此 [!DNL Amazon Redshift] 連線規格ID： `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**响应**

成功回應會傳回新建立的連線，包括其唯一識別碼(`id`)。 在下一個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Amazon Redshift] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用探索資料表格的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流以使用將資料庫資料帶到Platform [!DNL Flow Service] API](../../collect/database-nosql.md)
