---
title: 屬性端點
description: 瞭解如何在Reactor API中呼叫/properties端點。
exl-id: 7830c519-312f-4f73-b3f5-64ab0420d902
source-git-commit: e602f78470fe4eeb2a42e6333ba52096d8a9fe8a
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 6%

---

# 屬性端點

屬性是一種容器建構，可保留Reactor API中大部分的其他可用資源。 您可以使用以下程式設計方式管理屬性： `/properties` 端點。

在資源階層中，屬性是下列專案的擁有者：

* [内部版本](./builds.md)
* [回呼](./callbacks.md)
* [数据元素](./data-elements.md)
* [环境](./environments.md)
* [扩展](./extensions.md)
* [托管](./properties.md)
* [库](./libraries.md)
* [规则组件](./rule-components.md)
* [规则](./rules.md)

屬性只屬於一個 [公司](./companies.md). 公司可以有許多屬性。

如需有關屬性及其在Tag Management中角色的一般資訊，請參閱以下主題的概觀： [公司和屬性](../../ui/administration/companies-and-properties.md).

## 快速入门

本指南中使用的端點是 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/). 在繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 有關如何向API驗證的重要資訊。

## 擷取屬性清單 {#list}

您可以將公司ID包含在GET請求的路徑中，藉此擷取屬於公司的屬性清單。

**API格式**

```http
GET /companies/{COMPANY_ID}/properties
```

| 参数 | 描述 |
| --- | --- |
| `COMPANY_ID` | 此 `id` 擁有您要列出之屬性的公司名稱。 |

{style="table-layout:auto"}

>[!NOTE]
>
>使用查詢引數，可根據下列屬性篩選列出的屬性：<ul><li>`copying`</li><li>`created_at`</li><li>`enabled`</li><li>`name`</li><li>`platform`</li><li>`token`</li><li>`updated_at`</li></ul>請參閱指南： [篩選回應](../guides/filtering.md) 以取得詳細資訊。

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回指定公司的屬性清單。

```json
{
  "data": [
    {
      "id": "PR29e066628dcf4ba0a16780b2e339821c",
      "type": "properties",
      "attributes": {
        "created_at": "2020-12-14T17:51:28.215Z",
        "enabled": true,
        "name": "Kessel Example Property",
        "updated_at": "2020-12-14T17:51:28.215Z",
        "platform": "web",
        "development": false,
        "token": "30a138ca7f5b",
        "domains": [
          "example.com"
        ],
        "undefined_vars_return_empty": false,
        "rule_component_sequencing_enabled": false
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        },
        "callbacks": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/callbacks"
          }
        },
        "hosts": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/hosts"
          }
        },
        "environments": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/environments"
          }
        },
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/libraries"
          }
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/rules"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/notes"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "data_elements": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/data_elements",
        "environments": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/environments",
        "extensions": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/extensions",
        "rules": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c/rules",
        "self": "https://reactor.adobe.io/properties/PR29e066628dcf4ba0a16780b2e339821c"
      },
      "meta": {
        "rights": [
          "approve",
          "develop",
          "manage_environments",
          "manage_extensions",
          "publish"
        ]
      }
    },
    {
      "id": "PR0c559a62480142a7b9be4a118d1a0448",
      "type": "properties",
      "attributes": {
        "created_at": "2020-08-14T15:29:34.241Z",
        "enabled": true,
        "name": "new prop",
        "updated_at": "2020-08-14T15:29:34.241Z",
        "platform": "web",
        "development": true,
        "token": "b6cee01dedb7",
        "domains": [
          "google.com"
        ],
        "undefined_vars_return_empty": false,
        "rule_component_sequencing_enabled": false
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        },
        "callbacks": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/callbacks"
          }
        },
        "hosts": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/hosts"
          }
        },
        "environments": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/environments"
          }
        },
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/libraries"
          }
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/rules"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/notes"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "data_elements": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/data_elements",
        "environments": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/environments",
        "extensions": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/extensions",
        "rules": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448/rules",
        "self": "https://reactor.adobe.io/properties/PR0c559a62480142a7b9be4a118d1a0448"
      },
      "meta": {
        "rights": [
          "approve",
          "develop",
          "manage_environments",
          "manage_extensions",
          "publish"
        ]
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 2
    }
  }
}
```

