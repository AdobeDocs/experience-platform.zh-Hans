---
title: CSV範本到結構描述轉換API端點
description: 結構描述登入API中的/rpc/csv2schema端點可讓您使用CSV範本自動建立Experience Data Model (XDM)結構描述。
exl-id: cf08774a-db94-4ea1-a22e-bb06385f8d0e
source-git-commit: b4c186c8c40d1372fb5011f49979523e1201fb0b
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 5%

---

# CSV範本到結構描述轉換API端點

此 `/rpc/csv2schema` 中的端點 [!DNL Schema Registry] API可讓您使用CSV檔案作為範本，自動建立Experience Data Model (XDM)結構描述。 使用此端點，您可以建立範本以大量匯入結構描述欄位，並減少手動API或UI工作。

## 快速入门

此 `/rpc/csv2schema` 端點是 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功呼叫任何Adobe Experience Platform API所需標題的重要資訊。

此 `/rpc/csv2schema` 端點是遠端程式呼叫(RPC)的一部分，受 [!DNL Schema Registry]. 不像 [!DNL Schema Registry] API、RPC端點不需要其他標頭，例如 `Accept` 或 `Content-Type`，且請勿使用 `CONTAINER_ID`. 相反地，他們必須使用 `/rpc` 名稱空間，如下方API呼叫所示。

## CSV檔案需求

若要使用此端點，您必須先建立包含適當欄標題和對應值的CSV檔案。 有些欄是必要欄位，其餘則是選用欄位。 下表說明這些欄及其在結構描述建構中的角色。

