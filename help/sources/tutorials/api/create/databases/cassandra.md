---
keywords: Experience Platform；首頁；熱門主題；Apache Cassandra；Apache cassandra；Cassandra；cassandra
solution: Experience Platform
title: 使用流量服務API建立Apache Cassandra來源連線
type: Tutorial
description: 瞭解如何使用流量服務API將Apache Cassandra連線至Adobe Experience Platform。
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 2%

---


# 建立 [!DNL Apache Cassandra] 來源連線使用 [!DNL Flow Service] API

[!DNL Flow Service] 用於收集及集中Adobe Experience Platform內各種不同來源的客戶資料。 此服務提供可連線所有支援來源的使用者介面和RESTful API。

本教學課程使用 [!DNL Flow Service] API可引導您完成連線的步驟 [!DNL Apache Cassandra] （以下稱「Cassandra」）以 [!DNL Experience Platform].

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供您需要瞭解的其他資訊，以便使用成功連線到Cassandra [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Cassandra]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `host` | 的IP位址或主機名稱 [!DNL Cassandra] 伺服器。 |
| `port` | TCP連線埠， [!DNL Cassandra] 伺服器使用來監聽使用者端連線。 預設連線埠為 `9042`. |
| `username` | 用來連線至的使用者名稱 [!DNL Cassandra] 用於驗證的伺服器。 |
| `password` | 連線至的密碼 [!DNL Cassandra] 用於驗證的伺服器。 |
| `connectionSpec.id` | 建立連線所需的唯一識別碼。 的連線規格ID [!DNL Cassandra] 是 `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

如需入門的詳細資訊，請參閱 [這個Cassandra檔案](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### 讀取範例API呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

* 授權：持有人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括屬於 [!DNL Flow Service]，會隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* Content-Type: `application/json`

## 创建连接

連線會指定來源，並包含該來源的認證。 每個只需要一個聯結器 [!DNL Cassandra] 帳戶，因為它可用來建立多個來源聯結器以引入不同的資料。

**API格式**

```http
POST /connections
```

**请求**

為了建立 [!DNL Cassandra] 連線，其唯一的連線規格ID必須作為POST請求的一部分提供。 的連線規格ID [!DNL Cassandra] 是 `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cassandra test connection",
        "description": "A test connection for Cassandra",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST},
                    "port": "{PORT}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.host` | 的IP位址或主機名稱 [!DNL Cassandra] 伺服器。 |
| `auth.params.port` | TCP連線埠， [!DNL Cassandra] 伺服器使用來監聽使用者端連線。 預設連線埠為 `9042`. |
| `auth.params.username` | 用來連線至的使用者名稱 [!DNL Cassandra] 用於驗證的伺服器。 |
| `auth.params.password` | 連線至的密碼 [!DNL Cassandra] 用於驗證的伺服器。 |
| `connectionSpec.id` | 此 [!DNL Cassandra] 連線規格ID： `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**响应**

成功回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Cassandra] 使用下列專案的連線： [!DNL Flow Service] API且已取得連線的唯一ID值。 您可在下一個教學課程中使用此ID，瞭解如何 [使用流量服務API探索資料庫](../../explore/database-nosql.md).
