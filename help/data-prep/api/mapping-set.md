---
keywords: Experience Platform；首頁；熱門主題；資料準備；api指南；對應集；
solution: Experience Platform
title: 對應集API端點
description: 您可以在Adobe Experience Platform API中使用「/mappingSets」端點，以程式設計方式擷取、建立、更新及驗證對應集。
exl-id: a4e4ddcd-164e-42aa-b7d1-ba59d70da142
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 3%

---

# 對應集端點

對應集可用來定義來源結構描述中的資料如何對應到目的地結構描述。 您可以使用 `/mappingSets` 資料準備API中的端點，以程式設計方式擷取、建立、更新和驗證對應集。

## 清單對應集

您可以透過向以下專案發出GET請求，擷取貴組織的所有對應集清單： `/mappingSets` 端點。

**API格式**

此 `/mappingSets` 端點支援數個查詢引數，以協助篩選結果。 雖然這些引數大部分是選用的，但強烈建議使用它們來協助減少昂貴的額外負荷。 不過，您必須同時包含 `start` 和 `limit` 請求中的引數。 可包含多個引數，以&amp;符號(`&`)。

```http
GET /mappingSets?limit={LIMIT}&start={START}
GET /mappingSets?limit={LIMIT}&start={START}&name={NAME}
GET /mappingSets?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
GET /mappingSets?limit={LIMIT}&start={START}&expandSchema={EXPAND_SCHEMA}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{LIMIT}` | (**必填**)指定傳回的對應集數目。 |
| `{START}` | (**必填**)指定結果頁面的位移。 若要取得結果的第一頁，請將值設為 `start=0`. |
| `{NAME}` | 依名稱篩選對應集。 |
| `{ORDER_BY}` | 排序結果的順序。 僅支援的欄位為 `createdDate` 和 `updatedDate`. 您可以在屬性前面加上 `+` 或 `-` 以分別依遞增或遞減順序排序。 |
| `{EXPAND_SCHEMA}` | 一個布林值，可決定是否將完整輸出結構描述作為回應的一部分傳回。 |

**请求**

