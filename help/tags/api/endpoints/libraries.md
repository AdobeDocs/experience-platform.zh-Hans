---
title: 库端点
description: 了解如何在Reactor API中调用/libraries端点。
exl-id: 0f7bc10f-2e03-43fa-993c-a2635f4d0c64
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1517'
ht-degree: 5%

---

# 库端点

库是表示[属性](./properties.md)所需行为的标记资源（[扩展](./extensions.md)、[规则](./rules.md)和[数据元素](./data-elements.md)）的集合。 Reactor API中的`/libraries`端点允许您以编程方式管理标记属性中的库。

库只属于一个属性。 资产可以具有多个库。

## 快速入门

本指南中使用的端点是[Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)的一部分。 在继续之前，请查看[快速入门指南](../getting-started.md)，以了解有关如何对API进行身份验证的重要信息。

在使用Reactor API中的库之前，请务必了解库状态和环境在决定您可以对特定库执行哪些操作方面扮演的角色。 有关详细信息，请参阅[库发布流](../../ui/publishing/publishing-flow.md)指南。

## 检索库列表 {#list}

您可以通过在GET请求的路径中包含资产的ID来检索资产的库列表。

**API格式**

```http
GET /properties/{PROPERTY_ID}/libraries
```

| 参数 | 描述 |
| --- | --- |
| `PROPERTY_ID` | 拥有库的属性的`id`。 |

{style="table-layout:auto"}

>[!NOTE]
>
>使用查询参数，可以根据以下属性过滤列出的库：<ul><li>`created_at`</li><li>`name`</li><li>`published_at`</li><li>`stale`</li><li>`state`</li><li>`updated_at`</li></ul>有关详细信息，请参阅[筛选响应](../guides/filtering.md)指南。

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR4bc17fb09ed845b1acfb0f6600a1f3c0/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应将返回指定属性的库列表。

