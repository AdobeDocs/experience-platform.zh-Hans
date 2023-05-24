---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
title: 設定自助式來源的驗證規格（批次SDK）
description: 本檔案提供使用Self-Serve Sources (Batch SDK)所需準備的設定概觀。
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 1%

---

# 設定自助式來源的驗證規格（批次SDK）

驗證規格會定義Adobe Experience Platform使用者如何連線至您的來源。

此 `authSpec` 陣列包含將來源連線至Platform所需的驗證引數資訊。 任何特定來源都可以支援多種不同型別的驗證。

## 驗證規格

自助來源（批次SDK）支援OAuth 2重新整理程式碼和基本驗證。 請參閱下表，取得使用OAuth 2重新整理程式碼和基本驗證的指引

### OAuth 2重新整理程式碼

OAuth 2重新整理程式碼可產生暫時存取權杖和重新整理權杖，以安全地存取應用程式。 存取權杖可讓您安全地存取您的資源，而無需提供其他認證，而重新整理權杖可讓您在存取權杖過期後產生新的存取權杖。

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
| `authSpec.name` | 顯示支援的驗證型別名稱。 | `oAuth2-refresh-code` |
| `authSpec.type` | 定義來源支援的驗證型別。 | `oAuth2-refresh-code` |
| `authSpec.spec` | 包含有關驗證的結構描述、資料型別和屬性的資訊。 |
| `authSpec.spec.$schema` | 定義用於驗證的結構描述。 | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | 定義結構描述的資料型別。 | `object` |
| `authSpec.spec.properties` | 包含用於驗證的認證的相關資訊。 |
| `authSpec.spec.properties.description` | 顯示認證的簡短說明。 |
| `authSpec.spec.properties.type` | 定義認證的資料型別。 | `string` |
| `authSpec.spec.properties.clientId` | 與您的應用程式相關聯的使用者端ID。 使用者端ID會與使用者端密碼搭配使用，以擷取您的存取權杖。 |
| `authSpec.spec.properties.clientSecret` | 與您的應用程式相關聯的使用者端密碼。 使用者端密碼會與使用者端ID搭配使用，以擷取您的存取權杖。 |
| `authSpec.spec.properties.accessToken` | 存取權杖會授權您對應用程式的安全存取。 |
| `authSpec.spec.properties.refreshToken` | 重新整理權杖是用來在存取權杖過期時產生新的存取權杖。 |
| `authSpec.spec.properties.expirationDate` | 定義存取權杖的到期日。 |
| `authSpec.spec.properties.refreshTokenUrl` | 用來擷取重新整理權杖的URL。 |
| `authSpec.spec.properties.accessTokenUrl` | 用來擷取重新整理權杖的URL。 |
| `authSpec.spec.properties.requestParameterOverride` | 可讓您指定認證引數以在驗證時覆寫。 |
| `authSpec.spec.required` | 顯示驗證所需的認證。 | `accessToken` |

{style="table-layout:auto"}


### 基本驗證

基本驗證是一種驗證型別，可讓您使用帳戶使用者名稱和帳戶密碼的組合來存取應用程式。

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
| `authSpec.name` | 顯示支援的驗證型別名稱。 | `Basic Authentication` |
| `authSpec.type` | 定義來源支援的驗證型別。 | `BasicAuthentication` |
| `authSpec.spec` | 包含有關驗證的結構描述、資料型別和屬性的資訊。 |
| `authSpec.spec.$schema` | 定義用於驗證的結構描述。 | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | 定義結構描述的資料型別。 | `object` |
| `authSpec.spec.description` | 顯示驗證型別的進一步特定資訊。 |
| `authSpec.spec.properties` | 包含用於驗證的認證的相關資訊。 |
| `authSpec.spec.properties.username` | 與您的應用程式相關聯的帳戶使用者名稱。 |
| `authSpec.spec.properties.password` | 與您的應用程式相關聯的帳戶密碼。 |
| `authSpec.spec.required` | 指定在Platform中輸入必填欄位作為必要值。 | `username` |

{style="table-layout:auto"}

## 範例驗證規格

以下範例是使用 [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md) 來源。

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

填入驗證規格後，您可以繼續設定要整合至平台的來源的來源規格。 檢視檔案： [設定來源規格](./sourcespec.md) 以取得詳細資訊。
