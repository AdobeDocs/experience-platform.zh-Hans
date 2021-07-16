---
title: 主机端点
description: 了解如何在Reactor API中对/hosts端点进行调用。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 7%

---

# 主机端点

>[!NOTE]
>
>本文档介绍如何管理Reactor API中的主机。 有关标记主机的更多常规信息，请参阅发布文档中[主机概述](../../ui/publishing/hosts/hosts-overview.md)的指南。

在Reactor API中，主机定义可以传送[build](./builds.md)的目标。

当Adobe Experience Platform中的标记用户请求生成库时，系统会检查库以确定应将库构建到的[environment](./environments.md)。 每个环境都与主机有关，指示交付内部版本的位置。

主机恰好属于一个[属性](./properties.md)，而一个属性可能拥有多个主机。 在发布之前，资产必须至少具有一个主机。

一个主机可由资产中的多个环境使用。 资产上通常有一个主机，并且该资产上的所有环境都使用同一台主机。

## 快速入门

本指南中使用的端点是[Reactor API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml)的一部分。 在继续操作之前，请查看[快速入门指南](../getting-started.md) ，以了解有关如何对API进行身份验证的重要信息。

## 检索主机列表 {#list}

您可以通过在GET请求的路径中包含属性的ID来检索属性的主机列表。

**API格式**

```http
GET /properties/{PROPERTY_ID}/hosts
```

| 参数 | 描述 |
| --- | --- |
| `PROPERTY_ID` | 拥有主机的属性的`id`。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>使用查询参数，可以根据以下属性筛选列出的主机：<ul><li>`created_at`</li><li>`name`</li><li>`type_of`</li><li>`updated_at`</li></ul>有关更多信息，请参阅[筛选响应](../guides/filtering.md)指南。

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应会返回指定属性的主机列表。

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

## 查找主机 {#lookup}

您可以通过在GET请求的路径中提供主机ID来查找主机。

**API格式**

```http
GET /hosts/{HOST_ID}
```

| 参数 | 描述 |
| --- | --- |
| `HOST_ID` | 要查找的主机的`id`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应会返回主机的详细信息。

```json
{
  "data": {
    "id": "HT5d90148e72224224aac9bc0b01498b84",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:25.353Z",
      "server": "https://server.example.com",
      "name": "Example Akamai Host",
      "path": "/akamai",
      "port": 8000,
      "status": "succeeded",
      "type_of": "akamai",
      "updated_at": "2020-12-14T17:42:25.353Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property"
        },
        "data": {
          "id": "PRd7cf174259f34057b5c435ef873a79bf",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRd7cf174259f34057b5c435ef873a79bf",
      "self": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84"
    }
  }
}
```

## 创建主机 {#create}

您可以通过发出POST请求来创建新主机。

**API格式**

```http
POST /properties/{PROPERTY_ID}/hosts
```

| 参数 | 描述 |
| --- | --- |
| `PROPERTY_ID` | 要在下定义主机的[属性](./properties.md)的`id`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求会为指定的属性创建新主机。 此调用还会通过`relationships`属性将主机与现有扩展关联。 有关更多信息，请参阅[relationships](../guides/relationships.md)指南。

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example SFTP Host",
            "type_of": "sftp",
            "username": "John Doe",
            "encrypted_private_key": "{PRIVATE_KEY}",
            "server": "https://example.com",
            "path": "assets",
            "port": 22
          },
          "type": "hosts"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `attributes.name` | **（必需）** 主机的人类可读名称。 |
| `attributes.type_of` | **（必需）** 主机的类型。可以是以下两个选项之一： <ul><li>`akamai` 对于 [Adobe管理的主机](../../ui/publishing/hosts/managed-by-adobe-host.md)</li><li>`sftp` (对于 [SFTP主机)](../../ui/publishing/hosts/sftp-host.md)</li></ul> |
| `attributes.encrypted_private_key` | 用于主机身份验证的可选私钥。 |
| `attributes.path` | 附加到`server` URL的路径。 |
| `attributes.port` | 一个整数，用于指示要使用的特定服务器端口。 |
| `attributes.server` | 服务器的主机URL。 |
| `attributes.username` | 用于身份验证的可选用户名。 |
| `type` | 要更新的资源类型。 对于此端点，值必须为`hosts`。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回新创建主机的详细信息。

```json
{
  "data": {
    "id": "HT69bfe634dead4a9a8c659f5d4d94cecd",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:07.033Z",
      "server": "//example.com",
      "name": "Example SFTP Host",
      "path": "assets",
      "port": 22,
      "status": "pending",
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:07.033Z",
      "username": "John Doe"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd/property"
        },
        "data": {
          "id": "PRb25a704c0b7c4562835ccdf96d3afd31",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31",
      "self": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd"
    }
  }
}
```

## 更新主机 {#update}

>[!NOTE]
>
>只能更新SFTP主机。

您可以通过在PATCH请求的路径中包含主机ID来更新主机。

**API格式**

```http
PATCH /hosts/{HOST_ID}
```

| 参数 | 描述 |
| --- | --- |
| `HOST_ID` | 要更新的主机的`id`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求会更新现有主机的`name`。

```shell
curl -X PUT \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New host Name"
          },
          "id": "HT5d90148e72224224aac9bc0b01498b84",
          "type": "hosts"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `attributes` | 一个对象，其属性表示要为主机更新的属性。 可以为主机更新以下属性： <ul><li>`encrypted_private_key`</li><li>`name`</li><li>`path`</li><li>`port`</li><li>`server`</li><li>`type_of`</li><li>`username`</li></ul> |
| `id` | 要更新的主机的`id`。 这应该与请求路径中提供的`{HOST_ID}`值匹配。 |
| `type` | 要更新的资源类型。 对于此端点，值必须为`hosts`。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回更新后的主机的详细信息。

```json
{
  "data": {
    "id": "HTb14e136a6fe147459b298a4645d2a6f5",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:45.087Z",
      "server": null,
      "name": "My SFTP host",
      "path": null,
      "port": null,
      "status": "succeeded",
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:45.696Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5/property"
        },
        "data": {
          "id": "PR8f240526f7b54a4dbd46965e79519fde",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR8f240526f7b54a4dbd46965e79519fde",
      "self": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5"
    }
  }
}
```

## 删除主机

您可以删除主机，方法是将其ID包含在DELETE请求的路径中。

**API格式**

```http
DELETE /hosts/{HOST_ID}
```

| 参数 | 描述 |
| --- | --- |
| `HOST_ID` | 要删除的主机的`id`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**响应**

成功的响应会返回没有响应正文的HTTP状态204（无内容），表示主机已被删除。

## 检索主机的相关资源 {#related}

以下调用演示了如何检索主机的相关资源。 当[查找主机](#lookup)时，这些关系将列在`relationships`属性下。

有关Reactor API中关系的更多信息，请参阅[关系指南](../guides/relationships.md)。

### 查找主机的相关属性 {#property}

您可以通过将`/property`附加到查找请求的路径来查找拥有主机的属性。

**API格式**

```http
GET /hosts/{HOST_ID}/property
```

| 参数 | 描述 |
| --- | --- |
| `{HOST_ID}` | 要查找其属性的主机的`id`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应会返回指定主机属性的详细信息。

```json
{
  "data": {
    "id": "PRbdfaffb7bf374b87be50e672f0cf9309",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:05.900Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:05.900Z",
      "platform": "web",
      "development": false,
      "token": "47d65c7c98db",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments",
      "extensions": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions",
      "rules": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules",
      "self": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309"
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
