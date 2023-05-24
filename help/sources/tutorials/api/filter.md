---
keywords: Experience Platform；首頁；熱門主題；流程服務；流程服務API；來源；來源
title: 使用Flow Service API篩選來源的列層級資料
description: 本教學課程涵蓋如何使用Flow Service API在來源層級篩選資料的步驟
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: 963fc5e31e1728a8a1a7e94bc0cc47d010347325
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 2%

---

# 使用「 」篩選來源的列層級資料 [!DNL Flow Service] API

>[!IMPORTANT]
>
>篩選列層級資料的支援目前僅適用於下列來源：
>
>* [Google BigQuery](../../connectors/databases/bigquery.md)
>* [Salesforce](../../connectors/crm/salesforce.md)
>* [Snowflake](../../connectors/databases/snowflake.md)


本教學課程提供如何使用來篩選來源的列層級資料的步驟。 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本教學課程需要您實際瞭解Adobe Experience Platform的下列元件：

* [來源](../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../landing/api-guide.md).

## 篩選來源資料

以下概述篩選來源之列層級資料時應採取的步驟。

### 查詢連線規格

在使用API來篩選來源的列層級資料之前，您必須先擷取來源的連線規格詳細資料，以判斷特定來源支援的運運算元和語言。

GET若要擷取指定來源的連線規格，請向 `/connectionSpecs` 的端點 [!DNL Flow Service] API時輸入來源的屬性名稱，作為查詢引數的一部分。

**API格式**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMS}` | 篩選結果的選用查詢引數。 您可以擷取 [!DNL Google BigQuery] 透過套用 `name` 屬性和指定 `"google-big-query"` 以取得搜尋結果。 |

**请求**

下列要求會擷取下列專案的連線規格： [!DNL Google BigQuery].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回的連線規格 [!DNL Google BigQuery]，包括其支援的查詢語言和邏輯運運算元的資訊。

>[!NOTE]
>
>以下API回應會因簡短原因而截斷。

```json
"attributes": {
  "filterAtSource": {
    "enabled": true,
    "queryLanguage": "SQL",
    "logicalOperators": [
      "and",
      "or",
      "not"
    ],
    "comparisonOperators": [
      "=",
      "!=",
      "<",
      "<=",
      ">",
      ">=",
      "like",
      "in"
    ],
    "columnNameEscapeChar": "`",
    "valueEscapeChar": "'"
  }
```

| 属性 | 描述 |
| --- | --- |
| `attributes.filterAtSource.enabled` | 決定查詢的來源是否支援篩選列層級資料。 |
| `attributes.filterAtSource.queryLanguage` | 決定查詢來源支援的查詢語言。 |
| `attributes.filterAtSource.logicalOperators` | 決定可用來篩選來源之列層級資料的邏輯運運算元。 |
| `attributes.filterAtSource.comparisonOperators` | 決定可用來篩選來源之列層級資料的比較運運算元。 請參閱下表以瞭解比較運運算元的詳細資訊。 |
| `attributes.filterAtSource.columnNameEscapeChar` | 決定用於逸出欄的字元。 |
| `attributes.filterAtSource.valueEscapeChar` | 決定寫入SQL查詢時如何包圍值。 |

{style="table-layout:auto"}

#### 比较运算符

| 操作员 | 描述 |
| --- | --- |
| `==` | 依據屬性是否等於提供的值來篩選。 |
| `!=` | 依據屬性是否不等於提供的值來篩選。 |
| `<` | 依據屬性是否小於提供的值來篩選。 |
| `>` | 依據屬性是否大於提供的值來篩選。 |
| `<=` | 依據屬性是否小於或等於提供的值來篩選。 |
| `>=` | 依據屬性是否大於或等於提供的值來篩選。 |
| `like` | 在中使用的篩選器 `WHERE` 子句以搜尋指定的模式。 |
| `in` | 依據屬性是否在指定範圍內進行篩選。 |

{style="table-layout:auto"}

### 指定擷取的篩選條件

在識別來源支援的邏輯運運算元和查詢語言之後，您可以使用設定檔查詢語言(PQL)來指定您要套用至來源資料的篩選條件。

在下列範例中，條件僅會套用至選取與引數中所列節點型別所提供值相等的資料。

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "=",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "city"
      },
      {
        "nodeType": "literal",
        "value": "DDN"
      }
    ]
  }
}
```

### 預覽您的資料

您可以透過向以下發出GET請求來預覽資料： `/explore` 的端點 [!DNL Flow Service] API同時提供 `filters` 作為查詢引數的一部分，並在中指定PQL輸入條件 [!DNL Base64].

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 來源的基本連線ID。 |
| `{TABLE_PATH}` | 您要檢查的資料表的path屬性。 |
| `{FILTERS}` | 您的PQL篩選條件編碼於 [!DNL Base64]. |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的請求會傳回以下回應。

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "FIRSTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "LASTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "CITY",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "AGE",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "HEIGHT",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "ISEMPLOYED",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "POSTG",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "LATITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "LONGITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "JOINEDDATE",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDAT",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDATTS",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  },
 "data": [
    {
        "CITY": "MZN",
        "LASTNAME": "Jain",
        "JOINEDDATE": "2022-06-22T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-06-22T17:19:33",
        "FIRSTNAME": "Shivam",
        "POSTG": true,
        "HEIGHT": "169",
        "CREATEDATTS": "2022-06-22T17:19:33",
        "ISEMPLOYED": true,
        "LATITUDE": 2000.89,
        "AGE": "25"
    },
    {
        "CITY": "MUM",
        "LASTNAME": "Kreet",
        "JOINEDDATE": "2022-09-07T00:00:00",
        "LONGITUDE": 10500.01,
        "CREATEDAT": "2022-09-07T17:19:33",
        "FIRSTNAME": "Rakul",
        "POSTG": true,
        "HEIGHT": "155",
        "CREATEDATTS": "2022-09-07T17:19:33",
        "ISEMPLOYED": false,
        "LATITUDE": 2500.89,
        "AGE": "42"
    },
    {
        "CITY": "MAN",
        "LASTNAME": "Lee",
        "JOINEDDATE": "2022-09-14T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-09-14T05:02:33",
        "FIRSTNAME": "Denzel",
        "POSTG": true,
        "HEIGHT": "185",
        "CREATEDATTS": "2022-09-14T05:02:33",
        "ISEMPLOYED": true,
        "LATITUDE": 123.89,
        "AGE": "16"
    }
  ]
}
```

### 建立篩選資料的來源連線

若要建立來源連線並擷取經過篩選的資料，請向發出POST要求 `/sourceConnections` 端點時，將篩選條件提供為body引數的一部分。

**API格式**

```http
POST /sourceConnections
```

**请求**

以下請求會建立來源連線，以從中擷取資料 `test1.fasTestTable` 位置 `city` = `DDN`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "BigQuery Source Connection",
      "description": "Source Connection for Filter test",
      "baseConnectionId": "89d1459e-3cd0-4069-acb3-68f240db4eeb",
      "data": {
        "format": "tabular"
      },
      "params": {
        "tableName": "test1.fasTestTable",
        "filters": {
          "type": "PQL",
          "format": "pql/json",
          "value": {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "DDN"
              }
            ]
          }
        }
      },
      "connectionSpec": {
        "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
        "version": "1.0"
      }
    }'
```

