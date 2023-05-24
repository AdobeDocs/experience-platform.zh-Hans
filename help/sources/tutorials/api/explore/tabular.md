---
keywords: Experience Platform；首頁；熱門主題；來源；API；探索；流程服務
title: 使用Flow Service API探索表格來源
description: 本教學課程使用流量服務API來探索表格來源的內容和結構。
exl-id: 0c7a5b8a-2071-4ac2-b2d1-c5534e7c7d9c
source-git-commit: 3bdeec8284873b8d9368f833b24e9922ed489019
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 2%

---

# 探索資料表，使用 [!DNL Flow Service] API

本教學課程提供的步驟說明如何使用 [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API。

>[!NOTE]
>
> 為了探索您的資料表，您必須擁有表格來源的有效基本連線ID。 如果您沒有此ID，請參閱下列教學課程，以瞭解如何為表格來源建立基本連線ID的步驟： <ul><li>[Advertising](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[客戶成功](../../../home.md#customer-success)</li><li>[数据库](../../../home.md#database)</li><li>[電子商務](../../../home.md#ecommerce)</li><li>[行銷自動化](../../../home.md#marketing-automation)</li><li>[付款](../../../home.md#payments)</li><li>[通訊協定](../../../home.md#protocols)</li></ul>

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../landing/api-guide.md).

## 探索您的資料表格

您可以透過向以下網站發出GET請求，擷取有關資料表格結構的資訊： [!DNL Flow Service] API，同時提供來源的基本連線ID。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 來源的基本連線ID。 |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會從您的來源傳回資料表陣列。 找到您要帶入Platform的表格並記下該表格 `path` 屬性，因為您必須在下一個步驟中提供它以檢查其結構。

```json
[
    {
        "type": "table",
        "name": "ACME Spring Campaign",
        "path": "acmeSpringCampaign",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "ACME Summer Campaign",
        "path": "acmeSummerCampaign",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect表格的結構

GET若要檢查資料表的內容，請對 [!DNL Flow Service] 將表格的路徑指定為查詢引數時的API。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 來源的基本連線ID。 |
| `{TABLE_PATH}` | 您要檢查的資料表的path屬性。 |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=table&object=acmeSpringCampaign' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回指定表格內容和結構的相關資訊。 有關每個表格欄的詳細資訊位於 `columns` 陣列。

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "TestID",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Name",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "complaint_type",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "complaint_description",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status_change_date",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "city",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield2",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  }
}
```

## 后续步骤

依照本教學課程，您已收集有關資料表結構和內容的資訊。 此外，您已擷取要擷取至Platform的表格路徑。 您可以使用此資訊來建立來源連線和資料流，以將您的資料匯入Platform。 如需有關如何使用建立來源連線和資料流的特定步驟，請參閱下列教學課程 [!DNL Flow Service] API：

* [廣告來源](../collect/advertising.md)
* [CRM來源](../collect/crm.md)
* [客戶成功來源](../collect/customer-success.md)
* [資料庫來源](../collect/database-nosql.md)
* [電子商務來源](../collect/ecommerce.md)
* [行銷自動化來源](../collect/marketing-automation.md)
* [付款來源](../collect/payments.md)
* [通訊協定來源](../collect/protocols.md)
