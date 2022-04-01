---
title: 客户端状态管理
description: 了解Adobe Experience Platform Edge Network如何管理客户端状态
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: 客户端；状态；管理；边缘；网络；网关；API
source-git-commit: eaeab8fe96a9af399f8288b62b6ca9f31d949cfa
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 2%

---


# 客户端状态管理

边缘网络本身是无状态的（它不维护自己的会话）。 但是，在某些用例中，需要客户端状态持久性，例如：

* 一致的设备标识(请参阅 [访客识别](visitor-identification.md))
* 收集并强制用户同意
* 保留个性化会话ID

边缘网络使用状态管理协议，将存储方面委派给其客户端/SDK，并在其响应中包含状态条目。 对于浏览器，这些条目将存储为Cookie。

客户负责存储这些请求并将其包含在所有后续请求中。 客户端还必须按照网关的指示，处理条目的适当过期时间。 当条目存储为Cookie时，浏览器会自动执行所有这些操作。

尽管状态条目总是有一个简单的 `String` 值（对调用方/SDK可见），您不应以任何方式使用或篡改值。 值结构/格式，甚至名称本身可能随时发生更改，这可能会导致内部使用状态的客户端出现意外行为。 状态旨在始终由网关本身或其他边缘服务使用。

## 将客户端状态保留为元数据

返回的状态 [!DNL Edge Network] 在响应主体中为 `Handle` 具有类型的对象 `state:store`.

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
| `key` | 字符串 | **必需**. 条目名称。 |
| `value` | 字符串 | *可选*. 条目值。 |
| `maxAge` | 整数 | *可选* 登录生存时间(TTL)，以秒为单位。 缺少时，应仅存储当前会话的条目。 |
| `attrs` | `Map<String, String>` | *可选*. 条目属性的可选列表。 对于具有安全引用器HTTP标头的所有安全连接， `SameSite` 属性设置为 `None`. |


为支持多标记（即同一属性中的多个SDK实例，这些实例可能会引用不同的组织），所有状态条目会自动添加前缀 `kndctr_` 和URL安全的组织ID。

客户端SDK收到 `state:store` 在响应中处理，它必须执行以下操作：

* 在客户端存储条目，并遵守网关提供的过期时间。
* 从客户端存储加载它们，并在后续请求中包含所有未过期的条目。

以下是一个在客户端存储状态中传递的请求示例：

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

## 在浏览器Cookie中保持客户端状态

使用浏览器客户端时，边缘网络会自动将条目保留为浏览器Cookie。 这允许透明的状态存储支持，因为浏览器默认遵循状态管理协议。

几乎所有条目在启用和支持时都会作为第一方Cookie进行实体化（请参阅下文的注释），但是当第三方时，网关也可以存储一些第三方Cookie `adobedc.demdex.net` 域。

由于条目根据其定义始终绑定到特定范围（设备/应用程序），因此边缘网络将只写入与当前请求上下文兼容的子集。 在 `state:store` 句柄。

通常，应用程序范围的条目始终作为第一方Cookie写入，而设备范围的条目作为第三方Cookie写入。 该决定对呼叫者完全透明，网关根据呼叫上下文决定哪些条目可以写入。

调用方必须通过 `meta.state.cookiesEnabled` 标记：

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
| `cookiesEnabled` | 布尔型 | 设置后，将支持Cookie。 默认值为 `false`。 |
| `domain` | 字符串 | 在 `cookiesEnabled: true`. 应在其中写入Cookie的顶级域。 边缘网络将使用此值来确定状态是否可以作为Cookie持久保留。 |

即使通过 `cookiesEnabled` 标记中，Adobe Experience Platform边缘网络仅在请求顶级域与 `domain` 由调用方指定。 当存在不匹配时，将在 `state:store` 句柄。

在以下情况下，无法写入第一方Cookie（即使启用了支持）：

* 第三方提出请求 `adobedc.demdex.net` 域。
* 请求是第一方 `CNAME` 域，不同于 `meta.state.domain`.

## Cookie安全性

所有Cookie都具有 [安全标志](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) 已启用。

所有安全Cookie都具有 [SameSite属性](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) 设置为 `None`，这意味着Cookie在所有上下文（第一方和跨域）中发送。

* 对于第一方Cookie(`kndcrt_*`)、 `Secure` 标记仅在请求上下文安全(HTTPS)且反向链接([引用HTTP标头](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer))也是HTTPS。 如果反向链接不安全(HTTP)，则 `Secure` 标记被忽略，以允许Web SDK读取它们。 无法从不安全的上下文中读取安全Cookie。
* 对于第三方Cookie(demdex), `Secure` 标记始终设置，因为所有请求都是HTTPS，因此请求上下文是安全的，并且永远不会从JavaScript读取此Cookie。

的 `Secure` 标记不在 [cookie的元数据表示](#state-as-metadata). 仅 `SameSite` 属性。 在这种情况下，客户有责任正确设置 `Secure` 标记 `SameSite` 属性存在。 Cookie与 `SameSite=None` 还必须指定 `Secure` 属性，因为它们需要安全上下文(HTTPS)。
