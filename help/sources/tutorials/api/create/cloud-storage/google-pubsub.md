---
title: 使用Flow Service API建立Google PubSub來源連線
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至Google PubSub帳戶。
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: 371947cff518c16816692210054680367fd6504c
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---

# 建立 [!DNL Google PubSub] 使用流量服務API的來源連線

本教學課程將逐步引導您完成連線的步驟 [!DNL Google PubSub] (以下稱&quot;[!DNL PubSub]&quot;)進行Experience Platform，使用 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL PubSub] 至平台，使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線到 [!DNL PubSub]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `projectId` | 驗證所需的專案ID [!DNL PubSub]. |
| `credentials` | 驗證所需的認證或金鑰 [!DNL PubSub]. |
| `topicName` | 代表訊息摘要的資源名稱。 如果您想要提供對以下專案中的特定資料流的存取權，則必須指定主題名稱： [!DNL PubSub] 來源。 主題名稱格式為： `projects/{PROJECT_ID}/topics/{TOPIC_ID}`. |
| `subscriptionName` | 您的名稱 [!DNL PubSub] 訂閱。 在 [!DNL PubSub]，訂閱可讓您透過訂閱訊息已發佈到的主題來接收訊息。 **注意**：單一 [!DNL PubSub] 訂閱只能用於一個資料流。 若要建立多個資料流，您必須有多個訂閱。 訂閱名稱格式為： `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}`. |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎和來源目標連線相關的驗證規格。 此 [!DNL PubSub] 連線規格ID為： `70116022-a743-464a-bbfe-e226a7f8210c`. |

如需這些值的詳細資訊，請參閱此 [[!DNL PubSub] 驗證](https://cloud.google.com/pubsub/docs/authentication) 檔案。 若要使用以服務帳戶為基礎的驗證，請參閱此 [[!DNL PubSub] 建立服務帳戶的指南](https://cloud.google.com/docs/authentication/production#create_service_account) 瞭解如何產生認證的步驟。

>[!TIP]
>
>如果您使用以服務帳戶為基礎的驗證，在複製和貼上您的認證時，請確保您已授予足夠的使用者存取權給您的服務帳戶，並且JSON中沒有額外的空格。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

建立來源連線的第一個步驟是驗證您的 [!DNL PubSub] 來源並產生基本連線ID。 基礎連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL PubSub] 要求引數中的驗證認證。

此 [!DNL PubSub] 來源可讓您指定在驗證期間允許使用的存取型別。 您可以將帳戶設定為擁有根存取權，或限制特定專案的存取權 [!DNL PubSub] 主題和訂閱。

>[!NOTE]
>
>指派給使用者的主體（角色） [!DNL PubSub] 專案會繼承內建立的所有主題和訂閱 [!DNL PubSub] 專案。 如果您希望主參與者（角色）有權存取特定主題，則也必須將該主參與者（角色）新增至主題的對應訂閱。 如需詳細資訊，請閱讀 [[!DNL PubSub] 存取控制檔案](<https://cloud.google.com/pubsub/docs/access-control>).

**API格式**

```http
POST /connections
```

**请求**

>[!BEGINTABS]

>[!TAB 專案型驗證]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Project Based Authentication",
          "params": {
              "projectId": "{PROJECT_ID}",
              "credentials": "{CREDENTIALS}"
          }
      },
      "connectionSpec": {
          "id": "70116022-a743-464a-bbfe-e226a7f8210c",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.projectId` | 驗證所需的專案ID [!DNL PubSub]. |
| `auth.params.credentials` | 驗證所需的認證或金鑰 [!DNL PubSub]. |
| `connectionSpec.id` | 此 [!DNL PubSub] 連線規格ID： `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!TAB 主題和訂閱型驗證]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Topic & Subscription Based Authentication",
          "params": {
              "credentials": "{CREDENTIALS}",
              "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
              "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}"
          }
      },
      "connectionSpec": {
          "id": "70116022-a743-464a-bbfe-e226a7f8210c",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.credentials` | 驗證所需的認證或金鑰 [!DNL PubSub]. |
| `auth.params.topicName` | 的專案ID和主題ID配對 [!DNL PubSub] 您想要提供存取權的來源。 |
| `auth.params.subscriptionName` | 的專案ID和訂閱ID配對 [!DNL PubSub] 您想要提供存取權的來源。 |
| `connectionSpec.id` | 此 [!DNL PubSub] 連線規格ID： `70116022-a743-464a-bbfe-e226a7f8210c`. |

>[!ENDTABS]

**响应**

成功回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此基本連線ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 建立來源連線 {#source}

來源連線會建立和管理與擷取資料之外部來源的連線。 來源連線包含資料來源、資料格式等資訊，以及建立資料流所需的來源連線ID。 租使用者和組織專屬的來源連線例項。

POST若要建立來源連線，請向 `/sourceConnections` 的端點 [!DNL Flow Service] API。

**API格式**

```http
POST /sourceConnections
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Google PubSub source connection",
      "description": "A source connection for Google PubSub",
      "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
      "connectionSpec": {
          "id": "70116022-a743-464a-bbfe-e226a7f8210c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
          "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}",
          "dataType": "raw"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 來源連線的名稱。 確保來源連線的名稱是描述性的，因為您可以使用此名稱來查閱來源連線的資訊。 |
| `description` | 您可以提供的選用值，包含來源連線的更多資訊。 |
| `baseConnectionId` | 您的的基本連線ID [!DNL PubSub] 上一步驟中產生的來源。 |
| `connectionSpec.id` | 的固定連線規格ID [!DNL PubSub]. 此ID為： `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | 的格式 [!DNL PubSub] 您要擷取的資料。 目前唯一支援的資料格式為 `json`. |
| `params.topicName` | 您的名稱 [!DNL PubSub] 主題。 在 [!DNL PubSub]，主題是代表訊息摘要的已命名資源。 |
| `params.subscriptionName` | 與指定主題對應的訂閱名稱。 在 [!DNL PubSub]，訂閱可讓您從主題讀取訊息。 可以將一個或多個訂閱指派給單一主題。 |
| `params.dataType` | 此引數會定義所擷取的資料型別。 支援的資料型別包括： `raw` 和 `xdm`. |

**响应**

成功的回應會傳回唯一識別碼(`id`)。 在下個教學課程中，需要此ID才能建立資料流。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL PubSub] 來源連線使用 [!DNL Flow Service] API。 您可以在下一個教學課程中使用此來源連線ID來 [使用建立串流資料流 [!DNL Flow Service] API](../../collect/streaming.md).