## 查詢屬性 {#lookup}

您可以在GET請求的路徑中提供屬性ID以查詢屬性。

**API格式**

```http
GET /properties/{PROPERTY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `PROPERTY_ID` | 此 `id` ，屬於您要查閱的屬性。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回屬性的詳細資料。

```json
{
  "data": {
    "id": "PR48ade10e6acf4385ba96214e9f5d31e1",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:51:18.725Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:51:18.725Z",
      "platform": "web",
      "development": false,
      "token": "c54ba5e843e6",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/environments",
      "extensions": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/extensions",
      "rules": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1/rules",
      "self": "https://reactor.adobe.io/properties/PR48ade10e6acf4385ba96214e9f5d31e1"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```

## 创建资产 {#create}

您可以發出POST要求來建立新屬性。

**API格式**

```http
POST /company/{COMPANY_ID}/properties
```

| 参数 | 描述 |
| --- | --- |
| `COMPANY_ID` | 此 `id` ，位於您正在定義其屬性的公司底下。 |

{style="table-layout:auto"}

**请求**

下列要求會為指定的屬性建立新屬性。 此呼叫也會透過，將屬性與現有擴充功能建立關聯， `relationships` 屬性。 請參閱指南： [關係](../guides/relationships.md) 以取得詳細資訊。

```shell
curl -X POST \
  https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Example Property",
            "platform": "web"
            "domains": [
              "example.com"
            ],
            "privacy": "gdpr",
            "rule_component_sequencing_enabled": false,
            "ssl_enabled": false,
            "undefined_vars_return_empty": true
          },
          "type": "properties"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `attributes.name` | **（必要）** 可讀取的屬性名稱。 |
| `attributes.platform` | **（必要）** 屬性的平台。 可以是 `web` 針對Web屬性，或 `mobile` 或 `edge` 適用於行動屬性。 |
| `attributes.domains` | **（Web屬性的必要專案）** 屬性的URL網域陣列。 |
| `attributes.development` | 表示這是否為開發屬性的布林值。 |
| `attributes.privacy` | 字串；可用來參考屬性的隱私權相關考量事項。 |
| `attributes.rule_component_sequencing_enabled` | 此屬性的布林值表示是否應啟用規則元件排序。 |
| `attributes.ssl_enabled` | 此屬性的布林值表示是否應該啟用安全通訊端層(SSL)。 |
| `attributes.undefined_vars_return_empty` | 此屬性的布林值表示未定義的變數是否應傳回為空白。 |
| `type` | 正在更新的資源型別。 此端點的值必須為 `properties`. |

{style="table-layout:auto"}

**响应**

成功的回應會傳回新建立屬性的詳細資料。

```json
{
  "data": {
    "id": "PR505e39de0d0042d1b22321e7767edb4d",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:31:31.579Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:31:31.579Z",
      "platform": "web",
      "development": false,
      "token": "a969ffc6f872",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/environments",
      "extensions": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/extensions",
      "rules": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d/rules",
      "self": "https://reactor.adobe.io/properties/PR505e39de0d0042d1b22321e7767edb4d"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```

## 更新屬性 {#update}

您可以在PATCH請求的路徑中包含屬性的ID來更新屬性。

**API格式**

```http
PATCH /properties/{PROPERTY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `PROPERTY_ID` | 此 `id` 要更新的屬性。 |

{style="table-layout:auto"}

**请求**

以下請求會更新 `name` 和 `domains` 用於現有屬性。

```shell
curl -X PATCH \
  https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Property B",
            "domains": [
              "example.com"
            ]
          },
          "id": "PR541dbb24bad54dceb04710d7a9e7a740",
          "type": "properties"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `attributes` | 物件，其屬性代表要針對屬性更新的屬性。 可更新屬性的下列屬性： <ul><li>`development`</li><li>`domains`</li><li>`name`</li><li>`platform`</li><li>`privacy`</li><li>`rule_component_sequencing_enabled`</li><li>`ssl_enabled`</li><li>`undefined_vars_return_empty`</li></ul> |
| `id` | 此 `id` 要更新的屬性。 這應該符合 `{PROPERTY_ID}` 請求路徑中提供的值。 |
| `type` | 正在更新的資源型別。 此端點的值必須為 `properties`. |

