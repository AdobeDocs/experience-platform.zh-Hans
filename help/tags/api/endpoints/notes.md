---
title: Notes端点
description: 了解如何在Reactor API中调用/notes端点。
exl-id: fa3bebc0-215e-4515-87b9-d195c9ab76c1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 7%

---

# Notes端点

在Reactor API中，注释是可添加到某些资源的文本批注。 注释主要是对各自资源的评论。 注释的内容对资源行为没有影响，可用于包括以下内容在内的各种用例：

* 提供背景信息
* 作为待办事项列表
* 传递资源使用建议
* 向其他团队成员提供说明
* 记录历史上下文

的 `/notes` reactor API中的端点允许您以编程方式管理这些注释。

注释可应用以下资源：

* [数据元素](./data-elements.md)
* [扩展](./extensions.md)
* [库](./libraries.md)
* [属性](./properties.md)
* [规则组件](./rule-components.md)
* [规则](./rules.md)
* [秘密](./secrets.md)

这六种类型统称为“显着”资源。 删除显着资源时，也会删除其关联的注释。

>[!NOTE]
>
>对于可具有多个修订的资源，必须在当前（标题）修订版上创建任何注释。 它们不得附加到其他修订版本。
>
>但是，注释仍可从修订中读取。 在这种情况下，API仅返回在创建修订之前存在的注释。 它们提供了与剪切修订版本时一样的注释快照。 相反，从当前（头）修订版中读取注释会返回其所有注释。

## 快速入门

本指南中使用的端点是 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/). 在继续之前，请查看 [入门指南](../getting-started.md) 以了解有关如何对API进行身份验证的重要信息。

## 检索注释列表 {#list}

您可以通过附加来检索资源的注释列表 `/notes` 到相关资源的GET请求的路径。

**API格式**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| 参数 | 描述 |
| --- | --- |
| `RESOURCE_TYPE` | 您为获取注释的资源类型。 必须是以下值之一： <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | 的 `id` 要列出其注释的特定资源。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求列出了附加到库的注释。

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应会返回附加到指定资源的注释列表。

```json
{
  "data": [
    {
      "id": "NTa40de8d76bfd4e40835830900ce83b7b",
      "type": "notes",
      "attributes": {
        "author_display_name": "John Smith",
        "author_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:51:00.411Z",
        "text": "this is a note on a library"
      },
      "relationships": {
        "resource": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d"
          },
          "data": {
            "id": "LBcffea1a38c52408cae2398868625a12d",
            "type": "libraries"
          }
        }
      },
      "links": {
        "resource": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d",
        "self": "https://reactor.adobe.io/notes/NTa40de8d76bfd4e40835830900ce83b7b"
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

## 查找备注 {#lookup}

您可以在GET请求的路径中提供注释ID，以查找注释。

**API格式**

```http
GET /notes/{NOTE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `NOTE_ID` | 的 `id` 你想查的便笺。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**响应**

成功的响应会返回注释的详细信息。

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "this is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```

## 创建注释 {#create}

>[!WARNING]
>
>在创建新注释之前，请记住，注释不可编辑，删除注释的唯一方法是删除其相应的资源。

您可以通过附加 `/notes` 到相关资源的POST请求的路径。

**API格式**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| 参数 | 描述 |
| --- | --- |
| `RESOURCE_TYPE` | 要为其创建注释的资源类型。 必须是以下值之一： <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | 的 `id` 要为其创建注释的特定资源。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求会为资产创建新注释。

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "type": "notes",
          "attributes": {
            "text": "this is a note on a property"
          }
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `type` | **（必需）** 要更新的资源类型。 对于此端点，值必须为 `notes`. |
| `attributes.text` | **（必需）** 包含注释的文本。 每个注释限制为512个Unicode字符。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回新创建注释的详细信息。

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "This is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```