```json
{
  "data": [
    {
      "id": "LBb174d60bdbd34f87a2e9466fadaacae0",
      "type": "libraries",
      "attributes": {
        "created_at": "2020-12-14T17:44:10.776Z",
        "name": "My Library",
        "published_at": null,
        "state": "development",
        "updated_at": "2020-12-14T17:44:10.776Z",
        "build_required": true
      },
      "relationships": {
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/builds"
          }
        },
        "environment": {
          "links": {
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/environment"
          },
          "data": null
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/data_elements",
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/extensions",
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/notes"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/rules",
            "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/relationships/rules"
          }
        },
        "upstream_library": {
          "data": null
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/property"
          },
          "data": {
            "id": "PR4bc17fb09ed845b1acfb0f6600a1f3c0",
            "type": "properties"
          }
        },
        "last_build": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0/last_build"
          },
          "data": null
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR4bc17fb09ed845b1acfb0f6600a1f3c0",
        "self": "https://reactor.adobe.io/libraries/LBb174d60bdbd34f87a2e9466fadaacae0"
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

## 查找库 {#lookup}

您可以通过在GET请求的路径中提供库的ID来查找库。

**API格式**

```http
GET /libraries/{LIBRARY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `LIBRARY_ID` | 要查找的库的`id`。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应将返回库的详细信息。

```json
{
  "data": {
    "id": "LB5862ee2dc21b4646a5536c8d6edb0c84",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:44:00.476Z",
      "name": "My Library",
      "published_at": null,
      "state": "development",
      "updated_at": "2020-12-14T17:44:00.476Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/builds"
        }
      },
      "environment": {
        "links": {
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/environment"
        },
        "data": null
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/extensions",
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/rules",
          "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/property"
        },
        "data": {
          "id": "PRc90084c615844db58201d4e70d47b8bf",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/last_build"
        },
        "data": null
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRc90084c615844db58201d4e70d47b8bf",
      "self": "https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```

## 创建库 {#create}

您可以通过发出POST请求来创建新库。

**API格式**

```http
POST /properties/{PROPERTY_ID}/libraries
```

| 参数 | 描述 |
| --- | --- |
| `PROPERTY_ID` | 您正在定义库的[属性](./properties.md)的`id`。 |

{style="table-layout:auto"}

**请求**

以下请求为指定属性创建新库。 首次创建库时，只能配置其`name`属性。 要将数据元素、扩展和规则添加到库，您必须创建关系。 有关详细信息，请参阅[管理库资源](#resources)一节。

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "My Library"
          },
          "type": "libraries"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `attributes.name` | **（必需）**&#x200B;易于用户识别的库名称。 |
| `type` | 正在更新的资源类型。 对于此终结点，值必须为`libraries`。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回新创建库的详细信息。

```json
{
  "data": {
    "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:33:21.774Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "My library 2020-12-14 17:33:21 +0000",
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
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/property"
        },
        "data": {
          "id": "PR05ad70a8078f44c1a229ecf0da2802f2",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/origin"
        },
        "data": {
          "id": "DE8667bc64ceba4b599e8458ea4ab58b8f",
          "type": "libraries"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/extension"
        },
        "data": {
          "id": "EX28788723a8e24a2f927fce1b55eb7ffc",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f/updated_with_extension"
        },
        "data": {
          "id": "EXd6bf04b143e64fe0ae7efe55a6655fa9",
          "type": "extensions"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR05ad70a8078f44c1a229ecf0da2802f2",
      "origin": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "self": "https://reactor.adobe.io/libraries/DE8667bc64ceba4b599e8458ea4ab58b8f",
      "extension": "https://reactor.adobe.io/extensions/EX28788723a8e24a2f927fce1b55eb7ffc"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 管理库的资源 {#resources}

与库关联的数据元素、扩展、规则和环境是通过关系建立的。 以下部分介绍了如何通过API调用管理这些关系。

### 将资源添加到库 {#add-resources}

您可以将`/relationships`附加到POST请求的路径中，然后附加资源类型，从而向库添加资源。

**API格式**

```http
POST /libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{LIBRARY_ID}` | 要将资源添加到的库的ID。 |
| `{RESOURCE_TYPE}` | 要添加到库的资源类型。 接受以下值： <ul><li>`data_elements`</li><li>`extensions`</li><li>`rules`</li></ul> |

{style="table-layout:auto"}

**请求**

以下请求向库中添加两个数据元素。

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": [
          {
            "id": "DEce7fdee2afe44efeb4d974247d1e8dbe",
            "type": "data_elements"
          },
          {
            "id": "DE8097636264104451ac3a18c95d5ff833",
            "type": "data_elements"
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `id` | 要添加到库的资源的ID。 |
| `type` | 要添加到库的资源类型。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回添加关系的详细信息。 对该库执行[查找请求](#lookup)会在`relationships`属性下显示添加的关系。

```json
{
  "data": [
    {
      "type": "data_elements",
      "id": "DEce7fdee2afe44efeb4d974247d1e8dbe"
    },
    {
      "id": "DE8097636264104451ac3a18c95d5ff833",
      "type": "data_elements"
    }
  ],
  "links": {
    "related": "https://reactor.adobe.io/libraries/LB09eca17e012842b49466506f419283a7/data_elements",
    "self": "https://reactor.adobe.io/libraries/LB09eca17e012842b49466506f419283a7/relationships/data_elements"
  }
}
```

### 替换库的资源 {#replace-resources}

您可以将`/relationships`附加到PATCH请求的路径中，后跟要替换的资源类型，以替换库的特定类型的所有现有资源。

**API格式**

```http
PATCH /libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{LIBRARY_ID}` | 要替换其关系的库的ID。 |
| `{RESOURCE_TYPE}` | 要替换的资源类型。 接受以下值： <ul><li>`data_elements`</li><li>`extensions`</li><li>`rules`</li></ul> |

{style="table-layout:auto"}

**请求**

以下请求将库的扩展替换为`data`数组中提供的扩展。

```shell
curl -X PATCH \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": [
          {
            "id": "EX58312732fd0f43f98037d765ef96c4cd",
            "type": "extensions"
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `id` | 要添加到库的资源的ID。 |
| `type` | 要添加到库的资源类型。 |

{style="table-layout:auto"}

**响应**

成功的响应会返回已更新关系的详细信息。 对该库执行[查找请求](#lookup)将显示`relationships`属性下的关系。

```json
{
  "data": [
    {
      "type": "extensions",
      "id": "EX58312732fd0f43f98037d765ef96c4cd"
    }
  ],
  "links": {
    "related": "https://reactor.adobe.io/libraries/LBdbc7c49ac8f040bc9576db26b127444d/extensions",
    "self": "https://reactor.adobe.io/libraries/LBdbc7c49ac8f040bc9576db26b127444d/relationships/extensions"
  }
}
```

### 删除库的资源 {#remove-resources}

您可以将`/relationships`附加到DELETE请求的路径中，后跟要删除的资源类型，以从库中移除现有资源。

**API格式**

```http
DELETE /libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{LIBRARY_ID}` | 要删除其资源的库的ID。 |
| `{RESOURCE_TYPE}` | 要移除的资源类型。 接受以下值： <ul><li>`data_elements`</li><li>`extensions`</li><li>`rules`</li></ul> |

{style="table-layout:auto"}

**请求**

以下请求从库中移除规则。 任何未包含在`data`数组中的现有规则都不会被删除。

```shell
curl -X DELETE \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": [
          {
            "id": "RLa16f7859c7404239940c2cf2ec02b03c",
            "type": "rules"
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `id` | 要从库中移除的资源的ID。 |
| `type` | 要从库中移除的资源类型。 |

{style="table-layout:auto"}

**响应**

成功的响应会返回资源类型已更新关系的详细信息。 如果此资源类型不存在任何关系，则将`data`属性作为空数组返回。 对该库执行[查找请求](#lookup)将显示`relationships`属性下的关系。

```json
{
  "data": [

  ],
  "links": {
    "related": "https://reactor.adobe.io/libraries/LBbde5759742844fe59458ca0c988ecd61/rules",
    "self": "https://reactor.adobe.io/libraries/LBbde5759742844fe59458ca0c988ecd61/relationships/rules"
  }
}
```

## 将库分配到环境 {#environment}

您可以将库分配给POST`/relationships/environment`环境，以将其分配给Environment请求的路径。

**API格式**

```http
POST /libraries/{LIBRARY_ID}/relationships/environment
```

| 参数 | 描述 |
| --- | --- |
| `{LIBRARY_ID}` | 要分配的库的ID。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "id": "EN867c480dc5ea4158be3ea68e5543bd85",
          "type": "environments"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `id` | 您为库分配的环境的ID。 |
| `type` | 必须设置为`environments`。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回关系的详细信息。 对该库执行[查找请求](#lookup)会在`relationships`属性下显示添加的关系。

```json
{
  "data": {
    "id": "EN867c480dc5ea4158be3ea68e5543bd85",
    "type": "environments"
  },
  "links": {
    "related": "https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/environment",
    "self": "https://reactor.adobe.io/libraries/LBdd2f55e9c3bb4ce0a582a0b0c586a6f5/relationships/environment"
  }
}
```

## 过渡库 {#transition}

通过在PATCH请求的路径中包含库的ID并在有效负载中提供相应的`meta.action`值，可以将库转换为其他发布状态。

**API格式**

```http
PATCH /libraries/{LIBRARY_ID}
```

| 参数 | 描述 |
| --- | --- |
| `LIBRARY_ID` | 要转换的库的`id`。 |

{style="table-layout:auto"}

**请求**

以下请求基于有效负载中提供的`meta.action`值转换现有库的状态。 库的可用操作取决于其当前发布状态，如[发布流](../../ui/publishing/publishing-flow.md#state)中所述。

```shell
curl -X PATCH \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "id": "LB80c337c956804738b2db2ea2f69fcdf0",
          "type": "libraries",
          "meta": {
            "action": "submit"
          }
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `meta.action` | 您希望对库执行的特定过渡操作。 根据库的当前发布状态，可以使用以下操作： <ul><li>`develop`</li><li>`submit`</li><li>`approve`</li><li>`reject`</li></ul> |
| `id` | 要更新的库的`id`。 这应当与在请求路径中提供的`{LIBRARY_ID}`值匹配。 |
| `type` | 正在更新的资源类型。 对于此终结点，值必须为`libraries`。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回已更新库的详细信息。

```json
{
  "data": {
    "id": "LB80c337c956804738b2db2ea2f69fcdf0",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:47:57.783Z",
      "name": "My Library",
      "published_at": null,
      "state": "submitted",
      "updated_at": "2020-12-14T17:48:06.431Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/builds"
        }
      },
      "environment": {
        "links": {
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/environment"
        },
        "data": null
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/extensions",
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/rules",
          "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/property"
        },
        "data": {
          "id": "PRbc84c93c1c9f48c9836ade5ea4199006",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/last_build"
        },
        "data": {
          "id": "BL8d6e931f2f6d48ea96d6730122f13bcc",
          "type": "builds"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRbc84c93c1c9f48c9836ade5ea4199006",
      "self": "https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```

## Publish a library {#publish}

>[!NOTE]
>
>只有已获批准的库才能发布到生产环境。

要将库发布到生产环境，请确保已向库添加了生产环境，然后创建内部版本。

**API格式**

```http
POST /libraries/{LIBRARY_ID}/builds
```

| 参数 | 描述 |
| --- | --- |
| `LIBRARY_ID` | 要发布的库的`id`。 |

{style="table-layout:auto"}

**请求**

此请求不需要有效负载。

```shell
curl -X POST \
  https://reactor.adobe.io/libraries/LB80c337c956804738b2db2ea2f69fcdf0/builds \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
```

**响应**

```json
{
  "data": {
    "id": "BL162b63703eb74c6bb3c12471e0062c05",
    "type": "builds",
    "attributes": {
      "created_at": "2020-12-14T17:48:18.731Z",
      "status": "pending",
      "updated_at": "2020-12-14T17:48:18.731Z",
      "token": "b223fc55df1c"
    },
    "relationships": {
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/rules"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/environment"
        },
        "data": {
          "id": "EN5428335fff304c749f06a241db137a60",
          "type": "environments"
        }
      },
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/library"
        },
        "data": {
          "id": "LBa937e62887e94d85b77cbe703f5dfc56",
          "type": "libraries"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05/property"
        },
        "data": {
          "id": "PR7e2b7aaaffcb499398010ba964603415",
          "type": "properties"
        }
      }
    },
    "links": {
      "environment": "https://reactor.adobe.io/environments/EN5428335fff304c749f06a241db137a60",
      "library": "https://reactor.adobe.io/libraries/LBa937e62887e94d85b77cbe703f5dfc56",
      "self": "https://reactor.adobe.io/builds/BL162b63703eb74c6bb3c12471e0062c05"
    },
    "meta": {
      "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/8b659dd115cf/launch-5986a1b644a4-development.min.js",
      "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/8b659dd115cf/b223fc55df1c/launch-5986a1b644a4-development.min.js",
      "archive": false,
      "host_type_of": "akamai"
    }
  }
}
```

## 管理库的注释 {#notes}

库是“重要”资源，这意味着您可以在每个资源中创建和检索基于文本的注释。 有关如何管理库和其他兼容资源的注释的更多信息，请参阅[注释端点指南](./notes.md)。

## 检索库的相关资源 {#related}

以下调用演示了如何检索库的相关资源。 在[查找库](#lookup)时，这些关系将列在`relationships`属性下。

有关Reactor API中关系的详细信息，请参阅[关系指南](../guides/relationships.md)。

### 列出库的相关数据元素 {#data-elements}

您可以将`/data_elements`附加到查找请求的路径中，以列出库所使用的数据元素。

**API格式**

```http
GET  /libraries/{LIBRARY_ID}/data_elements
```

| 参数 | 描述 |
| --- | --- |
| `{LIBRARY_ID}` | 要列出其数据元素的库的`id`。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/data_elements \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应将返回使用指定库的数据元素列表。

```json
{
  "data": [
    {
      "id": "DE4956628e8baa4b358cc592337049b37b",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:45:11.694Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "My Data Element 2020-12-14 17:45:10 +0000",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:45:11.694Z",
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
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/property"
          },
          "data": {
            "id": "PR245ca5e560784249b2a88ef82f2851b6",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/origin"
          },
          "data": {
            "id": "DE4c027939f2004fdcb15e3b4099e70974",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/extension"
          },
          "data": {
            "id": "EX5942ffd7fac94428875bd664e397bd47",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b/updated_with_extension"
          },
          "data": {
            "id": "EXbf411638b90843c486254b5ca0fe47d6",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR245ca5e560784249b2a88ef82f2851b6",
        "origin": "https://reactor.adobe.io/data_elements/DE4c027939f2004fdcb15e3b4099e70974",
        "self": "https://reactor.adobe.io/data_elements/DE4956628e8baa4b358cc592337049b37b",
        "extension": "https://reactor.adobe.io/extensions/EX5942ffd7fac94428875bd664e397bd47"
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

### 列出库的相关扩展 {#extensions}

您可以将`/extensions`附加到查找请求的路径中，以列出库所使用的扩展。

**API格式**

```http
GET  /libraries/{LIBRARY_ID}/extensions
```

| 参数 | 描述 |
| --- | --- |
| `{LIBRARY_ID}` | 要列出其扩展的库的`id`。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应将返回使用指定库的扩展列表。

```json
{
  "data": [
    {
      "id": "EXac1e55883e5b47eb9a3589b311960677",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:45:23.759Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:45:23.759Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/property"
          },
          "data": {
            "id": "PR2d1f3ba867204dc7a4c17614d23bbab0",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/origin"
          },
          "data": {
            "id": "EX63cf3b91ec8146889759bbacb15627c3",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR2d1f3ba867204dc7a4c17614d23bbab0",
        "origin": "https://reactor.adobe.io/extensions/EX63cf3b91ec8146889759bbacb15627c3",
        "self": "https://reactor.adobe.io/extensions/EXac1e55883e5b47eb9a3589b311960677",
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

### 列出库的相关规则 {#rules}

您可以将`/rules`附加到查找请求的路径中，以列出库使用的规则。

**API格式**

```http
GET  /libraries/{LIBRARY_ID}/rules
```

| 参数 | 描述 |
| --- | --- |
| `{LIBRARY_ID}` | 要列出其规则的库的`id`。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应将返回使用指定库的规则列表。

```json
{
  "data": [
    {
      "id": "RL460e550125054fffb824cce56c8cb1ac",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:45:36.405Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:45:36.405Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/property"
          },
          "data": {
            "id": "PRa68d0d2c6e0a4ae380fb30f17f7c435d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/origin"
          },
          "data": {
            "id": "RL04911614524d463a9c115bea442bce72",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRa68d0d2c6e0a4ae380fb30f17f7c435d",
        "origin": "https://reactor.adobe.io/rules/RL04911614524d463a9c115bea442bce72",
        "self": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac",
        "rule_components": "https://reactor.adobe.io/rules/RL460e550125054fffb824cce56c8cb1ac/rule_components"
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

### 查找库的相关环境 {#related-environment}

您可以通过将`/environment`附加到GET请求的路径来查找库已分配到的环境。

**API格式**

```http
GET  /libraries/{LIBRARY_ID}/environment
```

| 参数 | 描述 |
| --- | --- |
| `{LIBRARY_ID}` | 要查找其环境的库的`id`。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应将返回指定库所分配到的环境的详细信息。

```json
{
  "data": {
    "id": "ENe66122e6793641d8a8453f63c42e4270",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:39:12.484Z",
      "library_path": "f9fd106ab399/2df53b69e8a2",
      "library_name": "launch-1d2ffee7eef5-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-1d2ffee7eef5-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/2df53b69e8a2/launch-1d2ffee7eef5-development.min.js"
          ],
          "license_path": "f9fd106ab399/2df53b69e8a2/launch-1d2ffee7eef5-development.js"
        },
        {
          "library_name": "launch-1d2ffee7eef5-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/2df53b69e8a2/launch-1d2ffee7eef5-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:39:13.988Z",
      "status": "succeeded",
      "token": "1d2ffee7eef5"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/library"
        },
        "data": {
          "id": "LB52ccd7f1e99146999f90cb3bca4940a2",
          "type": "libraries"
        }
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/host",
          "self": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/relationships/host"
        },
        "data": {
          "id": "HT53a4ebcb177d431e8fd26929930de0af",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270/property"
        },
        "data": {
          "id": "PR79de7e0885a9451786f1bf4b9136a72c",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR79de7e0885a9451786f1bf4b9136a72c",
      "self": "https://reactor.adobe.io/environments/ENe66122e6793641d8a8453f63c42e4270"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

### 查找库的相关属性 {#property}

您可以通过将`/property`附加到GET请求的路径来查找拥有库的属性。

**API格式**

```http
GET  /libraries/{LIBRARY_ID}/property
```

| 参数 | 描述 |
| --- | --- |
| `{LIBRARY_ID}` | 您要查找其属性的库的`id`。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应将返回拥有指定库的属性的详细信息。

```json
{
  "data": {
    "id": "PRb18ac8f8b69d4f99af43870e91c17543",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:51:56.180Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:51:56.180Z",
      "platform": "web",
      "development": false,
      "token": "9d97006b0f9b",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/environments",
      "extensions": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/extensions",
      "rules": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543/rules",
      "self": "https://reactor.adobe.io/properties/PRb18ac8f8b69d4f99af43870e91c17543"
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

### 查找库的上游 {#upstream}

您可以通过将`/upstream_library`附加到GET请求的路径中，从库上游查找下一个库。

**API格式**

```http
GET  /libraries/{LIBRARY_ID}/upstream_library
```

| 参数 | 描述 |
| --- | --- |
| `{LIBRARY_ID}` | 要查找其上游库的库的`id`。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LB5862ee2dc21b4646a5536c8d6edb0c84/upstream_library \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功响应将返回上游库的详细信息。

```json
{
  "data": {
    "id": "LB29cc2f86b3684e00a10d196a60f4b0c0",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:49:32.459Z",
      "name": "My Library",
      "published_at": null,
      "state": "submitted",
      "updated_at": "2020-12-14T17:49:41.070Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/builds"
        }
      },
      "environment": {
        "links": {
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/environment"
        },
        "data": null
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/extensions",
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/rules",
          "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/property"
        },
        "data": {
          "id": "PR7c206ed399644222aef329488cee7fa7",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0/last_build"
        },
        "data": {
          "id": "BL87cde018ecd44ac7a20b0271ab06d04b",
          "type": "builds"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR7c206ed399644222aef329488cee7fa7",
      "self": "https://reactor.adobe.io/libraries/LB29cc2f86b3684e00a10d196a60f4b0c0"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```
