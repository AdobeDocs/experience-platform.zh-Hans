---
title: 資料元素端點
description: 瞭解如何在Reactor API中呼叫/data_elements端點。
exl-id: ea346682-441b-415b-af06-094158eb7c71
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 4%

---

# 資料元素端點

資料元素的作用就像變數，指向應用程式內的重要資料片段。 資料元素會用於 [規則](./rules.md) 和 [擴充功能](./extensions.md) 設定。 當規則在執行階段在瀏覽器或應用程式中觸發時，將會解析資料元素的值並在規則中使用。 資料元素的功能與擴充功能設定相同。

將數個資料元素搭配使用會產生資料字典或資料對應。 此字典代表Adobe Experience Platform知道且能使用的資料。

資料元素只屬於一個 [屬性](./properties.md). 屬性可以有許多資料元素。

如需資料元素及其在標籤中使用的一般資訊，請參閱 [資料元素指南](../../ui/managing-resources/data-elements.md) UI檔案中。

## 快速入门

本指南中使用的端點是 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/). 在繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 有關如何向API驗證的重要資訊。

## 擷取資料元素清單 {#list}

您可以在GET要求的路徑中包含屬性的ID，以擷取屬性的資料元素清單。

**API格式**

```http
GET /properties/{PROPERTY_ID}/data_elements
```

| 参数 | 描述 |
| --- | --- |
| `PROPERTY_ID` | 此 `id` 擁有資料元素之屬性的ID。 |

{style="table-layout:auto"}

>[!NOTE]
>
>使用查詢引數，可根據下列屬性篩選列出的資料元素：<ul><li>`created_at`</li><li>`dirty`</li><li>`enabled`</li><li>`name`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li></ul>請參閱指南： [篩選回應](../guides/filtering.md) 以取得詳細資訊。

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

成功的回應會傳回指定屬性的資料元素清單。

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

## 查詢資料元素 {#lookup}

您可以在GET請求的路徑中提供其ID來查詢資料元素。

>[!NOTE]
>
>刪除資料元素時，會將其標籤為已刪除，但實際上並未從系統中移除。 因此，可以查詢已刪除的資料元素。 刪除的資料元素可由以下專案識別： `data.meta.deleted_at` 屬性。

**API格式**

```http
GET /data_elements/{DATA_ELEMENT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `DATA_ELEMENT_ID` | 此 `id` 要查閱的資料元素的URL名稱。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回資料元素的詳細資料。

```json
{
  "data": {
    "id": "DE8097636264104451ac3a18c95d5ff833",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:35:54.956Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "My Data Element 2020-12-14 17:35:54 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:35:54.956Z",
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
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/property"
        },
        "data": {
          "id": "PRa5621686159f44c880557e12af412a95",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/origin"
        },
        "data": {
          "id": "DE8097636264104451ac3a18c95d5ff833",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/extension"
        },
        "data": {
          "id": "EX085a465793b54be39b5408d13b50b46e",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833/updated_with_extension"
        },
        "data": {
          "id": "EXf9a32699efde42e9b9410b43bd660848",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRa5621686159f44c880557e12af412a95",
      "origin": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833",
      "self": "https://reactor.adobe.io/data_elements/DE8097636264104451ac3a18c95d5ff833",
      "extension": "https://reactor.adobe.io/extensions/EX085a465793b54be39b5408d13b50b46e"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 创建数据元素 {#create}

您可以發出POST要求，以建立新的資料元素。

**API格式**

```http
POST /properties/{PROPERTY_ID}/data_elements
```

| 参数 | 描述 |
| --- | --- |
| `PROPERTY_ID` | 此 `id` 的 [屬性](./properties.md) 您正在定義下方的資料元素。 |

{style="table-layout:auto"}

**请求**

下列要求會為指定的屬性建立新的資料元素。 此呼叫也會透過，將資料元素與現有擴充功能建立關聯， `relationships` 屬性。 請參閱指南： [關係](../guides/relationships.md) 以取得詳細資訊。

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "My Data Element 2020-12-14 17:33:21 +0000",
            "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
            "settings": "{\"elementSelector\":\".target-element\",\"elementProperty\":\"html\"}",
            "default_value": "general_label",
            "enabled": true,
            "force_lower_case": true,
            "clean_text": true,
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
                "type": "extensions"
              }
            }
          },
          "type": "data_elements"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `attributes.name` | **（必要）** 適用於資料元素的可讀取名稱。 |
