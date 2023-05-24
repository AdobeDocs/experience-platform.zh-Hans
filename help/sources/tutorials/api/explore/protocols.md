---
keywords: Experience Platform；首頁；熱門主題；通訊協定
solution: Experience Platform
title: 使用流量服務API探索通訊協定系統
description: 本教學課程使用流量服務API來探索通訊協定應用程式。
exl-id: e4b24312-543e-4014-aa53-e8ca9c620950
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 2%

---

# 探索通訊協定系統，使用 [!DNL Flow Service] API

[!DNL Flow Service] 用於收集及集中Adobe Experience Platform內各種不同來源的客戶資料。 此服務提供可連線所有支援來源的使用者介面和RESTful API。

本教學課程使用 [!DNL Flow Service] 用於探索通訊協定應用程式的API。

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供您需要瞭解的其他資訊，以便使用成功連線到通訊協定應用程式 [!DNL Flow Service] API。

### 取得基礎連線

為了探索您的通訊協定系統，使用 [!DNL Platform] API，您必須擁有有效的基本連線ID。 如果您尚未建立要使用的通訊協定系統的基礎連線，您可以透過下列教學課程來建立基礎連線：

* [通用OData](../create/protocols/odata.md)

### 讀取範例API呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

* 授權：持有人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括屬於 [!DNL Flow Service]，會隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* Content-Type: `application/json`

## 探索您的資料表格

使用通訊協定應用程式的連線ID，您可以透過執行GET請求來探索資料表格。 使用以下呼叫來尋找您要檢查或擷取的表格路徑 [!DNL Platform].

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 通訊協定基礎連線的ID。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/a5c6b647-e784-4b58-86b6-47e784ab580b/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會從通訊協定應用程式傳回資料表陣列。 尋找您要加入的表格 [!DNL Platform] 並記下其 `path` 屬性，因為您必須在下一個步驟中提供它以檢查其結構。

```json
[
    {
        "type": "table",
        "name": "Categories",
        "path": "Categories",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "CustomerDemographics",
        "path": "CustomerDemographics",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Customers",
        "path": "Customers",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Orders",
        "path": "Orders",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect表格的結構

若要從通訊協定應用程式檢查表格的結構，請在將表格的路徑指定為查詢引數時執行GET要求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 通訊協定應用程式的連線ID。 |
| `{TABLE_PATH}` | 通訊協定應用程式中表格的路徑。 |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/a5c6b647-e784-4b58-86b6-47e784ab580b/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回指定資料表的結構。 有關每個表格欄的詳細資訊位於 `columns` 陣列。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "OrderID",
                "type": "integer",
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "CustomerID",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "EmployeeID",
                "type": "integer",
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "OrderDate",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
        ]
    }
}
```

## 后续步骤

依照本教學課程，您已探索您的通訊協定應用程式，找到您要擷取的表格路徑 [!DNL Platform]，並取得有關其結構的資訊。 您可以在下一個教學課程中使用此資訊來 [從您的通訊協定應用程式收集資料，並將其帶入Platform](../collect/protocols.md).
