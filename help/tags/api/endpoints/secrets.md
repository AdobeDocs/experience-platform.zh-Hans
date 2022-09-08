---
title: Secrets端点
description: 了解如何在Reactor API中对/secrets端点进行调用。
exl-id: 76875a28-5d13-402d-8543-24db7e2bee8e
source-git-commit: 24e79c14268b9eab0e8286eb8cd1352c1dfcd1b6
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 7%

---

# Secrets端点

密钥是仅存在于事件转发属性(具有 `platform` 属性设置为 `edge`)。 它们允许事件转发向另一个系统进行身份验证，以便进行安全数据交换。

本指南将向您展示如何调用 `/secrets` 端点。 有关不同密钥类型及其使用方法的详细说明，请参阅 [秘密](../guides/secrets.md) ，然后再返回本指南。

## 快速入门

本指南中使用的端点是 [Reactor API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). 在继续之前，请查看 [入门指南](../getting-started.md) 以了解有关如何对API进行身份验证的重要信息。

## 检索属性的密钥列表 {#list-property}

您可以通过发出GET请求来列出属于某个资产的密钥。

**API格式**

```http
GET /properties/{PROPERTY_ID}/secrets
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 要列出其机密的属性的ID。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRe005d921bb724bc88c3ff28e3e916f04/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**响应**

成功响应会返回属于该属性的机密列表。

```json
{
  "data": [
    {
      "id": "SE8bd20bd5d16b49ee9d925929e292526c",
      "type": "secrets",
      "attributes": {
        "created_at": "2021-07-16T22:29:29.777Z",
        "updated_at": "2021-07-16T22:29:29.777Z",
        "name": "Example Secret",
        "type_of": "token",
        "activated_at": null,
        "expires_at": null,
        "refresh_at": null,
        "status": "pending",
        "credentials": {
        }
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/property"
          },
          "data": {
            "id": "PRe005d921bb724bc88c3ff28e3e916f04",
            "type": "properties"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/environment"
          },
          "data": {
            "id": "EN80ad9efbf4ff4f15bebd770613378a75",
            "type": "environments"
          },
          "meta": {
            "stage": "development"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/notes"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c",
        "property": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/property"
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

## 检索环境的密钥列表 {#list-environment}

您可以通过发出GET请求来列出属于某个环境的密钥。

**API格式**

```http
GET /environments/{ENVIRONMENT_ID}/secrets
```

| 参数 | 描述 |
| --- | --- |
| `{ENVIRONMENT_ID}` | 要列出其机密的环境的ID。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/EN0a1b00749daf4ff48a34d2ec37286aa7/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**响应**

成功的响应会返回属于该环境的机密列表。

```json
{
  "data": [
    {
      "id": "SE57b5ea69acde4595825b85befd1675b3",
      "type": "secrets",
      "attributes": {
        "created_at": "2021-07-16T22:29:35.447Z",
        "updated_at": "2021-07-16T22:29:35.447Z",
        "name": "Example Secret",
        "type_of": "token",
        "activated_at": null,
        "expires_at": null,
        "refresh_at": null,
        "status": "pending",
        "credentials": {
        }
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/property"
          },
          "data": {
            "id": "PRb302ca3557334c13b130da719222ec97",
            "type": "properties"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/environment"
          },
          "data": {
            "id": "EN0a1b00749daf4ff48a34d2ec37286aa7",
            "type": "environments"
          },
          "meta": {
            "stage": "development"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/notes"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3",
        "property": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/property"
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

## 查个秘密 {#lookup}

您可以通过在GET请求的路径中包含密钥ID来查找密钥。

**API格式**

```http
GET /secrets/{SECRET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 要查找的密钥的ID。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**响应**

成功的响应会返回密钥的详细信息。

```json
{
  "data": {
    "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
    "type": "secrets",
    "attributes": {
      "created_at": "2021-07-16T22:29:41.135Z",
      "updated_at": "2021-07-16T22:29:41.135Z",
      "name": "Example Secret",
      "type_of": "token",
      "activated_at": null,
      "expires_at": null,
      "refresh_at": null,
      "status": "pending",
      "credentials": {
        }
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
        },
        "data": {
          "id": "PR19717d5acf114209a5aebd0f2b228438",
          "type": "properties"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment"
        },
        "data": {
          "id": "EN04d820606cc74d5eaf51616e8b50201a",
          "type": "environments"
        },
        "meta": {
          "stage": "development"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/notes"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3",
      "property": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
    }
  }
}
```

## 创建密钥 {#create}

您可以通过发出POST请求来创建密钥。

>[!NOTE]
>
>创建新密钥时，API会返回一个立即响应，其中包含该资源的信息。 同时，触发秘密交换任务以测试凭证交换是否正常工作。 此任务将异步处理，并将密钥的状态属性更新为 `succeeded` 或 `failed` 取决于结果。

**API格式**

```http
POST /properties/{PROPERTY_ID}/secrets
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 要在下定义密钥的属性的ID。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR9eff664dc6014217b76939bb78b83976/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example Secret",
            "type_of": "simple-http",
            "credentials": {
              "username": "example_username",
              "password": "pass12345"
            }
          },
          "relationships": {
            "environment": {
              "data": {
                "id": "EN04cdddbdb6574170bcac9f470f3b8087",
                "type": "environments"
              }
            }
          },
          "type": "secrets"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 密钥的唯一描述性名称。 |
| `type_of` | 密钥表示的身份验证凭据类型。 具有三个可接受的值：<ul><li>`token`:令牌字符串。</li><li>`simple-http`:用户名和密码。</li><li>`oauth2`:符合OAuth标准的凭据。</li></ul> |
| `credentials` | 包含密钥凭据值的对象。 根据 `type_of` 属性中，必须提供不同的属性。 请参阅 [凭据](../guides/secrets.md#credentials) 有关每种类型要求的详细信息，请参阅“机密指南”。 |
| `relationships.environment` | 首次创建环境时，必须将每个密钥与环境关联。 的 `data` 此属性中的对象必须包含 `id` 分配到的环境的密钥，以及 `type` 值 `environments`. |
| `type` | 要创建的资源类型。 对于此调用，值必须为 `secrets`. |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回密钥的详细信息。 请注意，根据密钥类型， `credentials` 可能是隐藏的。

```json
{
  "data": { 
    "id": "SE39fdf431f8ad4600bbc24ea73fcb1154", 
    "type": "secrets", 
    "attributes": { 
    "created_at": "2021-07-14T19:33:25.628Z", 
    "updated_at": "2021-07-14T19:33:25.628Z", 
    "name": "Example Secret", 
    "type_of": "simple-http", 
    "activated_at": null, 
    "expires_at": null, 
    "refresh_at": null, 
    "status": "pending", 
    "credentials": { 
      "username": "example_username" 
      } 
    }, 
    "relationships": { 
      "property": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
        }, 
        "data": { 
          "id": "PR9eff664dc6014217b76939bb78b83976", 
          "type": "properties" 
        } 
      }, 
      "environment": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/environment" 
        }, 
        "data": { 
          "id": "EN04cdddbdb6574170bcac9f470f3b8087", 
          "type": "environments" 
        }, 
        "meta": { 
          "stage": "development" 
        } 
      }, 
      "notes": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/notes" 
        } 
      } 
    }, 
    "links": { 
      "self": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154", 
      "property": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
    } 
  } 
}
```

## 测试 `oauth2` 秘密 {#test}

>[!NOTE]
>
>此操作只能对具有 `type_of` 值 `oauth2`.

您可以测试 `oauth2` 密钥，方法是将其ID包含在PATCH请求的路径中。 测试操作执行交换，并在 `test_exchange` 属性 `meta` 对象。 此操作不会更新密钥本身。

**API格式**

```http
PATCH /secrets/{SECRET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 的ID `oauth2` 要测试的秘密。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X PATCH \
  https://reactor.adobe.io/secrets/SE6c15a7a64f9041b5985558ed3e19a449 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "type_of": "oauth2"
          },
          "meta": {
            "action": "test"
          },
          "id": "SE6c15a7a64f9041b5985558ed3e19a449",
          "type": "secrets"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `attributes` | 必须包含 `type_of` 值为的属性 `oauth2`. |
