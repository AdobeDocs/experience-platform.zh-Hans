---
description: 本页介绍了Destination SDK支持的各种OAuth 2授权流程，并提供了有关为目标设置OAuth 2授权的说明。
title: OAuth 2授权
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 2%

---


# OAuth 2授权

Destination SDK支持多种针对目标的授权方法。 其中有一个选项可使用[OAuth 2授权框架](https://tools.ietf.org/html/rfc6749)向您的目标进行身份验证。

本页介绍了Destination SDK支持的各种OAuth 2授权流程，并提供了有关为目标设置OAuth 2授权的说明。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;****。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 支持的集成类型 {#supported-integration-types}

有关哪些类型的集成支持此页面上描述的功能，请参阅下表。

| 集成类型 | 支持功能 |
|---|---|
| 实时（流）集成 | 是 |
| 基于文件（批处理）的集成 | 否 |

## 如何将OAuth 2授权详细信息添加到您的目标配置 {#how-to-setup}

### 系统中的先决条件 {#prerequisites}

第一步，您必须在系统中为Adobe Experience Platform创建应用程序，或在系统中注册Experience Platform。 目标是生成客户端ID和客户端密钥，向目标验证Experience Platform时需要这两个变量。

在您的系统中，作为此配置的一部分，您需要Adobe Experience Platform OAuth 2重定向/回调URL，可从以下列表中获取该URL。

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-can2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-gbr9.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>只有授权代码为[的](#authorization-code)OAuth 2授予类型才需要执行在系统中注册Adobe Experience Platform的重定向/回调URL的步骤。 对于其他两种受支持的授权类型（密码和客户端凭据），您可以跳过此步骤。

在此步骤结束时，您应该：

* 客户端ID；
* 客户密码；
* Adobe的回调URL（用于授权代码授权）。

### 在Destination SDK中需要执行的操作 {#to-do-in-destination-sdk}

要为您在Experience Platform中的目标设置OAuth 2授权，您必须在[参数下将OAuth 2详细信息添加到](../../authoring-api/destination-configuration/create-destination-configuration.md)目标配置`customerAuthenticationConfigurations`。 有关详细示例，请参阅[客户身份验证](../../functionality/destination-configuration/customer-authentication.md)。 根据您的OAuth 2授权授予类型，关于您需要向配置模板添加哪些字段的具体说明，请参阅本页下面的内容。

## 支持的OAuth 2授权类型 {#oauth2-grant-types}

Experience Platform支持下表中的三种OAuth 2授权类型。 如果您设置了自定义OAuth 2，Adobe将能够借助集成中的自定义字段支持它。 有关更多信息，请参阅每种授权类型的章节。

>[!IMPORTANT]
>
>* 您可以按照以下各节中的说明提供输入参数。 Adobe内部系统连接到您平台的授权系统并获取输出参数，这些参数用于验证用户并保持对目标的授权。
>* 表格中以粗体突出显示的输入参数是OAuth 2授权流中的必需参数。 其他参数是可选的。 此处未显示其他自定义输入参数，但这些参数在[自定义您的OAuth 2配置](#customize-configuration)和[访问令牌刷新](#access-token-refresh)部分中有详细介绍。

| OAuth 2授权 | 输入 | 输出 |
|---------|----------|---------|
| 授权码 | <ul><li><b>clientId</b></li><li><b>客户端密钥</b></li><li>范围</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokentype</li></ul> |
| 密码 | <ul><li><b>clientId</b></li><li><b>客户端密钥</b></li><li>范围</li><li><b>accessTokenUrl</b></li><li><b>用户名</b></li><li><b>密码</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokentype</li></ul> |
| 客户端凭据 | <ul><li><b>clientId</b></li><li><b>客户端密钥</b></li><li>范围</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokentype</li></ul> |

{style="table-layout:auto"}

上表列出了标准OAuth 2流程中使用的字段。 除了这些标准字段之外，各种合作伙伴集成可能还需要其他输入和输出。 Adobe为Destination SDK设计了一个灵活的OAuth 2授权框架，该框架可以处理上述标准字段模式的变化，同时支持自动重新生成无效输出（如过期的访问令牌）的机制。

在所有情况下，输出都包含访问令牌，Experience Platform会使用该令牌对您的目标进行身份验证和维护授权。

Adobe为OAuth 2授权设计的系统：

* 支持所有三个OAuth 2授权，并会考虑其中的任何变量，例如附加数据字段、非标准API调用等。
* 支持具有不同生命周期值（90天、30分钟或您指定的任何其他生命周期值）的访问令牌。
* 支持使用或不使用刷新令牌的OAuth 2授权流。

## OAuth 2，带有授权代码 {#authorization-code}

如果您的目标支持标准OAuth 2.0授权代码流（请阅读[RFC标准规范](https://tools.ietf.org/html/rfc6749#section-4.1)）或其变体，请查阅下面的必需和可选字段：

| OAuth 2授权 | 输入 | 输出 |
|---------|----------|---------|
| 授权码 | <ul><li><b>clientId</b></li><li><b>客户端密钥</b></li><li>范围</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokentype</li></ul> |

{style="table-layout:auto"}

要为您的目标设置此授权方法，请在您[创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)时，将以下行添加到您的配置中：

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_AUTHORIZATION_CODE",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "authorizationUrl": "https://www.moviestar.com/dialog/OAuth",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `authType` | 字符串 | 使用“OAUTH2”。 |
| `grant` | 字符串 | 使用“OAUTH2_AUTHORIZATION_CODE”。 |
| `accessTokenUrl` | 字符串 | 您这边的URL，用于发出访问令牌并（可选）刷新令牌。 |
| `authorizationUrl` | 字符串 | 授权服务器的URL，您可以在其中将用户重定向到您的应用程序。 |
| `refreshTokenUrl` | 字符串 | *可选。*&#x200B;您这边的URL，这会产生刷新令牌的问题。 通常，`refreshTokenUrl`与`accessTokenUrl`相同。 |
| `clientId` | 字符串 | 系统分配给Adobe Experience Platform的客户端ID。 |
| `clientSecret` | 字符串 | 系统分配给Adobe Experience Platform的客户端密码。 |
| `scope` | 字符串列表 | *可选*。 设置访问令牌允许Experience Platform对您的资源执行的范围。 示例：“read， write”。 |

{style="table-layout:auto"}

## 具有密码授予的OAuth 2

对于OAuth 2密码授予（请阅读[RFC标准规范](https://tools.ietf.org/html/rfc6749#section-4.3)），Experience Platform需要用户用户名和密码。 在授权流中，Experience Platform将这些凭据交换为访问令牌和（可选）刷新令牌。
Adobe利用以下标准输入来简化目标配置，并能够覆盖值：

| OAuth 2授权 | 输入 | 输出 |
|---------|----------|---------|
| 密码 | <ul><li><b>clientId</b></li><li><b>客户端密钥</b></li><li>范围</li><li><b>accessTokenUrl</b></li><li><b>用户名</b></li><li><b>密码</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokentype</li></ul> |

{style="table-layout:auto"}

>[!NOTE]
>
> 您不需要在下面的配置中为`username`和`password`添加任何参数。 在目标配置中添加`"grant": "OAUTH2_PASSWORD"`时，系统会要求用户在Experience Platform UI中提供用户名和密码，用户在对您的目标进行身份验证时。

要为您的目标设置此授权方法，请在您[创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)时，将以下行添加到您的配置中：

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_PASSWORD",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `authType` | 字符串 | 使用“OAUTH2”。 |
| `grant` | 字符串 | 使用“OAUTH2_PASSWORD”。 |
| `accessTokenUrl` | 字符串 | 您这边的URL，用于发出访问令牌并（可选）刷新令牌。 |
| `clientId` | 字符串 | 系统分配给Adobe Experience Platform的客户端ID。 |
| `clientSecret` | 字符串 | 系统分配给Adobe Experience Platform的客户端密码。 |
| `scope` | 字符串列表 | *可选*。 设置访问令牌允许Experience Platform对您的资源执行的范围。 示例：“read， write”。 |

{style="table-layout:auto"}

## 具有客户端凭据授权的OAuth 2

您可以配置OAuth 2客户端凭据（读取[RFC标准规范](https://tools.ietf.org/html/rfc6749#section-4.4)）目标，该目标支持下面列出的标准输入和输出。 您可以自定义值。 有关详细信息，请参阅[自定义您的OAuth 2配置](#customize-configuration)。

| OAuth 2授权 | 输入 | 输出 |
|---------|----------|---------|
| 客户端凭据 | <ul><li><b>clientId</b></li><li><b>客户端密钥</b></li><li>范围</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokentype</li></ul> |

{style="table-layout:auto"}

要为您的目标设置此授权方法，请在您[创建目标配置](../../authoring-api/destination-configuration/create-destination-configuration.md)时，将以下行添加到您的配置中：

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_CLIENT_CREDENTIALS",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `authType` | 字符串 | 使用“OAUTH2”。 |
| `grant` | 字符串 | 使用“OAUTH2_CLIENT_CREDENTIALS”。 |
| `accessTokenUrl` | 字符串 | 授权服务器的URL，它会颁发一个访问令牌和一个可选的刷新令牌。 |
| `refreshTokenUrl` | 字符串 | *可选。*&#x200B;您这边的URL，这会产生刷新令牌的问题。 通常，`refreshTokenUrl`与`accessTokenUrl`相同。 |
| `clientId` | 字符串 | 系统分配给Adobe Experience Platform的客户端ID。 |
| `clientSecret` | 字符串 | 系统分配给Adobe Experience Platform的客户端密码。 |
| `scope` | 字符串列表 | *可选*。 设置访问令牌允许Experience Platform对您的资源执行的范围。 示例：“read， write”。 |

{style="table-layout:auto"}

## 自定义您的OAuth 2配置 {#customize-configuration}

上节中描述的配置描述了标准OAuth 2授权。 但是，由Adobe设计的系统提供了灵活性，因此您可以将自定义参数用于OAuth 2授权中的任何变体。 要自定义标准OAuth 2设置，请使用`authenticationDataFields`参数，如以下示例所示。

### 示例1：使用`authenticationDataFields`捕获来自授权响应的信息 {#example-1}

在此示例中，目标平台的刷新令牌在一定时间后过期。 在这种情况下，合作伙伴设置`refreshTokenExpiration`自定义字段以从API响应中的`refresh_token_expires_in`字段获取刷新令牌过期时间。

```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "options":{
            
         },
         "grant":"OAUTH2_AUTHORIZATION_CODE",
         "accessTokenUrl":"https://api.moviestar.com/OAuth/access_token",
         "authorizationUrl":"https://api.moviestar.com/OAuth/authorization",
         "scope":[
            "read",
            "write",
            "delete"
         ],
         "refreshTokenUrl":"https://api.moviestar.com/OAuth/accessToken",
         "clientSecret":"client-secret-here",
         "authenticationDataFields":[
            {
               "name":"refreshTokenExpiration",
               "title":"Refresh Token Expires In",
               "description":"Time in seconds when the refresh token will expire",
               "type":"string",
               "isRequired":false,
               "source":"CUSTOMER",
               "authenticationResponsePath":"refresh_token_expires_in"
            }
         ]
      }
   ]
}  
```

### 示例2：使用`authenticationDataFields`提供特殊刷新令牌 {#example-2}

在此示例中，合作伙伴设置其目标以提供特殊的刷新令牌。 此外，API响应中不会返回访问令牌的过期日期，因此它们可以对默认值进行硬编码，在本例中为3600秒。

```json
      "authenticationDataFields": [
        {
            "name": "refreshToken",
            "value": "special_refresh_token"
        },
        {
            "name": "expiresIn",
            "value": 3600
        } 
      ]
```

### 示例3：用户在配置目标时输入客户端ID和客户端密码 {#example-3}

在此示例中，客户需要输入客户端ID、客户端密钥和帐户ID（客户用于登录到目标的ID），而不是创建全局客户端ID和客户端密钥，如[系统必备项](#prerequisites)部分中所示

```json
{
    //...
    "customerAuthenticationConfigurations": [
        {
            "authType": "OAUTH2",
            "grant": "OAUTH2_CLIENT_CREDENTIALS",
            "authenticationDataFields": [
                {
                    "name": "clientId",
                    "title": "Client ID",
                    "description": "Client ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                },
                {
                    "name": "clientSecret",
                    "title": "Client Secret",
                    "description": "Client Secret",
                    "type": "string",
                    "isRequired": true,
                    "format": "password",
                    "source": "CUSTOMER"
                },
                {
                    "name": "moviestarId",
                    "title": "Moviestar ID",
                    "description": "Moviestar ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                }
            ],
            "accessTokenRequest": {
                "destinationServerType": "URL_BASED",
                "urlBasedDestination": {
                    "url": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "https://{{ authData.moviestarId }}.yourdestination.com/identity/oauth/token"
                    }
                },
                "httpTemplate": {
                    "requestBody": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
                    },
                    "httpMethod": "POST",
                    "contentType": "application/x-www-form-urlencoded"
                },
                "responseFields": [
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.access_token }}",
                        "name": "accessToken"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.scope }}",
                        "name": "scope"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.token_type }}",
                        "name": "tokenType"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.expires_in }}",
                        "name": "expiresIn"
                    }
                ]
            }
        }
    ]
//...
}
```



您可以在`authenticationDataFields`中使用以下参数来自定义OAuth 2配置：

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `authenticationDataFields.name` | 字符串 | 自定义字段的名称。 |
| `authenticationDataFields.title` | 字符串 | 可为自定义字段提供的标题。 |
| `authenticationDataFields.description` | 字符串 | 您设置的自定义数据字段的描述。 |
| `authenticationDataFields.type` | 字符串 | 定义自定义数据字段的类型。 <br>接受的值： `string`、`boolean`、`integer` |
| `authenticationDataFields.isRequired` | 布尔值 | 指定授权流中是否需要自定义数据字段。 |
| `authenticationDataFields.format` | 字符串 | 当您选择`"format":"password"`时，Adobe将加密授权数据字段的值。 与`"fieldType": "CUSTOMER"`一起使用时，这也会在用户键入字段时隐藏UI中的输入。 |
| `authenticationDataFields.fieldType` | 字符串 | 指示当合作伙伴（您）在Experience Platform中设置您的目标时，输入是来自合作伙伴还是用户。 |
| `authenticationDataFields.value` | 字符串。 布尔型。 整数 | 自定义数据字段的值。 该值与`authenticationDataFields.type`中选择的类型匹配。 |
| `authenticationDataFields.authenticationResponsePath` | 字符串 | 指示您正在引用API响应路径中的哪个字段。 |

{style="table-layout:auto"}

## 访问令牌刷新 {#access-token-refresh}

Adobe设计了一个系统，无需用户登录回您的平台，即可刷新过期的访问令牌。 系统能够生成新的令牌，以便客户能够继续无缝地激活您的目标。

要设置访问令牌刷新，您可能需要配置一个模板化HTTP请求，以允许Adobe使用刷新令牌获取新的访问令牌。 如果访问令牌已过期，Adobe会采用您提供的模板化请求，并添加您提供的参数。 使用`accessTokenRequest`参数配置访问令牌刷新机制。


```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "grant":"OAUTH2_CLIENT_CREDENTIALS",
         "accessTokenRequest":{
            "destinationServerType":"URL_BASED",
            "urlBasedDestination":{
               "url":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"https://{{authData.customerId}}.yourdestination.com/identity/oauth/token"
               }
            },
            "httpTemplate":{
               "requestBody":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
               },
               "httpMethod":"POST",
               "contentType":"application/x-www-form-urlencoded",
               "headers":[
                  
               ]
            },
            "responseFields":[
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.expires_in }}",
                  "name":"expiresIn"
               },
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.access_token }}",
                  "name":"accessToken"
               }
            ],
            "validations":[
               {
                  "name":"access_token validation",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{response.body.access_token is empty }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"false"
                  }
               },
               {
                  "name":"response status",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{ response.status }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"200"
                  }
               }
            ]
         }
      }
   ]
}
```

您可以在`accessTokenRequest`中使用以下参数自定义令牌刷新过程：

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | 字符串 | 使用`URL_BASED`。 |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | 字符串 | <ul><li>如果您对`PEBBLE_V1`中的值使用模板，请使用`accessTokenRequest.urlBasedDestination.url.value`。</li><li> 如果字段`NONE`中的值为常量，则使用`accessTokenRequest.urlBasedDestination.url.value`。 </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | 字符串 | Experience Platform请求访问令牌的URL。 |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | 字符串 | <ul><li>如果您对`PEBBLE_V1`中的值使用模板，请使用`accessTokenRequest.httpTemplate.requestBody.value`。</li><li> 如果字段`NONE`中的值为常量，则使用`accessTokenRequest.httpTemplate.requestBody.value`。 </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | 字符串 | 使用模板化语言自定义访问令牌端点的HTTP请求中的字段。 有关如何使用模板自定义字段的信息，请参阅[模板约定](#templating-conventions)部分。 |
| `accessTokenRequest.httpTemplate.httpMethod` | 字符串 | 指定用于调用访问令牌端点的HTTP方法。 在大多数情况下，此值为`POST`。 |
| `accessTokenRequest.httpTemplate.contentType` | 字符串 | 指定对您的访问令牌端点的HTTP调用的内容类型。 <br>例如： `application/x-www-form-urlencoded`或`application/json`。 |
| `accessTokenRequest.httpTemplate.headers` | 字符串 | 指定是否应将任何标头添加到对访问令牌端点的HTTP调用中。 |
| `accessTokenRequest.responseFields.templatingStrategy` | 字符串 | <ul><li>如果您对`PEBBLE_V1`中的值使用模板，请使用`accessTokenRequest.responseFields.value`。</li><li> 如果字段`NONE`中的值为常量，则使用`accessTokenRequest.responseFields.value`。 </li></li> |
| `accessTokenRequest.responseFields.value` | 字符串 | 使用模板化语言从访问令牌端点访问HTTP响应中的字段。 有关如何使用模板自定义字段的信息，请参阅[模板约定](#templating-conventions)部分。 |
| `accessTokenRequest.validations.name` | 字符串 | 指示为此验证提供的名称。 |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | 字符串 | <ul><li>如果您对`PEBBLE_V1`中的值使用模板，请使用`accessTokenRequest.validations.actualValue.value`。</li><li> 如果字段`NONE`中的值为常量，则使用`accessTokenRequest.validations.actualValue.value`。 </li></li> |
| `accessTokenRequest.validations.actualValue.value` | 字符串 | 使用模板化语言访问HTTP响应中的字段。 有关如何使用模板自定义字段的信息，请参阅[模板约定](#templating-conventions)部分。 |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | 字符串 | <ul><li>如果您对`PEBBLE_V1`中的值使用模板，请使用`accessTokenRequest.validations.expectedValue.value`。</li><li> 如果字段`NONE`中的值为常量，则使用`accessTokenRequest.validations.expectedValue.value`。 </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | 字符串 | 使用模板化语言访问HTTP响应中的字段。 有关如何使用模板自定义字段的信息，请参阅[模板约定](#templating-conventions)部分。 |

{style="table-layout:auto"}

## 模板惯例 {#templating-conventions}

根据您的授权自定义，您可能需要访问授权响应中的数据字段，如上一节所示。 为此，请熟悉Adobe使用的[Pebble模板语言](https://pebbletemplates.io/)，并参阅下面的模板惯例以自定义您的OAuth 2实施。


| 前缀 | 描述 | 示例 |
|---------|----------|---------|
| authData | 访问任何合作伙伴或客户数据字段的值。 | `{{ authData.accessToken }}` |
| response.body | HTTP响应正文 | `{{ response.body.access_token }}` |
| response.status | HTTP响应状态 | `{{ response.status }}` |
| response.headers | HTTP响应标头 | `{{ response.headers.server[0] }}` |
| userContext | 访问有关当前授权尝试的信息 | <ul><li>`{{ userContext.sandboxName }}`</li><li>`{{ userContext.sandboxId }}`</li><li>`{{ userContext.imsOrgId }}`</li><li>`{{ userContext.client }} // the client executing the authorization attempt`</li></ul> |

{style="table-layout:auto"}

## 后续步骤 {#next-steps}

阅读本文后，您现在了解了Adobe Experience Platform支持的OAuth 2授权模式，并知道如何使用OAuth 2授权支持配置您的目标。 接下来，您可以使用Destination SDK设置支持OAuth 2的目标。 阅读[使用Destination SDK配置目标](../../guides/configure-destination-instructions.md)以了解后续步骤。
