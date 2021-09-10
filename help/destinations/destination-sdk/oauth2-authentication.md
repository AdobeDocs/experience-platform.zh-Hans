---
description: 本页介绍了目标SDK支持的各种OAuth 2身份验证流，并提供了为目标设置OAuth 2身份验证的说明。
title: OAuth 2身份验证
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 9be8636b02a15c8f16499172289413bc8fb5b6f0
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 5%

---

# OAuth 2身份验证

## 概述 {#overview}

使用目标SDK ，允许Adobe Experience Platform使用[OAuth 2身份验证框架](https://tools.ietf.org/html/rfc6749)连接到您的目标。

本页介绍了目标SDK支持的各种OAuth 2身份验证流，并提供了为目标设置OAuth 2身份验证的说明。

## 如何将OAuth 2身份验证详细信息添加到目标配置 {#how-to-setup}

### 系统中的先决条件 {#prerequisites}

第一步，您必须在系统中为Adobe Experience Platform创建应用程序，或在系统中注册Experience Platform。 目标是生成客户端ID和客户端密钥，验证目标Experience Platform所需的客户端ID和客户端密钥。 作为系统中此配置的一部分，您需要Adobe Experience Platform OAuth 2重定向/回调URL，您可以从下表中获取该URL。

>[!IMPORTANT]
>
>只有具有授权代码](./oauth2-authentication.md#authorization-code)授予类型的[OAuth 2的OAuth才需要在系统中为Adobe Experience Platform注册重定向/回调URL的步骤。 对于其他两种受支持的授权类型（密码和客户端凭据），您可以跳过此步骤。

| 重定向/回调URL | 环境 |
|---------|----------|
| `https://platform.adobe.io/data/core/activation/oauth/api/v1/callback` | 生产 |
| `https://platform-stage.adobe.io/data/core/activation/oauth/api/v1/callback` | 暂存 |

{style=&quot;table-layout:auto&quot;}

在此步骤结束时，您应该：
* 客户ID;
* 客户密码；
* Adobe的回调URL（用于授权代码授予）。

### 您在目标SDK中需要执行的操作 {#to-do-in-destination-sdk}

要在Experience Platform中为目标设置OAuth 2身份验证，必须使用`platform.adobe.io/data/core/activation/authoring/destinations` [ API端点](./destination-configuration-api.md)在`customerAuthenticationConfigurations`参数下将OAuth 2详细信息添加到[目标配置](./destination-configuration.md)中。 请参阅[示例配置](./destination-configuration.md#example-configuration)。 根据OAuth 2身份验证授权类型，此页面下面将进一步说明您需要向配置模板添加哪些字段。

## 支持的OAuth 2授权类型 {#oauth2-grant-types}

Experience Platform支持下表中的三种OAuth 2授权类型。 如果您设置了自定义OAuth 2，则Adobe可以在集成中的自定义字段帮助下支持它。 有关更多信息，请参阅每种授权类型的章节。

>[!IMPORTANT]
>
>* 按照以下部分的说明提供输入参数。 Adobe内部系统连接到您平台的身份验证系统并获取输出参数，这些参数用于对用户进行身份验证并维护对目标的身份验证。
>* 表中以粗体突出显示的输入参数是OAuth 2身份验证流程中的必需参数。 其他参数是可选的。 此处未显示其他自定义输入参数，但在[自定义OAuth 2配置](./oauth2-authentication.md#customize-configuration)和[访问令牌刷新](./oauth2-authentication.md#access-token-refresh)章节中对这些参数进行了详细介绍。


| OAuth 2授予 | 输入 | 输出 |
|---------|----------|---------|
| 授权代码 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>范围</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| 密码 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>范围</li><li><b>accessTokenUrl</b></li><li><b>用户名</b></li><li><b>密码</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| 客户端凭据 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>范围</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

上表列出了在标准OAuth 2流中使用的字段。 除了这些标准字段外，各种合作伙伴集成可能还需要额外的输入和输出。 Adobe为目标SDK设计了一个灵活的OAuth 2身份验证/授权框架，该框架可以处理上述标准字段模式的变体，同时支持自动重新生成无效输出（如过期的访问令牌）的机制。

在所有情况下，输出都包含访问令牌，Experience Platform使用该令牌来验证和维护对目标的身份验证。

Adobe为OAuth 2身份验证设计的系统：
* 支持所有三个OAuth 2授权，同时考虑其中任何变体，例如附加数据字段、非标准API调用等。
* 支持具有不同生命周期值（无论是90天、30分钟还是您指定的任何其他生命周期值）的访问令牌。
* 支持具有或不具有刷新令牌的OAuth 2授权流。

## 具有授权代码的OAuth 2 {#authorization-code}

如果您的目标支持标准OAuth 2.0授权代码流（请阅读[RFC标准规范](https://tools.ietf.org/html/rfc6749#section-4.1)）或其变体，请查阅以下必填和可选字段：

| OAuth 2授予 | 输入 | 输出 |
|---------|----------|---------|
| 授权代码 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>范围</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

要为目标设置此身份验证方法，请在`/destinations` [endpoint](./destination-configuration.md)中将以下行添加到配置中：

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
| `accessTokenUrl` | 字符串 | 您的URL，该URL会出现访问令牌和（可选）刷新令牌的问题。 |
| `authorizationUrl` | 字符串 | 授权服务器的URL，用于将用户重定向到您的应用程序以登录。 |
| `refreshTokenUrl` | 字符串 | *可选.* 您的URL，会导致刷新令牌问题。通常，`refreshTokenUrl`与`accessTokenUrl`相同。 |
| `clientId` | 字符串 | 您的系统分配给Adobe Experience Platform的客户端ID。 |
| `clientSecret` | 字符串 | 您的系统分配给Adobe Experience Platform的客户端密钥。 |
| `scope` | 字符串列表 | *可选*. 设置访问令牌允许Experience Platform对您的资源执行的操作范围。 示例：“读，写”。 |

{style=&quot;table-layout:auto&quot;}

## 具有密码授予的OAuth 2

对于OAuth 2密码授权（请阅读[RFC标准规范](https://tools.ietf.org/html/rfc6749#section-4.3)），Experience Platform需要用户的用户名和密码。 在身份验证流程中，Experience Platform为访问令牌和（可选）刷新令牌交换这些凭据。
Adobe利用以下标准输入简化目标配置，并能够覆盖值：

| OAuth 2授予 | 输入 | 输出 |
|---------|----------|---------|
| 密码 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>范围</li><li><b>accessTokenUrl</b></li><li><b>用户名</b></li><li><b>密码</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
> 您无需在以下配置中为`username`和`password`添加任何参数。 在目标配置中添加`"grant": "OAUTH2_PASSWORD"`时，当用户对您的目标进行身份验证时，系统将请求用户在Experience PlatformUI中提供用户名和密码。

要为目标设置此身份验证方法，请在`/destinations` [endpoint](./destination-configuration.md)中将以下行添加到配置中：

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
| `accessTokenUrl` | 字符串 | 您的URL，该URL会出现访问令牌和（可选）刷新令牌的问题。 |
| `clientId` | 字符串 | 您的系统分配给Adobe Experience Platform的客户端ID。 |
| `clientSecret` | 字符串 | 您的系统分配给Adobe Experience Platform的客户端密钥。 |
| `scope` | 字符串列表 | *可选*. 设置访问令牌允许Experience Platform对您的资源执行的操作范围。 示例：“读，写”。 |

{style=&quot;table-layout:auto&quot;}

## 具有客户端凭据授予的OAuth 2

您可以配置OAuth 2客户端凭据（阅读[RFC标准规范](https://tools.ietf.org/html/rfc6749#section-4.4)）目标，该目标支持下面列出的标准输入和输出。 您可以自定义值。 有关详细信息，请参阅[自定义OAuth 2配置](./oauth2-authentication.md#customize-configuration)。

| OAuth 2授予 | 输入 | 输出 |
|---------|----------|---------|
| 客户端凭据 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>范围</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

要为目标设置此身份验证方法，请在`/destinations` [endpoint](./destination-configuration.md)中将以下行添加到配置中：

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
| `accessTokenUrl` | 字符串 | 授权服务器的URL，用于发出访问令牌和可选刷新令牌。 |
| `refreshTokenUrl` | 字符串 | *可选.* 您的URL，会导致刷新令牌问题。通常，`refreshTokenUrl`与`accessTokenUrl`相同。 |
| `clientId` | 字符串 | 您的系统分配给Adobe Experience Platform的客户端ID。 |
| `clientSecret` | 字符串 | 您的系统分配给Adobe Experience Platform的客户端密钥。 |
| `scope` | 字符串列表 | *可选*. 设置访问令牌允许Experience Platform对您的资源执行的操作范围。 示例：“读，写”。 |

{style=&quot;table-layout:auto&quot;}

## 自定义OAuth 2配置 {#customize-configuration}

上述部分中描述的配置描述了标准OAuth 2授予。 但是，由Adobe设计的系统具有灵活性，因此您可以将自定义参数用于OAuth 2授权中的任何变量。 要自定义标准OAuth 2设置，请使用`authenticationDataFields`参数，如以下示例中所示。

### 示例1:使用`authenticationDataFields`捕获来自身份验证响应的信息 {#example-1}

在此示例中，目标平台具有在特定时间后过期的刷新令牌。 在这种情况下，合作伙伴会设置`refreshTokenExpiration`自定义字段，以从API响应中的`refresh_token_expires_in`字段获取刷新令牌到期时间。

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

### 示例2:使用`authenticationDataFields`提供特殊的刷新令牌 {#example-2}

在此示例中，合作伙伴设置其目标以提供特殊的刷新令牌。 此外，访问令牌的过期日期不会在API响应中返回，因此他们可以硬编码默认值（在此例中为3600秒）。

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

### 示例3:用户在配置目标时输入客户端ID和客户端密钥 {#example-3}

在此示例中，客户无需创建全局客户端ID和客户端密钥（如[系统](./oauth2-authentication.md#prerequisites)的先决条件部分中所示），而是需要输入客户端ID、客户端密钥和帐户ID（客户用于登录到目标的ID）

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
                    "fieldType": "CUSTOMER"
                },
                {
                    "name": "clientSecret",
                    "title": "Client Secret",
                    "description": "Client Secret",
                    "type": "string",
                    "isRequired": true,
                    "format": "password",
                    "fieldType": "CUSTOMER"
                },
                {
                    "name": "moviestarId",
                    "title": "Moviestar ID",
                    "description": "Moviestar ID",
                    "type": "string",
                    "isRequired": true,
                    "fieldType": "CUSTOMER"
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
| `authenticationDataFields.type` | 字符串 | 定义自定义数据字段的类型。 <br> 接受的值： `string`,  `boolean`  `integer` |
| `authenticationDataFields.isRequired` | 布尔型 | 指定身份验证流程中是否需要自定义数据字段。 |
| `authenticationDataFields.format` | 字符串 | 选择`"format":"password"`时，Adobe会加密身份验证数据字段的值。 与`"fieldType": "CUSTOMER"`一起使用时，当用户在字段中键入内容时，这也会隐藏UI中的输入。 |
| `authenticationDataFields.fieldType` | 字符串 | 指示输入是来自合作伙伴（您）还是来自用户，用户以Experience Platform设置目标时。 |
| `authenticationDataFields.value` | 字符串. 布尔型. 整数 | 自定义数据字段的值。 值与`authenticationDataFields.type`中的选定类型匹配。 |
| `authenticationDataFields.authenticationResponsePath` | 字符串 | 指示您引用的API响应路径中的哪个字段。 |

{style=&quot;table-layout:auto&quot;}

## 访问令牌刷新 {#access-token-refresh}

Adobe设计了一个系统，该系统可刷新过期的访问令牌，而无需用户重新登录您的平台。 系统能够生成新令牌，以便客户能够继续无缝地激活到您的目标。

要设置访问令牌刷新，您可能需要配置一个模板化HTTP请求，以便Adobe使用刷新令牌获取新的访问令牌。 如果访问令牌已过期，则Adobe会获取您提供的模板请求，并添加您提供的参数。 使用`accessTokenRequest`参数配置访问令牌刷新机制。


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

您可以在`accessTokenRequest`中使用以下参数来自定义令牌刷新过程：

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | 字符串 | 使用 `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | 字符串 | <ul><li>如果对`accessTokenRequest.urlBasedDestination.url.value`中的值使用模板，则使用`PEBBLE_V1`。</li><li> 如果字段`accessTokenRequest.urlBasedDestination.url.value`中的值是常量，则使用`NONE`。 </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | 字符串 | Experience Platform请求访问令牌的URL。 |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | 字符串 | <ul><li>如果对`accessTokenRequest.httpTemplate.requestBody.value`中的值使用模板，则使用`PEBBLE_V1`。</li><li> 如果字段`accessTokenRequest.httpTemplate.requestBody.value`中的值是常量，则使用`NONE`。 </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | 字符串 | 使用模板语言对访问令牌端点的HTTP请求中的字段进行自定义。 有关如何使用模板来自定义字段的信息，请参阅[模板约定](./oauth2-authentication.md#templating-conventions)一节。 |
| `accessTokenRequest.httpTemplate.httpMethod` | 字符串 | 指定用于调用访问令牌端点的HTTP方法。 在大多数情况下，此值为`POST`。 |
| `accessTokenRequest.httpTemplate.contentType` | 字符串 | 指定对访问令牌端点的HTTP调用的内容类型。 <br> 例如： `application/x-www-form-urlencoded` 或 `application/json`。 |
| `accessTokenRequest.httpTemplate.headers` | 字符串 | 指定是否应将任何标头添加到访问令牌端点的HTTP调用中。 |
| `accessTokenRequest.responseFields.templatingStrategy` | 字符串 | <ul><li>如果对`accessTokenRequest.responseFields.value`中的值使用模板，则使用`PEBBLE_V1`。</li><li> 如果字段`accessTokenRequest.responseFields.value`中的值是常量，则使用`NONE`。 </li></li> |
| `accessTokenRequest.responseFields.value` | 字符串 | 使用模板语言从访问令牌端点访问HTTP响应中的字段。 有关如何使用模板来自定义字段的信息，请参阅[模板约定](./oauth2-authentication.md#templating-conventions)一节。 |
| `accessTokenRequest.validations.name` | 字符串 | 指示您为此验证提供的名称。 |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | 字符串 | <ul><li>如果对`accessTokenRequest.validations.actualValue.value`中的值使用模板，则使用`PEBBLE_V1`。</li><li> 如果字段`accessTokenRequest.validations.actualValue.value`中的值是常量，则使用`NONE`。 </li></li> |
| `accessTokenRequest.validations.actualValue.value` | 字符串 | 使用模板语言访问HTTP响应中的字段。 有关如何使用模板来自定义字段的信息，请参阅[模板约定](./oauth2-authentication.md#templating-conventions)一节。 |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | 字符串 | <ul><li>如果对`accessTokenRequest.validations.expectedValue.value`中的值使用模板，则使用`PEBBLE_V1`。</li><li> 如果字段`accessTokenRequest.validations.expectedValue.value`中的值是常量，则使用`NONE`。 </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | 字符串 | 使用模板语言访问HTTP响应中的字段。 有关如何使用模板来自定义字段的信息，请参阅[模板约定](./oauth2-authentication.md#templating-conventions)一节。 |

{style=&quot;table-layout:auto&quot;}

## 模板惯例 {#templating-conventions}

根据您的身份验证自定义，您可能需要访问身份验证响应中的数据字段，如上一节中所示。 为此，请熟悉Adobe使用的[Pebble模板语言](https://pebbletemplates.io/)，并参阅以下模板约定以自定义您的OAuth 2实施。


| 前缀 | 描述 | 示例 |
|---------|----------|---------|
| authData | 访问任何合作伙伴或客户数据字段的值。 | ``{{ authData.accessToken }}`` |
| response.body | HTTP响应主体 | ``{{ response.body.access_token }}`` |
| response.status | HTTP响应状态 | ``{{ response.status }}`` |
| response.headers | HTTP响应头 | ``{{ response.headers.server[0] }}`` |
| authContext | 访问有关当前身份验证尝试的信息 | <ul><li>`{{ authContext.sandboxName }} `</li><li>`{{ authContext.sandboxId }} `</li><li>`{{ authContext.imsOrgId }} `</li><li>`{{ authContext.client }} // the client executing the authentication attempt `</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 后续步骤 {#next-steps}

通过阅读本文，您现在了解了Adobe Experience Platform支持的OAuth 2身份验证模式，并了解如何使用OAuth 2身份验证支持配置目标。 接下来，您可以使用目标SDK设置OAuth 2支持的目标。 阅读[使用目标SDK配置目标](./configure-destination-instructions.md)以执行后续步骤。