**响应**

成功的回應會傳回唯一識別碼(`id`)。

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## 附录

本節提供不同裝載的更多範例以供篩選。

### 奇異條件

您可以省略初始值 `fnApply` 適用於只需要一個條件的案例。

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "like",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "firstname"
      },
      {
        "nodeType": "literal",
        "value": "%s"
      }
    ]
  }
}
```

### 使用 `in` 運運算元

如需運運算元的範例，請參閱下方的裝載範例 `in`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "in",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "firstname"
          },
          {
            "nodeType": "literal",
            "value": [
              "Ramen",
              "John"
            ]
          }
        ]
      }
    ]
  }
}
```

### 使用 `isNull` 運運算元

如需運運算元的範例，請參閱下方的裝載範例 `isNull`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "isNull",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "complaint_type"
      }
    ]
  }
}
```

### 使用 `NOT` 運運算元

如需運運算元的範例，請參閱下方的裝載範例 `NOT`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "NOT",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "isNull",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "complaint_type"
          }
        ]
      }
    ]
  }
}
```

### 具有巢狀條件的範例

如需複雜巢狀條件的範例，請參閱下列裝載範例。

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": ">=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 20
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "<=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 30
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "or",
        "params": [
          {
            "nodeType": "fnApply",
            "fnName": "!=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "PUD"
              }
            ]
          },
          {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "joinedDate"
              },
              {
                "nodeType": "literal",
                "value": "2020-04-22"
              }
            ]
          }
        ]
      }
    ]
  }
}
```