| CSV標頭位置 | CSV標頭名稱 | 必填/可选 | 描述 |
| --- | --- | --- | --- |
| 1 | `isIgnored` | 可选 | 包含時並設為 `true`，表示欄位尚未準備好進行API上傳，應予以忽略。 |
| 2 | `isCustom` | 必需 | 指出欄位是否為自訂欄位。 |
| 3 | `fieldGroupId` | 可选 | 自訂欄位應關聯的欄位群組ID。 |
| 4 | `fieldGroupName` | （請參閱說明） | 要與此欄位產生關聯的欄位群組名稱。<br><br>對於不擴充現有標準欄位的自訂欄位而言，這是選擇性的。 如果保留為空白，系統會自動指派名稱。<br><br>擴充標準欄位群組的標準欄位或自訂欄位必須要有，用於查詢 `fieldGroupId`. |
| 5 | `fieldPath` | 必需 | 欄位的完整XED點標籤法路徑。 包含標準欄位群組中的所有欄位（如下所指示）： `fieldGroupName`)，將值設為 `ALL`. |
| 6 | `displayName` | 可选 | 欄位的標題或易記顯示名稱。 也可以是標題的別名（如果存在）。 |
| 7 | `fieldDescription` | 可选 | 欄位的說明。 也可以是說明的別名（如果存在）。 |
| 8 | `dataType` | （請參閱說明） | 指示 [基本資料型別](../schema/field-constraints.md#basic-types) （欄位）。 所有自訂欄位都需要此引數。<br><br>若 `dataType` 設為 `object`，可以 `properties` 或 `$ref` 也需要為同一列定義，但不能同時定義。 |
| 9 | `isRequired` | 可选 | 指出資料擷取是否需要欄位。 |
| 10 | `isArray` | 可选 | 指示欄位是否為所指示的陣列 `dataType`. |
| 11 | `isIdentity` | 可选 | 指示欄位是否為身分欄位。 |
| 12 | `identityNamespace` | 在以下情況下需要 `isIdentity` 為true | 此 [身分名稱空間](../../identity-service/namespaces.md) 身分欄位的。 |
| 13 | `isPrimaryIdentity` | 可选 | 指出欄位是否為結構描述的主要身分。 |
| 14 | `minimum` | 可选 | （僅適用於數值欄位）欄位的最小值。 |
| 15 | `maximum` | 可选 | （僅適用於數值欄位）欄位的最大值。 |
| 16 | `enum` | 可选 | 欄位的列舉值清單，以陣列表示(例如： `[value1,value2,value3]`)。 |
| 17 | `stringPattern` | 可选 | （僅適用於字串欄位）字串值必須符合的Regex模式，才能在資料擷取期間通過驗證。 |
| 18 | `format` | 可选 | （僅適用於字串欄位）字串欄位的格式。 |
| 19 | `minLength` | 可选 | （僅適用於字串欄位）字串欄位的最小長度。 |
| 20 | `maxLength` | 可选 | （僅適用於字串欄位）字串欄位的最大長度。 |
| 21 | `properties` | （請參閱說明） | 在以下情況下需要 `dataType` 設為 `object` 和 `$ref` 未定義。 這會將物件內文定義為JSON字串(例如 `{"myField": {"type": "string"}}`)。 |
| 22 | `$ref` | （請參閱說明） | 在以下情況下需要 `dataType` 設為 `object` 和 `properties` 未定義。 這會定義 `$id` 物件型別的參照物件的ID (例如： `https://ns.adobe.com/xdm/context/person`)。 |
| 23 | `comment` | 可选 | 時間 `isIgnored` 設為 `true`，此欄用於提供結構描述的標題資訊。 |

{style="table-layout:auto"}

請參閱下列內容 [csv範本](../assets/sample-csv-template.csv) 以判斷應如何格式化您的CSV檔案。

## 從CSV檔案建立匯出裝載

設定CSV範本後，您可以將檔案傳送至 `/rpc/csv2schema` 端點並將其轉換為匯出裝載。

**API格式**

```http
POST /rpc/csv2schema
```

**请求**

請求承載必須使用表單資料作為其格式。 必要的表單欄位如下所示。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/csv2schema \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'csv-file=@"/Users/userName/Documents/sample-csv-template.csv"' \
  -F 'schema-class-id="https://ns.adobe.com/xdm/context/profile"' \
  -F 'schema-name="Example Schema"' \
  -F 'schema-description="Example schema description."'
```

| 属性 | 描述 |
| --- | --- |
| `csv-file` | 儲存在本機電腦上的CSV範本路徑。 |
| `schema-class-id` | 此 `$id` XDM的 [類別](../schema/composition.md#class) 此結構描述將採用的屬性。 |
| `schema-name` | 結構描述的顯示名稱。 |
| `schema-description` | 結構描述的說明。 |

**响应**

成功的回應會傳回從CSV檔案產生的匯出裝載。 裝載採用陣列的形式，而每個陣列專案都是一個物件，代表結構描述的相依XDM元件。 選取以下區段以檢視從CSV檔案產生的匯出裝載的完整範例。

+++ 範例回應裝載

```json
[
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "description": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "required": [
            "_ddgxdmint"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField1": {
                        "type": "string",
                        "title": "my custom field1",
                        "description": "Sample custom field1"
                    },
                    "customField2": {
                        "properties": {
                            "customerField22": {
                                "type": "string",
                                "title": "my custom field22",
                                "description": "Sample custom field22"
                            }
                        },
                        "type": "object",
                        "required": [
                            "customerField22"
                        ]
                    },
                    "customField3": {
                        "type": "number",
                        "title": "my custom field3",
                        "description": "Sample custom field3",
                        "minimum": 0,
                        "maximum": 10
                    },
                    "customField4": {
                        "type": "string",
                        "title": "my custom field4",
                        "description": "Sample custom field4",
                        "enum": [
                            "one",
                            "two",
                            "three"
                        ]
                    },
                    "customField5": {
                        "type": "array",
                        "title": "my custom field5",
                        "description": "Sample custom field5",
                        "items": {
                            "type": "string"
                        }
                    },
                    "customField6": {
                        "type": "string",
                        "title": "my custom field6",
                        "description": "Sample custom field6",
                        "format": "date"
                    }
                },
                "type": "object",
                "required": [
                    "customField1",
                    "customField2"
                ]
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "SampleFieldGroup",
        "description": "Generated field group 7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField7": {
                        "type": "object",
                        "title": "my custom field7",
                        "description": "Sample custom field7",
                        "properties": {
                            "myField": {
                                "type": "string"
                            }
                        }
                    },
                    "customField8": {
                        "type": "array",
                        "title": "my custom field8",
                        "description": "Sample custom field8",
                        "items": {
                            "type": "object",
                            "$ref": "https://ns.adobe.com/xdm/context/person"
                        }
                    }
                },
                "type": "object"
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Demographic Details:Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "description": "Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile-person-details"
        ],
        "allOf": [
            {
                "properties": {
                    "person": {
                        "properties": {
                            "name": {
                                "properties": {
                                    "_ddgxdmint": {
                                        "properties": {
                                            "nickName": {
                                                "type": "string"
                                            }
                                        },
                                        "type": "object",
                                        "required": [
                                            "nickName"
                                        ]
                                    }
                                },
                                "type": "object",
                                "required": [
                                    "_ddgxdmint"
                                ]
                            }
                        },
                        "type": "object",
                        "required": [
                            "name"
                        ]
                    }
                },
                "required": [
                    "person"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Loyalty Details:Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "description": "Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
        ],
        "allOf": [
            {
                "properties": {
                    "loyalty": {
                        "properties": {
                            "_ddgxdmint": {
                                "properties": {
                                    "joinDate": {
                                        "type": "string"
                                    }
                                },
                                "type": "object"
                            }
                        },
                        "type": "object"
                    }
                }
            },
            {
                "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "schemas",
        "title": "My Sample Schema",
        "description": "My Sample Schema",
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
                "meta:refProperty": [
                    "/person/name/firstName",
                    "/person/name/lastName",
                    "/person/name/_ddgxdmint/nickName"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241"
            }
        ]
    },
    {
        "@type": "xdm:alternateDisplayInfo",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/person/name/firstName",
        "xdm:title": {
            "en_us": "My first name"
        }
    },
    {
        "@type": "xdm:descriptorIdentity",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_ddgxdmint/customField1",
        "xdm:namespace": "email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": true
    }
]
```

+++

## 匯入結構描述裝載

從CSV檔案產生匯出裝載後，您可以將該裝載傳送至 `/rpc/import` 端點，以產生結構描述。

請參閱 [匯入端點指南](./import.md) 以取得有關如何從匯出裝載產生結構描述的詳細資訊。
