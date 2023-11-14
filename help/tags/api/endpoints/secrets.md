---
title: 密钥端点
description: 了解如何在Reactor API中调用/secrets端点。
exl-id: 76875a28-5d13-402d-8543-24db7e2bee8e
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 4%

---

# 密钥端点

机密是仅存在于事件转发属性（具有的属性）中的资源 `platform` 属性设置为 `edge`)。 它们允许事件转发向另一个系统验证以进行安全的数据交换。

本指南向您说明如何调用 `/secrets` reactor API中的端点。 有关不同密钥类型及其使用方法的详细说明，请参阅 [密钥](../guides/secrets.md) 然后再参阅本指南。

## 快速入门

本指南中使用的端点是 [Reactor API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). 在继续之前，请查看 [快速入门指南](../getting-started.md) 有关如何对API进行身份验证的重要信息。

## 检索属性的密钥列表 {#list-property}

您可以通过发出GET请求来列出属于某个资产的密钥。

**API格式**

```http
GET /properties/{PROPERTY_ID}/secrets
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 要列出其密码的属性的ID。 |

{style="table-layout:auto"}

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

成功的响应将返回属于该属性的密钥列表。

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

您可以通过发出GET请求来列出属于环境的密钥。

**API格式**

```http
GET /environments/{ENVIRONMENT_ID}/secrets
```

| 参数 | 描述 |
| --- | --- |
| `{ENVIRONMENT_ID}` | 要列出其密码的环境的ID。 |

{style="table-layout:auto"}

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

成功的响应将返回属于环境的密钥列表。

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

## 查找密钥 {#lookup}

通过在GET请求的路径中包含某个密码的ID，您可以查找该密码。

**API格式**

```http
GET /secrets/{SECRET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 要查找的密码的ID。 |

{style="table-layout:auto"}

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

成功的响应将返回密码的详细信息。

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
>创建新密钥时，API会返回包含该资源信息的即时响应。 同时，触发秘密交换任务，以测试凭证交换是否正常工作。 此任务以异步方式处理，并将密码的状态属性更新为 `succeeded` 或 `failed` 取决于结果。

**API格式**

```http
POST /properties/{PROPERTY_ID}/secrets
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 要在其下定义密码的属性的ID。 |

{style="table-layout:auto"}

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
| `type_of` | 密码表示的身份验证凭据的类型。 具有三个接受的值：<ul><li>`token`：令牌字符串。</li><li>`simple-http`：用户名和密码。</li><li>`oauth2`：符合OAuth标准的凭据。</li></ul> |
| `credentials` | 包含密码的凭据值的对象。 根据 `type_of` 属性，必须提供不同的属性。 请参阅以下部分 [凭据](../guides/secrets.md#credentials) 有关每种类型的要求的详细信息，请参阅密钥指南。 |
| `relationships.environment` | 每个密钥必须在首次创建时与环境相关联。 此 `data` 此属性中的对象必须包含 `id` 要分配到的环境的密钥，以及 `type` 值 `environments`. |
| `type` | 正在创建的资源的类型。 对于此调用，值必须为 `secrets`. |

{style="table-layout:auto"}

**响应**

成功的响应将返回密码的详细信息。 请注意，根据密码的类型，某些属性位于 `credentials` 可能被隐藏。

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

## 测试 `oauth2` 密码 {#test}

>[!NOTE]
>
>此操作只能对具有的密码执行 `type_of` 值 `oauth2`.

您可以测试 `oauth2` 通过在PATCH请求的路径中包含其ID来保密。 测试操作执行交换并将授权服务响应包括在 `test_exchange` 秘密的属性 `meta` 对象。 此操作不会更新密码本身。

**API格式**

```http
PATCH /secrets/{SECRET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 的ID `oauth2` 要测试的秘密。 |

{style="table-layout:auto"}

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
| `id` | 您正在测试的密码的ID。 这必须与请求路径中提供的ID匹配。 |
| `type` | 正在操作的资源的类型。 必须设置为 `secrets`. |

{style="table-layout:auto"}

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

## 重试密码 {#retry}

重试密钥是手动触发密钥交换的操作。 通过在PATCH请求的路径中包含密码的ID，可以重试该密码。

**API格式**

```http
PATCH /secrets/{SECRET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 要重试的密码的ID。 |

{style="table-layout:auto"}

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
| `attributes` | 必须包含 `type_of` 与正在更新的密码的属性匹配的属性(`token`， `simple-http`，或 `oauth2`)。 |
| `meta` | 必须包含 `action` 值为的属性 `retry`. |
| `id` | 您正在重试的机密的ID。 这必须与请求路径中提供的ID匹配。 |
| `type` | 正在操作的资源的类型。 必须设置为 `secrets`. |

{style="table-layout:auto"}

**响应**

成功的响应将返回密码的详细信息，其状态将重置为 `pending`. 交换完成后，密码的状态将更新为 `succeeded` 或 `failed` 取决于结果。

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

## 重新授权 `oauth2-google` 密码 {#reauthorize}

每个 `oauth2-google` 密码包含 `meta.authorization_url_expires_at` 指示授权URL何时到期的属性。 在此时间之后，必须重新授权密钥，才能更新身份验证过程。

要重新授权 `oauth2-google` 秘诀，对相关秘诀提出PATCH请求。

**API格式**

```http
PATCH /secrets/{SECRET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 此 `id` 要重新授权的秘密。 |

**请求**

此 `data` 请求有效负载中的对象必须包含 `meta.action` 属性设置为 `reauthorize`.

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

成功的响应将返回已更新密钥的详细信息。 您必须从此处复制并粘贴 `meta.authorization_url` 导入浏览器以完成授权过程。

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

## 删除密码 {#delete}

通过在DELETE请求的路径中包含密码的ID，可以删除密码。 这是硬删除，会立即生效，无需重新发布库。

此操作会从与其相关的环境中删除密码，并删除基础资源。

>[!WARNING]
>
>如果您有任何已部署的规则引用了已删除的密钥，则这些规则将立即停止运行。 以后必须更新或删除引用此密码的任何数据元素。

**API格式**

```http
DELETE /secrets/{SECRET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 要删除的密码的ID。 |

{style="table-layout:auto"}

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

成功的响应返回HTTP状态204（无内容）和空响应正文，指示已从系统中删除密码。

## 列出密码的注释 {#notes}

Reactor API允许您向特定资源添加注释，包括密钥。 注释是对资源行为没有影响的文本批注，可用于各种用例。

>[!NOTE]
>
>请参阅 [注释端点指南](./notes.md) 有关如何创建和编辑Reactor API资源的注释的详细信息。

您可以通过发出GET请求来检索与密码相关的所有注释。

**API格式**

```http
GET /secrets/{SECRET_ID}/notes
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 要列出其注释的密码的ID。 |

{style="table-layout:auto"}

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

成功的响应将返回属于密码的注释列表。

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

## 检索密码的相关资源 {#related}

以下调用演示了如何检索密码的相关资源。 时间 [查找密钥](#lookup)，这些关系列在 `relationships` 属性。

请参阅 [关系指南](../guides/relationships.md) 有关Reactor API中关系的更多信息。

### 查找密码的相关环境 {#environment}

您可以通过附加密码来查找使用密码的环境 `/environment` 到GET请求的路径。

**API格式**

```http
GET /secrets/{SECRET_ID}/environment
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 要查找其环境的密码的ID。 |

{style="table-layout:auto"}

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

成功的响应将返回环境的详细信息。

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

### 查找密码的相关属性 {#property}

您可以通过附加来查找拥有机密的属性 `/property` 到GET请求的路径。

**API格式**

```http
GET /secrets/{SECRET_ID}/property
```

| 参数 | 描述 |
| --- | --- |
| `{SECRET_ID}` | 要查找其属性的密码的ID。 |

{style="table-layout:auto"}

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

成功的响应将返回该属性的详细信息。

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