{style="table-layout:auto"}

**响应**

成功的回應會傳回已更新屬性的詳細資料。

```json
{
  "data": {
    "id": "PR541dbb24bad54dceb04710d7a9e7a740",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:51:37.386Z",
      "enabled": true,
      "name": "Kessel Property B",
      "updated_at": "2020-12-14T17:51:43.062Z",
      "platform": "web",
      "development": false,
      "token": "3f2d8630a8d3",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/environments",
      "extensions": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/extensions",
      "rules": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740/rules",
      "self": "https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```

## 删除资产

您可以在DELETE請求的路徑中包含屬性ID來刪除屬性。

**API格式**

```http
DELETE /properties/{PROPERTY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `PROPERTY_ID` | 此 `id` 要刪除的屬性的ID。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/properties/PR541dbb24bad54dceb04710d7a9e7a740 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功的回應會傳回HTTP狀態204 （無內容），且沒有回應內文，這表示屬性已被刪除。

## 管理屬性的附註 {#notes}

屬性是「重要」資源，這表示您可以為每個個別資源建立和擷取文字型附註。 請參閱 [附註端點指南](./notes.md) 有關如何管理屬性和其他相容資源附註的詳細資訊。

## 擷取屬性的相關資源 {#related}

下列呼叫示範如何擷取屬性的相關資源。 時間 [查詢屬性](#lookup)，這些關係會列在 `relationships` 屬性。

請參閱 [關係指南](../guides/relationships.md) 以取得有關Reactor API中關係的詳細資訊。

### 列出屬性的相關回呼 {#callbacks}

您可以列出 [回呼](./callbacks.md) 透過附加以下內容在屬性上註冊的 `/callbacks` 至查閱請求的路徑。

**API格式**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 此 `id` 要列出其回呼的屬性。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回指定屬性擁有的回呼清單。

```json
{
  "data": [
    {
      "id": "CB26edef8d709243579589107bcda034da",
      "type": "callbacks",
      "attributes": {
        "created_at": "2020-12-14T17:34:47.082Z",
        "subscriptions": [
          "rule.created"
        ],
        "updated_at": "2020-12-14T17:34:47.082Z",
        "url": "https://www.example.com"
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da/property"
          },
          "data": {
            "id": "PR66a3356c73fc4aabb67ee22caae53d70",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70",
        "self": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### 列出屬性的相關資料元素 {#data-elements}

您可以列出 [資料元素](./data-elements.md) 透過附加屬性擁有的物件 `/data_elements` 至查閱請求的路徑。

**API格式**

```http
GET  /properties/{PROPERTY_ID}/data_elements
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 此 `id` 要列出其資料元素的屬性。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回指定屬性擁有的資料元素清單。

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:36:08 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:36:09.045Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 0
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### 列出屬性的相關環境 {#environments}

您可以列出 [環境](./environments.md) 透過附加屬性擁有的物件 `/environments` 至查閱請求的路徑。

**API格式**

```http
GET  /properties/{PROPERTY_ID}/environments
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 此 `id` 要列出其環境的屬性的。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR06c9196bc57048dd8ff169c27baeeca8/environments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回指定屬性所擁有的環境清單。

```json
{
  "data": [
    {
      "id": "ENbe322acb4fc64dfdb603254ffe98b5d3",
      "type": "environments",
      "attributes": {
        "archive": false,
        "created_at": "2020-12-14T17:38:51.047Z",
        "library_path": "f9fd106ab399/cb29d726b35e",
        "library_name": "launch-c0331746ae03-development.min.js",
        "library_entry_points": [
          {
            "library_name": "launch-c0331746ae03-development.min.js",
            "minified": true,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.min.js"
            ],
            "license_path": "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
          },
          {
            "library_name": "launch-c0331746ae03-development.js",
            "minified": false,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
            ]
          }
        ],
        "name": "Development Environment A",
        "path": "https://assets.adobedtm.com/staging",
        "stage": "development",
        "updated_at": "2020-12-14T17:38:51.047Z",
        "status": "succeeded",
        "token": "c0331746ae03"
      },
      "relationships": {
        "library": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/library"
          },
          "data": null
        },
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/builds"
          }
        },
        "host": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/host",
            "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/relationships/host"
          },
          "data": {
            "id": "HTc5cae9ce1e3943aab185bdba939f98bd",
            "type": "hosts"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/property"
          },
          "data": {
            "id": "PR06c9196bc57048dd8ff169c27baeeca8",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR06c9196bc57048dd8ff169c27baeeca8",
        "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3"
      },
      "meta": {
        "archive_encrypted": false
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### 列出屬性的相關副檔名 {#extensions}

您可以列出 [擴充功能](./extensions.md) 透過附加屬性擁有的物件 `/extensions` 至查閱請求的路徑。

**API格式**

```http
GET  /properties/{PROPERTY_ID}/extensions
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 此 `id` 要列出其副檔名的屬性。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回指定屬性擁有的擴充功能清單。

```json
{
  "data": [
    {
      "id": "EXd9d80c87afb6432ba823a58d3e78299b",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:40:21.000Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:40:21.000Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/property"
          },
          "data": {
            "id": "PRee071cb5b7794f42b74c913e1ad2e325",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/origin"
          },
          "data": {
            "id": "EXd9d80c87afb6432ba823a58d3e78299b",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325",
        "origin": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b",
        "self": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b",
        "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
        "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### 列出屬性的相關主機 {#hosts}

您可以列出 [主機](./hosts.md) 透過附加屬性來使用 `/hosts` 至查閱請求的路徑。

**API格式**

```http
GET  /properties/{PROPERTY_ID}/hosts
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 此 `id` 要列出其主機的屬性。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回指定屬性所使用的主機清單。

```json
{
  "data": [
    {
      "id": "HT405b8d9306004eb38106e66c8a4afc09",
      "type": "hosts",
      "attributes": {
        "created_at": "2020-12-14T17:42:35.239Z",
        "server": null,
        "name": "Example Akamai Host",
        "path": null,
        "port": null,
        "status": "succeeded",
        "type_of": "akamai",
        "updated_at": "2020-12-14T17:42:35.239Z",
        "username": null
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09/property"
          },
          "data": {
            "id": "PRd428c2a25caa4b32af61495f5809b737",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737",
        "self": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### 列出屬性的相關規則 {#rules}

您可以列出 [規則](./rules.md) 透過附加屬性來使用 `/rules` 至查閱請求的路徑。

**API格式**

```http
GET  /properties/{PROPERTY_ID}/rules
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 此 `id` 要列出其規則的屬性。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回指定屬性使用的規則清單。

```json
{
  "data": [
    {
      "id": "RL8429f3fee98b44c68f7a538e68e21747",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:56:44.109Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:56:44.109Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/property"
          },
          "data": {
            "id": "PR41f64d2a9d9b4862b0582c5ff6a07504",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/origin"
          },
          "data": {
            "id": "RL8429f3fee98b44c68f7a538e68e21747",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504",
        "origin": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "self": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "rule_components": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
      },
      "meta": {
        "latest_revision_number": 0
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### 查詢屬性的相關公司 {#company}

您可以透過附加來查詢擁有屬性的公司 `/company` 至查閱請求的路徑。

**API格式**

```http
GET /properties/{PROPERTY_ID}/company
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 此 `id` 要查詢其公司的屬性。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/HT5d90148e72224224aac9bc0b01498b84/company \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回指定屬性之公司的詳細資料。

```json
{
  "data": {
    "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
    "type": "companies",
    "attributes": {
      "created_at": "2020-08-13T17:13:30.711Z",
      "name": "Reactor QE",
      "org_id": "08364A825824E04F0A494115@AdobeOrg",
      "updated_at": "2020-08-13T17:13:30.711Z",
      "token": "f9fd106ab399",
      "cjm_enabled": true,
      "edge_enabled": false,
      "edge_events_allotment": null,
      "edge_fanout_ratio": null
    },
    "relationships": {
      "properties": {
        "links": {
          "related": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "properties": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1/properties"
    },
    "meta": {
      "rights": [
        "develop_extensions",
        "manage_properties",
        "manage_app_configurations"
      ],
      "platform_rights": {
        "web": [
          "develop_extensions",
          "manage_properties",
          "manage_app_configurations"
        ],
        "mobile": [
          "develop_extensions",
          "manage_properties",
          "manage_app_configurations"
        ]
      }
    }
  }
}
```
