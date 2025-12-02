---
title: 客户端状态管理
description: 了解Adobe Experience Platform Edge Network如何管理客户端状态
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: 客户端；状态；管理；边缘；网络；网关；API
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 1%

---

# 客户端状态管理

Edge Network本身是无状态的（它不维护自己的会话）。 但是，有一些用例需要客户端状态持久性，例如：

* 一致的设备标识
* 收集并强制执行用户同意
* 保留个性化会话ID

Edge Network使用状态管理协议，将存储方面的委派给其客户端/SDK，并在其响应中包含状态条目。 对于浏览器，条目将存储为Cookie。

客户端负责存储这些请求并将其包含在所有后续请求中。 客户端还必须按照网关的指示，确保条目正确过期。 当条目存储为Cookie时，浏览器会自动完成所有这些工作。

尽管状态条目始终具有纯`String`值(对调用方/SDK可见)，但您不应以任何方式使用或篡改这些值。 值结构/格式甚至名称本身都可能随时更改，这可能会导致在内部使用状态的客户端出现意外行为。 状态旨在始终由网关本身或其他边缘服务使用。

## 将客户端状态作为元数据保留

响应正文中的[!DNL Edge Network]返回的状态是类型为`Handle`的`state:store`对象。

```json
{
   "requestId":"421036b3-a7ff-480b-a9ab-30adba6eb4f0",
   "handle":[
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1",
               "maxAge":7200,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiY1NDc1ODIxNzIzODk5MDY5MzQzMTIzNjQ1NTczNzExNjE4OTA1MFINCLGOvszNLhABGAEgBKABsY6-zM0uqAGHz-z2y82cul3wAbGOvszNLg==",
               "maxAge":34128000,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
               "value":"general=in",
               "maxAge":15552000,
               "attrs":{
                  "SameSite":"None"
               }
            }
         ],
         "type":"state:store"
      }
   ]
}
```

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| `key` | 字符串 | **必需**。 条目名称。 |
| `value` | 字符串 | *可选*。 条目值。 |
| `maxAge` | 整数 | *可选*&#x200B;条目过期前的时间（秒）。 如果缺少条目，则只能存储当前会话的条目。 |
| `attrs` | `Map<String, String>` | *可选*。 条目属性的可选列表。 对于具有安全引用HTTP标头的所有安全连接，`SameSite`属性均设置为`None`。 |


为了支持多标记(即，同一属性中包含多个SDK实例，这些实例可能引用不同的组织)，所有状态条目都会自动添加前缀`kndctr_`以及URL安全的组织ID。

当客户端SDK在响应中收到`state:store`句柄时，必须执行以下操作：

* 存储客户端条目，遵守网关提供的过期时间。
* 从客户端存储加载它们，并在后续请求中包含所有未过期的条目。

以下是以客户端存储状态传递的请求的示例：

```json
{
   "meta":{
      "state":{
         "entries":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1"
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_personalization_sessionId",
               "value":"0a88f43e-044b-41a6-a4f3-6c2848bbc672"
            }
         ]
      }
   }
}
```

## 在浏览器Cookie中保留客户端状态

使用浏览器客户端时，Edge Network可以自动将条目作为浏览器Cookie保留。 这允许透明状态存储支持，因为默认情况下浏览器遵循状态管理协议。

几乎所有条目在启用和受支持时都会被具体化为第一方Cookie（请参阅下面的注释），但在使用第三方`adobedc.demdex.net`域时，网关还可以存储一些第三方Cookie。

由于条目根据其定义始终绑定到特定范围（设备/应用程序），因此Edge Network只会写入与当前请求上下文兼容的子集。 未写入的条目为
在`state:store`句柄中返回。

通常，应用程序范围的条目始终作为第一方Cookie写入，而设备范围的条目作为第三方Cookie写入。 该决定对于呼叫者是完全透明的，网关根据呼叫上下文决定可以写入哪些条目。

调用方必须通过`meta.state.cookiesEnabled`标志明确启用将客户端状态存储为Cookie的支持：

```json
{
   "meta":{
      "state":{
         "cookiesEnabled":true,
         "domain":"foo.com"
      }
   }
}
```

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| `cookiesEnabled` | 布尔值 | 设置后，将启用对Cookie的支持。 默认值为 `false`。 |
| `domain` | 字符串 | `cookiesEnabled: true`时必需。 应在其上写入Cookie的顶级域。 Edge Network将使用此值来确定状态能否作为Cookie保留。 |

即使通过`cookiesEnabled`标志启用了Cookie支持，Adobe Experience Platform Edge Network也只会在请求顶级域与调用方指定的`domain`匹配时写入状态条目。 当存在不匹配时，会在`state:store`句柄中返回条目。

在以下情况下，无法写入第一方Cookie（即使启用了支持）：

* 请求来自第三方`adobedc.demdex.net`域。
* 请求来自第一方`CNAME`域，不同于调用方在`meta.state.domain`中指定的域。

## Cookie安全性

所有Cookie都尽可能启用[安全标志](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies)。

所有安全Cookie的[SameSite属性](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite)均设置为`None`，这意味着Cookie会在第一方和跨域的所有上下文中发送。

* 对于第一方Cookie (`kndcrt_*`)，仅当请求上下文安全(HTTPS)并且反向链接（`Secure`Referer HTTP标头[）也是HTTPS时，才会设置](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Referer)标志。 如果反向链接不安全(HTTP)，则忽略`Secure`标志以允许Web SDK读取它们。 无法从不安全的上下文中读取安全Cookie。
* 对于第三方Cookie (demdex)，始终设置`Secure`标志，因为所有请求都是HTTPS，因此请求上下文是安全的，并且从不从JavaScript读取此Cookie。

`Secure`标记在Cookie的元数据表示中不存在。 仅包括`SameSite`特性。 在这种情况下，只要存在`Secure`属性，客户端就有责任正确设置`SameSite`标志。 具有`SameSite=None`的Cookie还必须指定`Secure`属性，因为它们需要安全上下文(HTTPS)。