| `meta` | 必须包含 `action` 值为的属性 `test`. |
| `id` | 您正在测试的密钥的ID。 此ID必须匹配请求路径中提供的ID。 |
| `type` | 运行的资源类型。 必须设置为 `secrets`. |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回密钥的详细信息，授权服务的响应包含在 `meta.test_exchange`.

```json
{ 
  "data": { 
    "id": "SE6c15a7a64f9041b5985558ed3e19a449", 
    "type": "secrets", 
    "attributes": { 
      "activated_at": null, 
      "created_at": "2021-07-14T19:33:25.628Z", 
      "credentials": { 
        "token_url": "https://token_url.test/token/authorize?required_param=value",
        "client_id": "test_client_id", 
        "client_secret": "test_client_secret", 
        "refresh_offset": 14400, 
      },
      "expires_at": null, 
      "name": "Example Secret", 
      "refresh_at": null, 
      "status": "pending", 
      "type_of": "oauth2", 
      "updated_at": "2021-07-14T19:33:25.628Z", 
    }, 
    "relationships": { 
      "property": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
        }, 
        "data": { 
          "id": "PR9eff664dc6014217b76939bb78b83976", 
          "type": "properties" 
        } 
      }, 
      "environment": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/environment" 
        }, 
        "data": { 
          "id": "EN04cdddbdb6574170bcac9f470f3b8087", 
          "type": "environments" 
        }, 
        "meta": { 
          "stage": "development" 
        } 
      }, 
      "notes": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/notes" 
        } 
      } 
    }, 
    "links": { 
      "self": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154", 
      "property": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
    }, 
    "meta": { 
      "test_exchange": { 
        "access_token": "FpIkBn3zxW0fH6EBC4MB", 
        "expires_in": 36000, 
        "token_type": "Bearer", 
      } 
    } 
  } 
}
```