| `attributes.delegate_descriptor_id` | **（必要）** 將資料元素與擴充功能套件建立關聯的格式化字串。 所有資料元素在首次建立時都必須與擴充功能套件建立關聯，因為每個擴充功能套件都會定義其委派資料元素的相容型別，以及其預期行為。 請參閱指南： [委派描述項ID](../guides/delegate-descriptor-ids.md) 以取得詳細資訊。 |
| `attributes.settings` | 以字串表示的設定JSON物件。 |
| `attributes.default_value` | 資料元素的評估結果為時傳回的預設值 `undefined`. |
| `attributes.enabled` | 表示資料元素是否已啟用的布林值。 |
| `attributes.force_lower_case` | 布林值，指出資料元素值在儲存前是否應轉換為小寫。 |
| `attributes.clean_text` | 布林值，指出是否應在儲存前從資料元素值移除開頭和結尾的空格。 |
| `type` | 正在更新的資源型別。 此端點的值必須為 `data_elements`. |

{style="table-layout:auto"}

**响应**

成功的回應會傳回新建立資料元素的詳細資料。

```json
{
  "data": {
    "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:33:21.774Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "My Data Element 2020-12-14 17:33:21 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:33:21.774Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/property"
        },
        "data": {
          "id": "PR05ad70a8078f44c1a229ecf0da2802f2",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/origin"
        },
        "data": {
          "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/extension"
        },
        "data": {
          "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension"
        },
        "data": {
          "id": "EXd6bf04b143e64fe0ae7efe55a6655fa9",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR05ad70a8078f44c1a229ecf0da2802f2",
      "origin": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "self": "https://reactor.adobe.io/data_elements/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "extension": "https://reactor.adobe.io/extensions/EX28788723a8e24a2f927fce1b55eb7ffc"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 更新資料元素 {#update}

您可以在PATCH請求的路徑中包含資料元素的ID來更新資料元素。

**API格式**

```http
PATCH /data_elements/{DATA_ELEMENT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `DATA_ELEMENT_ID` | 此 `id` 要更新的資料元素的ID。 |

{style="table-layout:auto"}

**请求**

以下請求會更新 `name` （針對現有資料元素）。

```shell
curl -X PATCH \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New Data Element Name"
          },
          "id": "DE3fab176ccf8641838b3da59f716fc42b",
          "type": "data_elements"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `attributes` | 物件，其屬性代表資料元素要更新的屬性。 所有資料元素屬性都可以更新。 請參閱的呼叫範例 [建立資料元素](#create) 以取得屬性及其使用案例的清單。 |
| `id` | 此 `id` 要更新的資料元素的ID。 這應該符合 `{DATA_ELEMENT_ID}` 請求路徑中提供的值。 |
| `type` | 正在更新的資源型別。 此端點的值必須為 `data_elements`. |

{style="table-layout:auto"}

**响应**

成功的回應會傳回已更新資料元素的詳細資料。

```json
{
  "data": {
    "id": "DE3fab176ccf8641838b3da59f716fc42b",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:36:24.552Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "New Data Element Name",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:36:25.578Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element-b\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/property"
        },
        "data": {
          "id": "PR85e261fb61ce44c9b2498807a6e6410b",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/origin"
        },
        "data": {
          "id": "DE3fab176ccf8641838b3da59f716fc42b",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/extension"
        },
        "data": {
          "id": "EX71f31a3eeec249dfb77fedd6c5ce6387",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension"
        },
        "data": {
          "id": "EX1f4df32a850c48a4930fb3e1dfa83536",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR85e261fb61ce44c9b2498807a6e6410b",
      "origin": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "self": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "extension": "https://reactor.adobe.io/extensions/EX71f31a3eeec249dfb77fedd6c5ce6387"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 修訂資料元素 {#revise}

當您修訂資料元素時，會以目前（標題）修訂版本建立資料元素的新修訂版本。 資料元素的每個修訂版本都有自己的ID。 可透過原始連結探索原始資料元素。

您可以透過提供下列專案來修訂資料元素 `meta.action` 屬性值為的屬性 `revise` 在PATCH要求內文中。

**API格式**

```http
PATCH /data_elements/{DATA_ELEMENT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `DATA_ELEMENT_ID` | 此 `id` 修改資料元素的URL名稱。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X PATCH \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New Data Element Name"
          },
          "meta": {
            "action": "revise"
          },
          "id": "DE7d7284657ee540ee8f402277860e9f8a",
          "type": "data_elements"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `attributes` | 物件，其屬性代表資料元素要更新的屬性。 所有資料元素屬性都可以更新。 請參閱的呼叫範例 [建立資料元素](#create) 以取得屬性及其使用案例的清單。 |
| `meta.action` | 當包含於值時 `revise`，此屬性會指出應為資料元素建立新的修訂版本。 |
| `id` | 此 `id` 修改資料元素的URL名稱。 這應該符合 `{DATA_ELEMENT_ID}` 請求路徑中提供的值。 |
| `type` | 正在修訂的資源型別。 此端點的值必須為 `data_elements`. |

{style="table-layout:auto"}

**响应**

成功回應會傳回資料元素新修訂版本的詳細資料，如增量所示 `meta.latest_revision_number` 屬性。

```json
{
  "data": {
    "id": "DE3fab176ccf8641838b3da59f716fc42b",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:36:24.552Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "New Data Element Name",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:36:25.578Z",
      "clean_text": false,
      "default_value": null,
      "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
      "force_lower_case": false,
      "review_status": "unsubmitted",
      "storage_duration": null,
      "settings": "{\"elementSelector\":\".target-element-b\",\"elementProperty\":\"html\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/property"
        },
        "data": {
          "id": "PR85e261fb61ce44c9b2498807a6e6410b",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/origin"
        },
        "data": {
          "id": "DE3fab176ccf8641838b3da59f716fc42b",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/extension"
        },
        "data": {
          "id": "EX71f31a3eeec249dfb77fedd6c5ce6387",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/updated_with_extension"
        },
        "data": {
          "id": "EX1f4df32a850c48a4930fb3e1dfa83536",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR85e261fb61ce44c9b2498807a6e6410b",
      "origin": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "self": "https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b",
      "extension": "https://reactor.adobe.io/extensions/EX71f31a3eeec249dfb77fedd6c5ce6387"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

## 刪除資料元素

您可以在DELETE請求的路徑中包含資料元素的ID來刪除資料元素。

**API格式**

```http
DELETE /data_elements/{DATA_ELEMENT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `DATA_ELEMENT_ID` | 此 `id` 資料元素的URL名稱。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功的回應會傳回HTTP狀態204 （無內容），且沒有回應內文，表示資料元素已刪除。

## 管理資料元素的附註 {#notes}

資料元素是「重要」資源，這表示您可以為每個個別資源建立和擷取文字型附註。 請參閱 [附註端點指南](./notes.md) 有關如何管理資料元素和其他相容資源的附註的詳細資訊。

## 擷取資料元素的相關資源 {#related}

下列呼叫示範如何擷取資料元素的相關資源。 時間 [查詢資料元素](#lookup)，這些關係會列在 `relationships` 屬性。

請參閱 [關係指南](../guides/relationships.md) 以取得有關Reactor API中關係的詳細資訊。

### 列出資料元素的相關程式庫 {#libraries}

您可以附加以列出使用資料元素的程式庫 `/libraries` 至查閱請求的路徑。

**API格式**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/libraries
```

| 参数 | 描述 |
| --- | --- |
| `{DATA_ELEMENT_ID}` | 此 `id` 要列出其程式庫的資料元素。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回使用指定資料元素的程式庫清單。

```json
{
  "data": [
    {
      "id": "LB62d20ad807a949e6b13b0a2c7299eb65",
      "type": "libraries",
      "attributes": {
        "created_at": "2020-12-14T17:50:19.589Z",
        "name": "My Library",
        "published_at": null,
        "state": "development",
        "updated_at": "2020-12-14T17:50:19.589Z",
        "build_required": true
      },
      "relationships": {
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/builds"
          }
        },
        "environment": {
          "links": {
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/environment"
          },
          "data": null
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/data_elements",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/extensions",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/notes"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/rules",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/rules"
          }
        },
        "upstream_library": {
          "data": null
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/property"
          },
          "data": {
            "id": "PR241ba9cd56324ac192de68d658f20cb0",
            "type": "properties"
          }
        },
        "last_build": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/last_build"
          },
          "data": null
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR241ba9cd56324ac192de68d658f20cb0",
        "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65"
      },
      "meta": {
        "build_status": null,
        "build_required_detail": "No build found since last state change"
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

### 列出資料元素的相關修訂版本 {#revisions}

您可以藉由附加，列出資料元素的先前修訂版本 `/revisions` 至查閱請求的路徑。

**API格式**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/revisions
```

| 参数 | 描述 |
| --- | --- |
| `{DATA_ELEMENT_ID}` | 此 `id` 要列出其修訂版本的資料元素。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/revisions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回指定資料元素的修訂清單。

```json
{
  "data": [
    {
      "id": "DEaeceb5164d494c768c18e37ec6f3b091",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:37:06.488Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:37:05 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:37:06.488Z",
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
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/property"
          },
          "data": {
            "id": "PR52072581500b44cd808e03e36c38e005",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/origin"
          },
          "data": {
            "id": "DE5172417ff56e43d2a99ca149021bf65a",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/extension"
          },
          "data": {
            "id": "EXdd53073348ef467683365286a33ade02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091/updated_with_extension"
          },
          "data": {
            "id": "EXf9d7d1ca8e6f436b900659ce499c09ce",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR52072581500b44cd808e03e36c38e005",
        "origin": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a",
        "self": "https://reactor.adobe.io/data_elements/DEaeceb5164d494c768c18e37ec6f3b091",
        "extension": "https://reactor.adobe.io/extensions/EXdd53073348ef467683365286a33ade02"
      },
      "meta": {
        "latest_revision_number": 1
      }
    },
    {
      "id": "DE5172417ff56e43d2a99ca149021bf65a",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:37:05.920Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:37:05 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:37:05.920Z",
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
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/property"
          },
          "data": {
            "id": "PR52072581500b44cd808e03e36c38e005",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/origin"
          },
          "data": {
            "id": "DE5172417ff56e43d2a99ca149021bf65a",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/extension"
          },
          "data": {
            "id": "EXdd53073348ef467683365286a33ade02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a/updated_with_extension"
          },
          "data": {
            "id": "EXf9d7d1ca8e6f436b900659ce499c09ce",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR52072581500b44cd808e03e36c38e005",
        "origin": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a",
        "self": "https://reactor.adobe.io/data_elements/DE5172417ff56e43d2a99ca149021bf65a",
        "extension": "https://reactor.adobe.io/extensions/EXdd53073348ef467683365286a33ade02"
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
      "total_count": 2
    }
  }
}
```

### 查詢資料元素的相關擴充功能 {#extension}

您可以藉由附加以查閱使用資料元素的擴充功能 `/extension` 到GET請求的路徑。

**API格式**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/extension
```

| 参数 | 描述 |
| --- | --- |
| `{DATA_ELEMENT_ID}` | 此 `id` 要查詢其副檔名的資料元素。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/extension \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回使用指定資料元素的擴充功能的詳細資料。

```json
{
  "data": {
    "id": "EX9c7f9f1e826149978f2dadaf4c639679",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:37:31.952Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:37:31.952Z",
      "delegate_descriptor_id": null,
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/property"
        },
        "data": {
          "id": "PR5c15543ef7bb403abc79d65fee0bf1f9",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/origin"
        },
        "data": {
          "id": "EX9c7f9f1e826149978f2dadaf4c639679",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR5c15543ef7bb403abc79d65fee0bf1f9",
      "origin": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679",
      "self": "https://reactor.adobe.io/extensions/EX9c7f9f1e826149978f2dadaf4c639679",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### 查詢資料元素的相關來源 {#origin}

您可以透過附加來查詢資料元素的來源 `/origin` 到GET請求的路徑。 資料元素的原點是建立目前修訂版本時所更新的先前修訂版本。

**API格式**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/origin
```

| 参数 | 描述 |
| --- | --- |
| `{DATA_ELEMENT_ID}` | 此 `id` 要查詢其來源的資料元素。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回指定資料元素來源的詳細資料。

```json
{
  "data": {
    "id": "DE790cb76f91594c2082a727b9f97024f6",
    "type": "data_elements",
    "attributes": {
      "created_at": "2020-12-14T17:37:19.891Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "My Data Element 2020-12-14 17:37:19 +0000",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:37:19.891Z",
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
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/property"
        },
        "data": {
          "id": "PRf1ac400fb1e04c689e28d5efcd675c94",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/origin"
        },
        "data": {
          "id": "DE790cb76f91594c2082a727b9f97024f6",
          "type": "data_elements"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/extension"
        },
        "data": {
          "id": "EX2345dba2c8b34d1cbe2795e29c62bf27",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6/updated_with_extension"
        },
        "data": {
          "id": "EXad7ebb72d721478483b741eebfffda6a",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRf1ac400fb1e04c689e28d5efcd675c94",
      "origin": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6",
      "self": "https://reactor.adobe.io/data_elements/DE790cb76f91594c2082a727b9f97024f6",
      "extension": "https://reactor.adobe.io/extensions/EX2345dba2c8b34d1cbe2795e29c62bf27"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### 查詢資料元素的相關屬性 {#property}

您可以透過附加來查詢擁有資料元素的屬性 `/property` 到GET請求的路徑。

**API格式**

```http
GET  /data_elements/{DATA_ELEMENT_ID}/property
```

| 参数 | 描述 |
| --- | --- |
| `{DATA_ELEMENT_ID}` | 此 `id` 要查詢其屬性的資料元素的ID。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/data_elements/DE3fab176ccf8641838b3da59f716fc42b/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的回應會傳回擁有指定資料元素之屬性的詳細資訊。

```json
{
  "data": {
    "id": "PRae9440b0f3234c4286569485f2b7a6a2",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:40.829Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:40.829Z",
      "platform": "web",
      "development": false,
      "token": "42daac072e1e",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/environments",
      "extensions": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/extensions",
      "rules": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2/rules",
      "self": "https://reactor.adobe.io/properties/PRae9440b0f3234c4286569485f2b7a6a2"
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
