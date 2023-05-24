---
keywords: Experience Platform；首頁；熱門主題；IBM [!DNL IBM DB2]；IBM；ibm [!DNL IBM DB2]；[!DNL IBM DB2]；[!DNL IBM DB2]
solution: Experience Platform
title: 建立IBM [!DNL IBM DB2] 使用流量服務API的基礎連線
type: Tutorial
description: 瞭解如何連結IBM [!DNL IBM DB2] 使用Flow Service API移至Adobe Experience Platform。
exl-id: 83c1dbe6-975f-4e3b-a7bf-166eb5106dd2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# 建立IBM [!DNL IBM DB2] 基礎連線使用 [!DNL Flow Service] API

>[!NOTE]
>
>IBM [!DNL IBM DB2] 聯結器為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用Beta標籤聯結器的詳細資訊。

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL IBM DB2] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL IBM DB2] 使用 [!DNL Flow Service] API。

| 認證 | 描述 |
| ---------- | ----------- |
| `server` | 的名稱 [!DNL IBM DB2] 伺服器。 您可以在以冒號分隔的伺服器名稱后面指定連線埠號碼。 例如：server：port。 |
| `database` | 的名稱 [!DNL IBM DB2] 資料庫。 |
| `username` | 用來連線至的使用者名稱 [!DNL IBM DB2] 資料庫。 |
| `password` | 您為使用者名稱指定的使用者帳戶密碼。 |
| `connectionSpec.id` | 建立連線所需的唯一識別碼。 的連線規格ID [!DNL IBM DB2] 是 `09182899-b429-40c9-a15a-bf3ddbc8ced7`. |

如需入門的詳細資訊，請參閱 [此 [!DNL IBM DB2] 檔案](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL IBM DB2] 要求引數中的驗證認證。

**API格式**

```https
POST /connections
```

**请求**

下列要求會建立 [!DNL IBM DB2]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "[!DNL IBM DB2] connection",
        "description": "[!DNL IBM DB2] test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "server": "{SERVER}",
                    "database": "{DATABASE}",
                    "authenticationType": "{AUTHENTICATION_TYPE}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "09182899-b429-40c9-a15a-bf3ddbc8ced7",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.connectionString` | 與您的關聯的連線字串 [!DNL IBM DB2] 帳戶。 |
| `connectionSpec.id` | 此 [!DNL IBM DB2] 連線規格ID： `09182899-b429-40c9-a15a-bf3ddbc8ced7`. |

**响应**

成功回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "575abae5-c99a-452c-9aba-e5c99ac52c4d",
    "etag": "\"e5012c89-0000-0200-0000-5eaa036b0000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL IBM DB2] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用探索資料表格的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流以使用將資料庫資料帶到Platform [!DNL Flow Service] API](../../collect/database-nosql.md)

