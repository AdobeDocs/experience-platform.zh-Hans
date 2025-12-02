---
title: cookie
description: 手动写入、编辑或删除标记属性的Cookie。
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 7%

---

# `cookie`

`_satellite.cookie`对象包含允许您写入、编辑或删除标记规则可引用的Cookie的方法。 它是[`js-cookie`](https://github.com/js-cookie/js-cookie)的部分副本，包含该库的许多核心功能。

## `cookie.set()`

`set()`方法会写入您的标记属性可以引用的Cookie。

```ts
_satellite.cookie.set(name: string, value: string, attributes?: {
  expires?: number | Date;
  path?: string;
  domain?: string;
  secure?: boolean;
  sameSite?: 'Strict' | 'Lax' | 'None';
}): string
```

可以使用以下方法参数：

| 名称 | 类型 | 必需 | 描述 |
|---|---|---|---|
| **`name`** | `string` | 是 | Cookie的名称。 |
| **`value`** | `string` | 是 | Cookie的值 |
| **`attributes`** | `object` | 否 | 您希望Cookie具有的其他属性。 |

`attributes`对象支持以下属性：

| 属性名称 | 类型 | 必需 | 默认 | 描述 |
|---|---|---|---|---|
| **`expires`** | `number`或[`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) | 否 | Cookie在浏览器会话结束时过期 | 您希望Cookie过期的天数。 |
| **`path`** | `string` | 否 | Cookie在整个站点中可见 | 在域中显示Cookie的位置。 |
| **`domain`** | `string` | 否 | Cookie对创建它的域可见 | Cookie可见的有效域（具有或不具有子域）。 如果某个域没有包含子域，则该域下的所有子域都可以看到该Cookie。 |
| **`secure`** | `boolean` | 否 | 未设置属性 | 确定Cookie是否需要安全协议(`https://`)。 如果省略，则没有安全协议要求。 |
| **`sameSite`** | `'Strict' \| 'Lax' \| 'None'` | 否 | 未设置属性 | 允许您设置Cookie的[`sameSite`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Set-Cookie#samesitesamesite-value)属性。 如果将`sameSite`设置为`None`，则还必须将`secure`设置为`true`。 |

```js
// Sets a cookie valid across the entire site, expires on session close
_satellite.cookie.set('simple_session_cookie', 'value');

// Sets a cookie that expires 7 days from now, valid across the entire site
_satellite.cookie.set('seven_day_cookie', 'value', { expires: 7 });

// Sets a cookie that expires 14 days from now, valid only on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { expires: 14, path: '/' });

// Cross-site compatible cookie (requires HTTPS)
_satellite.cookie.set('cross_site_cookie', 'value', { secure: true, sameSite: 'None' });
```

调用此方法将写入所需的Cookie，并返回所写入的序列化Cookie字符串。 此字符串主要用于调试或记录目的。

```text
'written_cookie=value; path=/'
```

>[!TIP]
>
>标记对象的早期版本使用了`_satellite.setCookie()`。 `setCookie()`方法已弃用，推荐使用`_satellite.cookie.set()`。

## `cookie.get()`

`get()`方法返回Cookie值。

```ts
_satellite.cookie.get(name: string): string | undefined;
```

| 名称 | 类型 | 必需 | 描述 |
|---|---|---|---|
| **`name`** | `string` | 是 | 要从中检索值的Cookie名称（区分大小写）。 |

如果该Cookie名称存在，则返回Cookie值。 如果Cookie名称不存在，则返回`undefined`。

>[!TIP]
>
>标记对象的早期版本使用了`_satellite.getCookie()`。 `getCookie()`方法已弃用，推荐使用`_satellite.cookie.get()`。

## `cookie.remove()`

`remove()`方法会删除您设置的Cookie。

```ts
_satellite.cookie.remove(name: string, attributes?: {
  path?: string;
  domain?: string;
}): void
```

| 名称 | 类型 | 必需 | 描述 |
|---|---|---|---|
| **`name`** | `string` | 是 | 要删除的Cookie名称。 |
| **`attributes`** | `object` | 否 | 与要删除的Cookie关联的属性。 如果您使用`path`或`domain`属性设置Cookie，请在删除Cookie时包含这些相同的属性。 无法包含这些属性不会删除Cookie。 |

```js
// Creates a session cookie
_satellite.cookie.set('session_cookie', 'Cookie value');

// Removes the above cookie
_satellite.cookie.remove('session_cookie');

// Creates a cookie that is only visible on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { path: '/' });

// This remove method does nothing because it does not match the path and domain attributes of the cookie set
_satellite.cookie.remove('page_specific_cookie');

// This remove method works correctly for the page-specific cookie
_satellite.cookie.remove('page_specific_cookie', { path: '/' });
```

>[!TIP]
>
>标记对象的早期版本使用了`_satellite.removeCookie()`。 `removeCookie()`方法已弃用，推荐使用`_satellite.cookie.remove()`。
