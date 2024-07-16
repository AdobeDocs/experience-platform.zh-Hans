---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK；SDK
title: 为自助源配置身份验证规范(Batch SDK)
description: 本文档概述了为使用自助源(Batch SDK)而需要准备的配置。
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---

# 为自助源配置身份验证规范(Batch SDK)

身份验证规范定义Adobe Experience Platform用户可以如何连接到您的源。

`authSpec`数组包含有关将源连接到平台所需的身份验证参数的信息。 任何给定的源都可以支持多种不同类型的身份验证。

## 身份验证规范

自助源（批处理SDK）支持OAuth 2刷新代码和基本身份验证。 有关使用OAuth 2刷新代码和基本身份验证的指导，请参阅下表

### OAuth 2刷新代码

OAuth 2刷新代码允许通过生成临时访问令牌和刷新令牌来安全地访问应用程序。 访问令牌允许您安全地访问资源，而无需提供其他凭据，而刷新令牌允许您在访问令牌过期后生成新的访问令牌。

```json
{
  "name": "OAuth2 Refresh Code",
  "type": "OAuth2RefreshCode",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
    "properties": {
      "authorizationTestUrl": {
        "description": "Authorization test url to validate accessToken.",
        "type": "string"
      },
      "clientId": {
        "description": "Client id of user account.",
        "type": "string"
      },
      "clientSecret": {
        "description": "Client secret of user account.",
        "type": "string",
        "format": "password"
      },
      "accessToken": {
        "description": "Access Token",
        "type": "string",
        "format": "password"
      },
      "refreshToken": {
        "description": "Refresh Token",
        "type": "string",
        "format": "password"
      },
      "expirationDate": {
        "description": "Date of token expiry.",
        "type": "string",
        "format": "date",
        "uiAttributes": {
          "hidden": true
        }
      },
      "accessTokenUrl": {
        "description": "Access token url to fetch access token.",
        "type": "string"
      },
      "requestParameterOverride": {
        "type": "object",
        "description": "Specify parameter to override.",
        "properties": {
          "accessTokenField": {
            "description": "Access token field name to override.",
            "type": "string"
          },
          "refreshTokenField": {
            "description": "Refresh token field name to override.",
            "type": "string"
          },
          "expireInField": {
            "description": "ExpireIn field name to override.",
            "type": "string"
          },
          "authenticationMethod": {
            "description": "Authentication method override.",
            "type": "string",
            "enum": [
              "GET",
              "POST"
            ]
          },
          "clientId": {
            "description": "ClientId field name override.",
            "type": "string"
          },
          "clientSecret": {
            "description": "ClientSecret field name override.",
            "type": "string"
          }
        }
      }
    },
    "required": [
      "accessToken"
    ]
  }
}
```

| 属性 | 描述 | 示例 |
| --- | --- | --- |
| `authSpec.name` | 显示支持的身份验证类型的名称。 | `oAuth2-refresh-code` |
| `authSpec.type` | 定义源支持的身份验证类型。 | `oAuth2-refresh-code` |
| `authSpec.spec` | 包含有关身份验证架构、数据类型和属性的信息。 |
| `authSpec.spec.$schema` | 定义用于身份验证的架构。 | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | 定义架构的数据类型。 | `object` |
| `authSpec.spec.properties` | 包含有关用于身份验证的凭据的信息。 |
| `authSpec.spec.properties.description` | 显示凭据的简短说明。 |
| `authSpec.spec.properties.type` | 定义凭据的数据类型。 | `string` |
| `authSpec.spec.properties.clientId` | 与您的应用程序关联的客户端ID。 客户端ID将与您的客户端密钥结合使用，以检索您的访问令牌。 |
| `authSpec.spec.properties.clientSecret` | 与您的应用程序关联的客户端密钥。 客户端密钥将与您的客户端ID结合使用，以检索您的访问令牌。 |
| `authSpec.spec.properties.accessToken` | 访问令牌可授权您对应用程序的安全访问。 |
| `authSpec.spec.properties.refreshToken` | 刷新令牌用于在访问令牌过期时生成新的访问令牌。 |
| `authSpec.spec.properties.expirationDate` | 定义访问令牌的过期日期。 |
| `authSpec.spec.properties.refreshTokenUrl` | 用于检索刷新令牌的URL。 |
| `authSpec.spec.properties.accessTokenUrl` | 用于检索刷新令牌的URL。 |
| `authSpec.spec.properties.requestParameterOverride` | 允许您指定验证时要覆盖的凭据参数。 |
| `authSpec.spec.required` | 显示进行身份验证所需的凭据。 | `accessToken` |

{style="table-layout:auto"}


### 基本身份验证

基本身份验证是一种身份验证类型，它允许您使用帐户用户名和帐户密码的组合来访问应用程序。

```json
{
  "name": "Basic Authentication",
  "type": "BasicAuthentication",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "defines auth params required for connecting to rest service.",
    "properties": {
      "username": {
        "description": "Username to connect rest endpoint.",
        "type": "string"
      },
      "password": {
        "description": "Password to connect rest endpoint.",
        "type": "string",
        "format": "password"
      }
    },
    "required": [
      "username",
      "password"
    ]
  }
}
```

| 属性 | 描述 | 示例 |
| --- | --- | --- |
| `authSpec.name` | 显示支持的身份验证类型的名称。 | `Basic Authentication` |
| `authSpec.type` | 定义源支持的身份验证类型。 | `BasicAuthentication` |
| `authSpec.spec` | 包含有关身份验证架构、数据类型和属性的信息。 |
| `authSpec.spec.$schema` | 定义用于身份验证的架构。 | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | 定义架构的数据类型。 | `object` |
| `authSpec.spec.description` | 显示特定于您的身份验证类型的详细信息。 |
| `authSpec.spec.properties` | 包含有关用于身份验证的凭据的信息。 |
| `authSpec.spec.properties.username` | 与您的应用程序关联的帐户用户名。 |
| `authSpec.spec.properties.password` | 与应用程序关联的帐户密码。 |
| `authSpec.spec.required` | 指定所需的字段作为在Platform中输入的必需值。 | `username` |

{style="table-layout:auto"}

## 身份验证规范示例

以下是使用[[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md)源的已完成身份验证规范示例。

```json
  "authSpec": [
    {
      "name": "OAuth2 Refresh Code",
      "type": "OAuth2RefreshCode",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
        "properties": {
          "authorizationTestUrl": {
            "description": "Authorization test url to validate accessToken.",
            "type": "string"
          },
          "accessToken": {
            "description": "Access Token of mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "accessToken"
        ]
      }
    },
    {
      "name": "Basic Authentication",
      "type": "BasicAuthentication",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines auth params required for connecting to rest service.",
        "properties": {
          "username": {
            "description": "Username to connect mailChimp endpoint.",
            "type": "string"
          },
          "password": {
            "description": "Password to connect mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "username",
          "password"
        ]
      }
    }
  ],
```

## 后续步骤

填充身份验证规范后，您可以继续配置要集成到Platform的源的源规范。 有关详细信息，请参阅[配置源规范](./sourcespec.md)上的文档。