以下請求將擷取組織內最後兩個對應集。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "data": [
        {
            "id": "428beb15b4864daaaa9dc3f005448005",
            "version": 1,
            "createdDate": 1582250953000,
            "modifiedDate": 1582251156000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_ui_platform",
            "supportVersion": "1.1",
            "inputSchema": {
                "id": "e660142cab8e438382abc5691b364b30",
                "version": 0,
                "sampleId": "f9e83882e3e34c1f8b873a3b8113c01e"
            },
            "outputSchema": {
                "id": "1956affc28be468aa452e5e47c680c6b",
                "version": 0,
                "schemaRef": {
                    "id": "https://ns.adobe.com/xdm/context/profile__union",
                    "contentType": "1.0"
                }
            },
            "mappings": [
                {
                    "id": "af809223484341009ce0db13d4b32a3a",
                    "version": 0,
                    "createdDate": 1582250953000,
                    "modifiedDate": 1582250953000,
                    "createdBy": "acp_xql_gateway",
                    "modifiedBy": "acp_xql_gateway",
                    "sourceType": "text/x.schema-path",
                    "source": "id",
                    "destination": "person.name.firstName",
                    "identity": false,
                    "primaryIdentity": false,
                    "matchScore": 0.0,
                    "functionVersion": 1,
                    "sourceAttribute": "id",
                    "destinationXdmPath": "person.name.firstName"
                }
            ],
            "status": "PUBLISHED",
            "strictMapping": false,
            "allowNullValues": false,
            "xdmVersion": "1.0",
            "schemaRef": {
                "id": "https://ns.adobe.com/xdm/context/profile__union",
                "contentType": "1.0"
            },
            "xdmSchema": "https://ns.adobe.com/xdm/context/profile__union"
        },
        {
            "id": "8afb1351833a4a4692ea61074b60813b",
            "version": 0,
            "createdDate": 1582250893000,
            "modifiedDate": 1582250893000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "supportVersion": "1.1",
            "inputSchema": {
                "id": "97fe2ecf4faa400bb66dd6be88a53fe4",
                "version": 0,
                "sampleId": "0248bfb352214f908bdd6cf9c19447e1"
            },
            "outputSchema": {
                "id": "e9c3696715d94905bb4e9bfc2c508e66",
                "version": 0,
                "schemaRef": {
                    "id": "https://ns.adobe.com/xdm/context/profile__union",
                    "contentType": "1.0"
                }
            },
            "mappings": [
                {
                    "id": "74647d8bf3b742f289534bee2fdeb732",
                    "version": 0,
                    "createdDate": 1582250893000,
                    "modifiedDate": 1582250893000,
                    "createdBy": "acp_xql_gateway",
                    "modifiedBy": "acp_xql_gateway",
                    "sourceType": "text/x.schema-path",
                    "source": "last_name",
                    "destination": "person.name.lastName",
                    "identity": false,
                    "primaryIdentity": false,
                    "matchScore": 0.0,
                    "functionVersion": 1,
                    "sourceAttribute": "last_name",
                    "destinationXdmPath": "person.name.lastName"
                }
            ],
            "status": "DRAFT",
            "strictMapping": false,
            "allowNullValues": false,
            "xdmVersion": "1.0",
            "schemaRef": {
                "id": "https://ns.adobe.com/xdm/context/profile__union",
                "contentType": "1.0"
            },
            "xdmSchema": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "_page": {
        "count": 0,
        "limit": 2
    }
}
```

## 建立對應集

您可以透過向以下專案發出POST請求來建立新的對應集： `/mappingSets` 端點。

**API格式**

```http
POST /mappingSets
```

**请求**

以下請求會建立新的對應集，由承載中提供的引數設定。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/mappingSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "lastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `outputSchema.schemaRef.id` | 您參考的XDM結構描述的ID。 |
| `outputSchema.schemaRef.contentType` | 決定參考之結構描述的回應格式。 有關此欄位的詳細資訊，請參閱 [Schema Registry開發人員指南](../../xdm/api/schemas.md#lookup). |
| `mappings.sourceType` | 來源型別說明如何將值從來源擷取至目的地。 來源型別支援兩種可能的值： <ul><li>`ATTRIBUTE`：來源型別 `ATTRIBUTE` 當輸入屬性來自來源結構描述時使用。</li><li>`EXPRESSION`：來源型別 `EXPRESSION` 使用計算欄位完成對應時使用。</li></ul> **警告**：錯誤設定來源型別值可能會使您的對應集無法編輯。 |
| `mappings.source` | 您希望資料從中對應的位置。 |
| `mappings.destination` | 您希望資料對應到的位置。 |

**响应**

成功的回應會傳回HTTP狀態200，其中包含您新建立對應集的相關資訊。

```json
{
    "id": "e7c80e4c0d8f4a98a7d400b4e178b635",
    "version": 0,
    "createdDate": 1614901254724,
    "modifiedDate": 1614901254724,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 驗證對應

您可以透過向以下發出POST請求，驗證您的對應是否正常運作： `/mappingSets/validate` 端點。

**API格式**

```http
POST /mappingSets/validate
```

**请求**

以下請求會驗證承載中提供的對應。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/mappingSets/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "lastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含建議對應的驗證資訊。

```json
{
    "validationResponse": [
        {
            "status": "SUCCESS",
            "errors": null
        },
        {
            "status": "SUCCESS",
            "errors": null
        },
        {
            "status": "SUCCESS",
            "errors": null
        }
    ]
}
```

## 預覽對應資料

您可以透過向以下專案發出POST請求，預覽您的資料將對應至的內容： `/mappingSets/preview` 端點。

**API格式**

```http
POST /mappingSets/preview
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/mappingSets/preview \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
{
    "data": [
        {
            "id": 1234,
            "firstName": "Jim",
            "lastName": "Seltzer"
        }
    ],
    "mappingSet": {
        "outputSchema": {
            "schemaRef": {
                "id": "https://ns.adobe.com/stardust/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "mappings": [
            {
                "sourceType": "ATTRIBUTE",
                "source": "id",
                "destination": "_id",
                "name": "id",
                "description": "Identifier field"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "firstName",
                "destination": "person.name.firstName"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "lastName",
                "destination": "person.name.lastName"
            }
        ]
    }
}'
```

**响应**

成功的回應會傳回HTTP狀態200，並預覽您的對應資料。

```json
[
    {
        "data": {
            "person": {
                "name": {
                    "firstName": "Jim",
                    "lastName": "Seltzer"
                }
            },
            "_id": "1234"
        },
        "errors": null
    }
]
```

## 查詢對應集

您可以在GET請求的路徑中提供其ID以擷取特定的對應集。 `/mappingSets` 端點。 此端點也支援數個查詢引數，以協助您擷取有關指定對應集版本的詳細資訊。

**API格式**

```http
GET /mappingSets/{MAPPING_SET_ID}
GET /mappingSets/{MAPPING_SET_ID}?expandSchema={EXPAND_SCHEMA}
GET /mappingSets/{MAPPING_SET_ID}?version={VERSION}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | (**必填**)您要擷取之對應集的ID。 |
| `{EXPAND_SCHEMA}` | 布林值查詢引數，可決定是否將輸出結構描述傳回為回應的一部分。 |
| `{VERSION}` | 整數查詢引數，可決定要擷取哪個版本的對應集。 |

**请求**

下列請求會擷取有關指定對應集的詳細資訊。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含您要擷取之對應集的詳細資訊。

>[!NOTE]
>
>下列回應已因空格而截斷。

```json
{
    "id": "e7c80e4c0d8f4a98a7d400b4e178b635",
    "version": 0,
    "createdDate": 1614901255000,
    "modifiedDate": 1614901255000,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "supportVersion": "1.1",
    "outputSchema": {
        "id": "cf0a57df22354cfdb5f32a747b63a456",
        "version": 0,
        "jsonSchema": {
            "title": "A sample schema",
            "description": "My sample schema",
            "type": "object",
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "description": "A unique identifier for the record.",
                    "type": "string"
                },
                "_repo": {
                    "type": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time"
                        }
                    }
                },
                "createdByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "modifiedByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "person": {
                    "type": "object",
                    "properties": {
                        "birthDate": {
                            "type": "string",
                            "format": "date"
                        },
                        "birthDayAndMonth": {
                            "type": "string",
                            "pattern": "[0-1][0-9]-[0-9][0-9]"
                        },
                        "birthYear": {
                            "type": "integer",
                            "minimum": 1,
                            "maximum": 32767
                        },
                        "gender": {
                            "type": "string",
                            "default": "not_specified",
                            "enum": [
                                "non_specific",
                                "not_specified",
                                "female",
                                "male"
                            ]
                        },
                        "name": {
                            "title": "Full name",
                            "description": "The person's full name.",
                            "type": "object",
                            "properties": {
                                "firstName": {
                                    "title": "First name",
                                    "type": "string"
                                },
                                "fullName": {
                                    "title": "Full name",
                                    "type": "string"
                                },
                                "lastName": {
                                    "title": "Last name",
                                    "type": "string"
                                },
                                "middleName": {
                                    "title": "Middle name",
                                    "type": "string"
                                }
                            }
                        }
                    }
                },
                "personID": {
                    "title": "Person ID",
                    "type": "string"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string"
                }
            },
            "version": "1.0",
            "imsOrg": "{ORG_ID}",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "id": "a11f44b0214d4fdcb79cbb5e1d93e638",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "id": "b9bf7873451f4b7ba767ca3ba9327750",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "firstName",
            "destination": "person.name.firstName",
        },
        {
            "id": "bab961fc18f54789b9268ec04c6f6f9b",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "lastName",
            "destination": "person.name.lastName",
        }
    ],
    "status": "DRAFT",
    "strictMapping": false,
    "allowNullValues": false,
    "xdmVersion": "application/vnd.adobe.xed-full+json;version=1",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
}
```

## 更新對應集

您可以在的路徑中提供對應集的ID，以更新對應集。 `PUT` 向以下專案提出的請求： `mappingSets` 端點。

**API格式**

```http
PUT /mappingSets/{MAPPING_SET_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | 您要更新的對應集ID。 |

**请求**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "id",
            "destination": "_id",
            "name": "id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "lastName",
            "destination": "person.name.lastName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "nationality",
            "destination": "person.nationality"           
        }
    ]
}
```

**响应**

成功回應會傳回HTTP狀態200，其中包含您新更新對應集的詳細資訊。

>[!NOTE]
>
>下列回應已因空格而截斷。

```json
{
    "id": "e7c80e4c0d8f4a98a7d400b4e178b635",
    "version": 1,
    "createdDate": 1614901255000,
    "modifiedDate": 1614909614227,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "supportVersion": "1.1",
    "outputSchema": {
        "id": "cf0a57df22354cfdb5f32a747b63a456",
        "version": 0,
        "jsonSchema": {
            "title": "A sample schema",
            "description": "My sample schema",
            "type": "object",
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "description": "A unique identifier for the record.",
                    "type": "string",
                },
                "_repo": {
                    "type": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time"
                        }
                    }
                },
                "createdByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "modifiedByBatchID": {
                    "type": "string",
                    "format": "uri-reference"
                },
                "person": {
                    "type": "object",
                    "properties": {
                        "birthDate": {
                            "type": "string",
                            "format": "date"
                        },
                        "birthDayAndMonth": {
                            "type": "string",
                            "pattern": "[0-1][0-9]-[0-9][0-9]"
                        },
                        "birthYear": {
                            "type": "integer",
                            "minimum": 1,
                            "maximum": 32767
                        },
                        "gender": {
                            "type": "string",
                            "default": "not_specified",
                            "enum": [
                                "non_specific",
                                "not_specified",
                                "female",
                                "male"
                            ]
                        },
                        "name": {
                            "title": "Full name",
                            "description": "The person's full name.",
                            "type": "object",
                            "properties": {
                                "firstName": {
                                    "title": "First name",
                                    "type": "string"
                                },
                                "fullName": {
                                    "title": "Full name",
                                    "type": "string"
                                },
                                "lastName": {
                                    "title": "Last name",
                                    "type": "string"
                                },
                                "middleName": {
                                    "title": "Middle name",
                                    "type": "string"
                                },
                                "suffix": {
                                    "title": "Suffix",
                                    "type": "string"
                                }
                            }
                        }
                },
                "personID": {
                    "title": "Person ID",
                    "type": "string"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string"
                }
            },
            "version": "1.0",
            "imsOrg": "6A29340459CA8D350A49413A@AdobeOrg",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "id": "1bb13ec5929f4847a8ea0f1d9e60d3e6",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "id",
            "destination": "_id",
            "name": "id"
        },
        {
            "id": "394bec970d54410b98e1d4c55a3843ca",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "firstName",
            "destination": "person.name.firstName"
        },
        {
            "id": "a78729629b22418998b528755b3e0fb1",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "lastName",
            "destination": "person.name.lastName"
        },
        {
            "id": "c5211e1e295f48018c125c24a04e925a",
            "version": 0,
            "sourceType": "text/x.schema-path",
            "source": "nationality",
            "destination": "person.nationality"
        }
    ],
    "strictMapping": false,
    "allowNullValues": false,
    "xdmVersion": "application/vnd.adobe.xed-full+json;version=1",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/89abc189258b1cb1a816d8f2b2341a6d98000ed8f4008305"
}
```

## 列出對應集的對應

您可以在GET要求的路徑中提供特定對應集的ID至下列端點，以檢視屬於該對應集的所有對應。

**API格式**

```http
GET /mappingSets/{MAPPING_SET_ID}/mappings
```

| 参数 | 描述 |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | 您要擷取對應的對應集ID。 |

**请求**

下列要求會傳回指定對應集中的所有對應。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635/mappings \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
[
    {
        "id": "1bb13ec5929f4847a8ea0f1d9e60d3e6",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "id",
        "destination": "_id",
        "name": "id",
        "description": "Identifier field",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "id",
        "destinationXdmPath": "_id"
    },
    {
        "id": "394bec970d54410b98e1d4c55a3843ca",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "firstName",
        "destination": "person.name.firstName",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "firstName",
        "destinationXdmPath": "person.name.firstName"
    },
    {
        "id": "a78729629b22418998b528755b3e0fb1",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "lastName",
        "destination": "person.name.lastName",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "lastName",
        "destinationXdmPath": "person.name.lastName"
    },
    {
        "id": "c5211e1e295f48018c125c24a04e925a",
        "version": 0,
        "createdDate": 1614909614000,
        "modifiedDate": 1614909614000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceType": "text/x.schema-path",
        "source": "nationality",
        "destination": "person.nationality",
        "identity": false,
        "primaryIdentity": false,
        "matchScore": 0.0,
        "functionVersion": 1,
        "sourceAttribute": "nationality",
        "destinationXdmPath": "person.nationality"
    }
]
```

## 查詢對應集內的對應

您可以在GET請求的路徑中提供其ID至下列端點，以擷取對應集的特定對應。

**API格式**

```http
GET /mappingSets/{MAPPING_SET_ID}/mappings/{MAPPING_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{MAPPING_SET_ID}` | 您要查閱對應資訊之對應集的ID。 |
| `{MAPPING_ID}` | 您要查閱的對應ID。 |

**请求**

下列請求會擷取指定對應集中特定對應的相關資訊。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/mappingSets/e7c80e4c0d8f4a98a7d400b4e178b635/mappings/394bec970d54410b98e1d4c55a3843ca \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含指定對應的詳細資訊。

```json
{
    "id": "394bec970d54410b98e1d4c55a3843ca",
    "version": 0,
    "createdDate": 1614909614000,
    "modifiedDate": 1614909614000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceType": "text/x.schema-path",
    "source": "firstName",
    "destination": "person.name.firstName",
    "identity": false,
    "primaryIdentity": false,
    "matchScore": 0.0,
    "functionVersion": 1,
    "sourceAttribute": "firstName",
    "destinationXdmPath": "person.name.firstName"
}
```
