---
keywords: Experience Platform；首頁；熱門主題；Apache Hive；Hive；Hive
solution: Experience Platform
title: 使用流量服務API在Azure HDInsights基本連線上建立Apache Hive
type: Tutorial
description: 瞭解如何使用Flow Service API將Azure HDInsights上的Apache Hive連線到Adobe Experience Platform。
exl-id: e1469a29-6f61-47ba-995e-39f06ee4a4a4
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 1%

---

# 建立 [!DNL Apache Hive] 於 [!DNL Azure HDInsights] 基礎連線使用 [!DNL Flow Service] API

>[!NOTE]
>
>此 [!DNL Apache Hive] 於 [!DNL Azure HDInsights] 聯結器為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用Beta標籤聯結器的詳細資訊。

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Apache Hive] 於 [!DNL Azure HDInsights] (以下稱&quot;[!DNL Hive]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL Hive] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Hive]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `host` | 的IP位址或主機名稱 [!DNL Hive] 伺服器。 |
| `username` | 您用來存取的使用者名稱 [!DNL Hive] 伺服器。 |
| `password` | 與使用者對應的密碼。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Hive] 為： `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |

如需入門的詳細資訊，請參閱 [此Hive檔案](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Hive] 要求引數中的驗證認證。

**API格式**

```https
POST /connections
```

**请求**

下列要求會建立 [!DNL Hive]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Apache Hive test connection",
        "description": "A test connection for Apache Hive",
        "auth": {
            "specName": "HDInsights Basic Authentication",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.connectionString` | 與您的關聯的連線字串 [!DNL Hive] 帳戶。 |
| `connectionSpec.id` | 此 [!DNL Hive] 連線規格ID： `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f`. |

**响应**

成功回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "9f6e4311-e032-4c00-ae43-11e032bc00c7",
    "etag": "\"f4004fb7-0000-0200-0000-5e865c1e0000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Apache Hive] 於 [!DNL Azure HDInsights] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用探索資料表格的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流以使用將資料庫資料帶到Platform [!DNL Flow Service] API](../../collect/database-nosql.md)
