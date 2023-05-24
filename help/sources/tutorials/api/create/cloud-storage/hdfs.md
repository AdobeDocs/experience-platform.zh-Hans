---
keywords: Experience Platform；首頁；熱門主題；ApacheHadoop分散式檔案系統；Apachehadoop；hdfs；HDFS
solution: Experience Platform
title: 使用流量服務API建立Apache HDFS基本連線
type: Tutorial
description: 瞭解如何使用流量服務API將ApacheHadoop分散式檔案系統連線到Adobe Experience Platform。
exl-id: 04fa65db-073c-48e1-b981-425185ae08aa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# 建立 [!DNL Apache] HDFS基本連線使用 [!DNL Flow Service] API

>[!NOTE]
>
>Apache HDFS聯結器為Beta版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用Beta標籤聯結器的詳細資訊。

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Apache Hadoop Distributed File System] (以下稱&quot;[!DNL HDFS]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL HDFS] 使用 [!DNL Flow Service] API。

### 收集必要的認證

| 認證 | 描述 |
| ---------- | ----------- |
| `url` | URL會定義連線至所需的驗證引數 [!DNL HDFS] 匿名。 如需如何取得此值的詳細資訊，請參閱 [此 [!DNL HDFS] 檔案](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL AdWords] 為： `54e221aa-d342-4707-bcff-7a4bceef0001`. |

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL HDFS] 要求引數中的驗證認證。

**API格式**

```http
POST /connections
```

**请求**

下列要求會建立 [!DNL HDFS]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "HDFS test connection",
        "description": "A test connection for an HDFS source",
        "auth": {
            "specName": "Anonymous Authentication",
            "params": {
                "url": "{URL}"
                }
        },
        "connectionSpec": {
            "id": "54e221aa-d342-4707-bcff-7a4bceef0001",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.url` | 定義連線至所需的驗證引數的URL [!DNL HDFS] 匿名 |
| `connectionSpec.id` | 此 [!DNL HDFS] 連線規格ID： `54e221aa-d342-4707-bcff-7a4bceef0001`. |

**响应**

成功回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL HDFS] 使用下列專案的連線： [!DNL Flow Service] API且已取得連線的唯一ID值。 您可在下一個教學課程中使用此ID，瞭解如何 [使用Flow Service API探索協力廠商雲端儲存空間](../../explore/cloud-storage.md).