## 重试密钥 {#retry}

重试密钥是手动触发密钥交换的操作。 您可以通过在密钥请求的路径中包含其ID来重试PATCH。

**API格式**

```http
PATCH /secrets/{SECRET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 要重试的密钥的ID。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X PATCH \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "type_of": "token"
          },
          "meta": {
            "action": "retry"
          },
          "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
          "type": "secrets"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `attributes` | 必须包含 `type_of` 与要更新的密钥匹配的属性(`token`, `simple-http`或 `oauth2`)。 |
| `meta` | 必须包含 `action` 值为的属性 `retry`. |
| `id` | 正在重试的密钥的ID。 此ID必须匹配请求路径中提供的ID。 |
| `type` | 运行的资源类型。 必须设置为 `secrets`. |

{style=&quot;table-layout:auto&quot;}

**响应**

成功响应会返回密钥的详细信息，其状态将重置为 `pending`. 交换完成后，密钥的状态将更新为 `succeeded` 或 `failed` 取决于结果。

```json
{
  "data": {
    "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
    "type": "secrets",
    "attributes": {
      "created_at": "2021-07-16T22:29:41.135Z",
      "updated_at": "2021-07-16T22:29:41.135Z",
      "name": "Example Secret",
      "type_of": "token",
      "activated_at": null,
      "expires_at": null,
      "refresh_at": null,
      "status": "pending",
      "credentials": {
        }
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
        },
        "data": {
          "id": "PR19717d5acf114209a5aebd0f2b228438",
          "type": "properties"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment"
        },
        "data": {
          "id": "EN04d820606cc74d5eaf51616e8b50201a",
          "type": "environments"
        },
        "meta": {
          "stage": "development"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/notes"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3",
      "property": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
    }
  }
}
```

## 重新授权 `oauth2-google` 秘密 {#reauthorize}

每个 `oauth2-google` 密码包含 `meta.authorization_url_expires_at` 属性，指示授权URL何时过期。 此后，必须重新授权该密钥，才能续订身份验证过程。

重新授权 `oauth2-google` 机密，请PATCH有关机密。

**API格式**

```http
PATCH /secrets/{SECRET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 的 `id` 要重新授权的秘密。 |

**请求**

的 `data` 请求有效负载中的对象必须包含 `meta.action` 属性设置为 `reauthorize`.

```shell
curl -X PATCH \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "type_of": "oauth2-google"
          },
          "meta": {
            "action": "reauthorize"
          },
          "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
          "type": "secrets"
        }
      }'
```

**响应**

成功的响应会返回更新密钥的详细信息。 从此处，必须复制并粘贴 `meta.authorization_url` 浏览器以完成授权过程。

```json
{
  "data": {
    "id": "SE5fdfa4c0a2d8404e8b1bc38827cc41c9",
    "type": "secrets",
    "attributes": {
      "created_at": "2021-07-15T19:00:25.628Z", 
      "updated_at": "2021-07-15T19:00:25.628Z", 
      "name": "Example Secret", 
      "type_of": "oauth2-google", 
      "activated_at": null, 
      "expires_at": null, 
      "refresh_at": null, 
      "status": "pending", 
      "credentials": { 
        "scopes": [
          "https://www.googleapis.com/auth/adwords",
          "https://www.googleapis.com/auth/pubsub"
        ], 
      } 
    }, 
    "relationships": { 
      "property": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE5fdfa4c0a2d8404e8b1bc38827cc41c9/property" 
        }, 
        "data": { 
          "id": "PR9eff664dc6014217b76939bb78b83976", 
          "type": "properties" 
        } 
      }, 
      "environment": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE5fdfa4c0a2d8404e8b1bc38827cc41c9/environment" 
        }, 
        "data": { 
          "id": "EN04cdddbdb6574170bcac9f470f3b8087", 
          "type": "environments" 
        }, 
        "meta": { 
          "stage": "development" 
        } 
      }, 
      "notes": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE5fdfa4c0a2d8404e8b1bc38827cc41c9/notes" 
        } 
      } 
    }, 
    "links": { 
      "self": "https://reactor.adobe.io/secrets/SE5fdfa4c0a2d8404e8b1bc38827cc41c9", 
      "property": "https://reactor.adobe.io/secrets/SE5fdfa4c0a2d8404e8b1bc38827cc41c9/property" 
    }, 
    "meta": { 
      "authorization_url": "https://accounts.google.com/o/oauth2/auth?access_type=offline&approval_prompt=force&client_id=434635668552-0qvlu519fdjtnkvk8hu8c8dj8rg3723r.apps.googleusercontent.com&redirect_uri=https%3A%2F%2Freactor.adobe.io%2Foauth2%2Fcallback&response_type=code&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fadwords&state=state", 
      "authorization_url_expires_at": "2021-07-15T20:00:25.628Z" 
    } 
  } 
}
```

## 删除密钥 {#delete}

您可以删除密钥，方法是将密钥的ID包含在DELETE请求的路径中。 这是一个硬删除操作，会立即生效，不需要库重新发布。

此操作会从与其相关的环境中删除密钥，并删除基础资源。

>[!WARNING]
>
>如果已部署的规则引用已删除的密钥，则这些规则将立即停止运行。 引用此密钥的任何数据元素必须在以后更新或删除。

**API格式**

```http
DELETE /secrets/{SECRET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 要删除的密钥的ID。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**响应**

成功响应会返回HTTP状态204（无内容）和空响应主体，表示该密钥已从系统中删除。

## 列出机密的注释 {#notes}

Reactor API允许您向特定资源添加注释，包括密钥。 注释是对资源行为没有影响的文本批注，可用于各种用例。

>[!NOTE]
>
>请参阅 [注释终端指南](./notes.md) 有关如何为Reactor API资源创建和编辑注释的详细信息。

您可以通过发出GET请求来检索与密钥相关的所有注释。

**API格式**

```http
GET /secrets/{SECRET_ID}/notes
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 要列出其注释的密钥的ID。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**响应**

成功响应会返回属于该密钥的注释列表。

```json
{
  "data": [
    {
      "id": "NTe666dbcc2f204218b6fde2fe60ab7043",
      "type": "notes",
      "attributes": {
        "author_display_name": "John Doe",
        "author_email": "jdoe@example.com",
        "created_at": "2021-07-16T22:29:58.259Z",
        "text": "This is a secret note."
      },
      "relationships": {
        "resource": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1"
          },
          "data": {
            "id": "SE591d3b86910f4e6883f0e1c36e54bff1",
            "type": "secrets"
          }
        }
      },
      "links": {
        "resource": "https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1",
        "self": "https://reactor.adobe.io/notes/NTe666dbcc2f204218b6fde2fe60ab7043"
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

## 检索密钥的相关资源 {#related}

以下调用演示了如何检索密钥的相关资源。 When [查了个秘密](#lookup)，则这些关系列在 `relationships` 属性。

请参阅 [关系指南](../guides/relationships.md) 有关Reactor API中关系的更多信息。

### 查找相关环境以获取密钥 {#environment}

您可以通过附加 `/environment` 到GET请求的路径。

**API格式**

```http
GET /secrets/{SECRET_ID}/environment
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 要查找其环境的密钥的ID。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**响应**

成功的响应会返回环境的详细信息。

```json
{
  "data": {
    "id": "EN33e8d63ac647448da1f77ced5c3c8580",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2021-07-16T22:19:13.438Z",
      "library_path": "bc12f2b85d11/b9a3067414ff",
      "library_name": "launch-3b6c4eea15ae-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-3b6c4eea15ae-development.min.js",
          "minified": true,
          "references": [
            "bc12f2b85d11/b9a3067414ff/launch-3b6c4eea15ae-development.min.js"
          ],
          "license_path": "bc12f2b85d11/b9a3067414ff/launch-3b6c4eea15ae-development.js"
        },
        {
          "library_name": "launch-3b6c4eea15ae-development.js",
          "minified": false,
          "references": [
            "bc12f2b85d11/b9a3067414ff/launch-3b6c4eea15ae-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": null,
      "stage": "development",
      "updated_at": "2021-07-16T22:19:13.438Z",
      "status": "succeeded",
      "token": "3b6c4eea15ae"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/host",
          "self": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/relationships/host"
        },
        "data": {
          "id": "HT7d5cf665463e46a1968ada1ceb1b5ca7",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/property"
        },
        "data": {
          "id": "PRba81d3027db846b084212391aa5d2f1f",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRba81d3027db846b084212391aa5d2f1f",
      "self": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

### 查找密钥的相关属性 {#property}

您可以通过附加 `/property` 到GET请求的路径。

**API格式**

```http
GET /secrets/{SECRET_ID}/property
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 要查找其资产的密钥的ID。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**响应**

成功的响应会返回属性的详细信息。

```json
{
  "data": {
    "id": "PR2d191feafef54c5da4ddb5ef647d4867",
    "type": "properties",
    "attributes": {
      "created_at": "2021-07-16T22:26:25.320Z",
      "enabled": true,
      "name": "Kessel Edge Example Property",
      "updated_at": "2021-07-16T22:26:25.320Z",
      "platform": "edge",
      "development": false,
      "token": "8efbe7023155"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/company"
        },
        "data": {
          "id": "COc26fb19f87d24cbe827a70ad2a672093",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/COc26fb19f87d24cbe827a70ad2a672093",
      "data_elements": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/environments",
      "extensions": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/extensions",
      "rules": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/rules",
      "self": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "edit_property",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```
