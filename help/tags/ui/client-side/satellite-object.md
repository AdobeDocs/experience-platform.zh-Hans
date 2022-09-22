---
title: 卫星对象引用
description: 了解客户端_satellite对象以及您可以在标记中使用该对象执行的各种功能。
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 42%

---

# 卫星对象引用

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

本文档用作客户端的参考 `_satellite` 对象以及您可以使用该对象执行的各种函数。

## `track`

**代码**

```javascript
_satellite.track(identifier: string [, detail: *] )
```

**示例**

```javascript
_satellite.track('contact_submit', { name: 'John Doe' });
```

`track` 使用已使用核心标记扩展的给定标识符配置的直接调用事件类型触发所有规则。 以上示例使用“直接调用”事件类型触发所有规则，其中配置的标识符为 `contact_submit`。此外，还会传递包含相关信息的可选对象。可以通过在条件或操作的文本字段中输入 `%event.detail%` 或者在“自定义代码”条件或操作的代码编辑器中输入 `event.detail` 来访问详细信息对象。

## `getVar`

**代码**

```javascript
_satellite.getVar(name: string) => *
```

**示例**

```javascript
var product = _satellite.getVar('product');
```

在提供的示例中，如果存在具有匹配名称的数据元素，则将返回数据元素的值。 如果不存在匹配的数据元素，则将检查以前是否使用 `_satellite.setVar()` 设置了具有匹配名称的自定义变量。如果找到匹配的自定义变量，则将返回其值。

>[!NOTE]
>
>您可以使用百分比(`%`)语法以引用数据收集UI中许多表单字段的变量，因此无需调用 `_satellite.getVar()`. 例如，使用 `%product%` 将访问产品数据元素或自定义变量的值。

当事件触发规则时，您可以传递规则的相应 `event` 对象 `_satellite.getVar()` 如此：

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

## `setVar`

**代码**

```javascript
_satellite.setVar(name: string, value: *)
```

**示例**

```javascript
_satellite.setVar('product', 'Circuit Pro');
```

`setVar()` 设置具有给定名称和值的自定义变量。 之后可以使用 `_satellite.getVar()` 访问该变量的值。

您可以选择一次设置多个变量，方法是传递一个对象，其中键是变量名称，值是各自的变量值。

```javascript
_satellite.setVar({ 'product': 'Circuit Pro', 'category': 'hobby' });
```

## `getVisitorId`

**代码**

```javascript
_satellite.getVisitorId() => Object
```

**示例**

```javascript
var visitorIdInstance = _satellite.getVisitorId();
```

如果资产上安装了 [!DNL Adobe Experience Cloud ID] 扩展，此方法将返回访客 ID 实例。有关详细信息，请参阅 [Experience Cloud ID 服务文档](https://experienceleague.adobe.com/docs/id-service/using/home.html)。

## `logger`

**代码**

```javascript
_satellite.logger.log(message: string)
```

```javascript
_satellite.logger.info(message: string)
```

```javascript
_satellite.logger.warn(message: string)
```

```javascript
_satellite.logger.error(message: string)
```

**示例**

```javascript
_satellite.logger.error('No product ID found.');
```

的 `logger` 对象允许消息记录到浏览器控制台。 仅当用户启用了标记调试(通过调用 `_satellite.setDebug(true)` 或使用适当的浏览器扩展)。

### 记录弃用警告

```javascript
_satellite.logger.deprecation(message: string)
```

**示例**

```javascript
_satellite.logger.deprecation('This method is no longer supported, please use [new example] instead.');
```

这会将警告记录到浏览器控制台。 无论用户是否启用了标记调试，都会显示该消息。

## `cookie` {#cookie}

`_satellite.cookie` 包含用于读取和写入Cookie的函数。 它是第三方库js-cookie的公开副本。 有关此库更高级用法的详细信息，请查看 [js-cookie文档](https://www.npmjs.com/package/js-cookie#basic-usage).

### 设置Cookie {#cookie-set}

要设置Cookie，请使用 `_satellite.cookie.set()`.

**代码**

```javascript
_satellite.cookie.set(name: string, value: string[, attributes: Object])
```

>[!NOTE]
>
>在旧 [`setCookie`](#setCookie) 设置cookie的方法中，此函数调用的第三个（可选）参数是一个整数，表示cookie的生存时间(TTL)（以天为单位）。 在此新方法中，“属性”对象被接受为第三个参数。 要使用新方法为Cookie设置TTL，您必须提供 `expires` 属性，并将其设置为所需的值。 以下示例中演示了这一点。

**示例**

以下函数调用会写入一个在一周后过期的Cookie。

```javascript
_satellite.cookie.set('product', 'Circuit Pro', { expires: 7 });
```

### 检索Cookie {#cookie-get}

要检索Cookie，请使用 `_satellite.cookie.get()`.

**代码**

```javascript
_satellite.cookie.get(name: string) => string
```

**示例**

以下函数调用会读取之前设置的Cookie。

```javascript
var product = _satellite.cookie.get('product');
```

### 删除Cookie {#cookie-remove}

要删除Cookie，请使用 `_satellite.cookie.remove()`.

**代码**

```javascript
_satellite.cookie.remove(name: string)
```

**示例**

以下函数调用会删除之前设置的Cookie。

```javascript
_satellite.cookie.remove('product');
```

## `buildInfo`

**代码**

```javascript
_satellite.buildInfo
```

此对象包含有关当前标记运行时库的生成信息。 该对象包含以下属性：

### `turbineVersion`

这提供了 [涡轮](https://www.npmjs.com/package/@adobe/reactor-turbine) 当前库中使用的版本。

### `turbineBuildDate`

生成容器内使用的 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 版本的 ISO 8601 日期。

### `buildDate`

生成当前库的 ISO 8601 日期。

以下示例展示了对象值：

```javascript
{
  turbineVersion: "14.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z"
}
```

## `environment`

此对象包含有关当前标记运行时库所部署的环境的信息。

**代码**

```javascript
_satellite.environment
```

该对象包含以下属性：

```javascript
{
  id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
  stage: "development"
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 环境的id。 |
| `stage` | 生成此库的环境。可能的值为 `development`, `staging`和 `production`. |

## `notify`

>[!NOTE]
>
>此方法已弃用。请改用 `_satellite.logger.log()`。

**代码**

```javascript
_satellite.notify(message: string[, level: number])
```

**示例**

```javascript
_satellite.notify('Hello world!');
```

`notify` 将消息记录到浏览器控制台。 仅当用户启用了标记调试(通过调用 `_satellite.setDebug(true)` 或使用适当的浏览器扩展)。

可以传递可选的日志记录级别，这将影响所记录消息的样式和过滤。 支持的级别包括：

3 - 信息性消息。

4 - 警告消息。

5 - 错误消息。

如果您未提供日志记录级别或未传递任何其他级别值，则消息将记录为常规消息。

## `setCookie` {#setCookie}

>[!IMPORTANT]
>
>此方法已弃用。请改用 [`_satellite.cookie.set()`](#cookie-set)。

**代码**

```javascript
_satellite.setCookie(name: string, value: string, days: number)
```

**示例**

```javascript
_satellite.setCookie('product', 'Circuit Pro', 3);
```

这会在用户的浏览器中设置Cookie。 Cookie 将持续保留指定的天数。

## `readCookie`

>[!IMPORTANT]
>
>此方法已弃用。请改用 [`_satellite.cookie.get()`](#cookie-get)。

**代码**

```javascript
_satellite.readCookie(name: string) => string
```

**示例**

```javascript
var product = _satellite.readCookie('product');
```

这会从用户的浏览器中读取Cookie。

## `removeCookie`

>[!NOTE]
>
>此方法已弃用。请改用 [`_satellite.cookie.remove()`](#cookie-remove)。

**代码**

```javascript
_satellite.removeCookie(name: string)
```

**示例**

```javascript
_satellite.removeCookie('product');
```

这会从用户的浏览器中删除Cookie。

## 调试函数

不应从生产代码访问以下函数。 这些函数仅用于调试目的，并将根据需要随时间发生更改。

### `container`

**代码**

```javascript
_satellite._container
```

**示例**

>[!IMPORTANT]
>
>不应从生产代码访问此函数。 此函数仅用于调试目的，并将根据需要随时间发生更改。

### `monitor`

**代码**

```javascript
_satellite._monitors
```

**示例**

>[!IMPORTANT]
>
>不应从生产代码访问此函数。 此函数仅用于调试目的，并将根据需要随时间发生更改。

**样例**

在运行标记库的网页上，向HTML中添加一个代码片段。 通常，代码会插入到 `<head>` 元素之前 `<script>` 元素。 这允许监视器捕获标记库中最早发生的系统事件。 例如：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window._satellite = window._satellite || {};
    window._satellite._monitors = window._satellite._monitors || [];
    window._satellite._monitors.push({
      ruleTriggered: function (event) {
        console.log(
          'rule triggered',
          event.rule
        );
      },
      ruleCompleted: function (event) {
        console.log(
          'rule completed',
          event.rule
        );
      },
      ruleConditionFailed: function (event) {
        console.log(
          'rule condition failed',
          event.rule,
          event.condition
        );
      }
    });
  </script>
  <script src="//assets.adobedtm.com/launch-EN5bfa516febde4b22b3e7c6f96f6b439f.min.js"
          async></script>
</head>
<body>
  <h1>Click me!</h1>
</body>
</html>
```

在第一个脚本元素中，由于尚未加载标记库，因此初始 `_satellite` 创建对象，并在上创建数组 `_satellite._monitors` 已初始化。 然后，此脚本将一个监视器对象添加到该数组。监视器对象可以指定以下方法，标记库稍后将调用这些方法：

### `ruleTriggered`

此函数在事件触发规则后但在处理规则条件和操作之前调用。 传递给 `ruleTriggered` 的事件对象包含有关已触发的规则的信息。

### `ruleCompleted`

在规则完全处理后，将调用此函数。 换言之，事件已发生，所有条件都已传递，所有操作都已执行。 传递给的事件对象 `ruleCompleted` 包含有关已完成的规则的信息。

### `ruleConditionFailed`

在触发规则且其某个条件失败后，将调用此函数。 传递给 `ruleConditionFailed` 的事件对象包含有关已触发的规则和失败的条件的信息。

如果调用 `ruleTriggered`，则此后不久将调用 `ruleCompleted` 或 `ruleConditionFailed`。

>[!NOTE]
>
>监视器不必指定所有三种方法（`ruleTriggered`、`ruleCompleted` 和 `ruleConditionFailed`）。Adobe Experience Platform中的标记可与监视器提供的任何受支持的方法配合使用。

### 测试监视器

上面的示例在监视器中指定了所有三种方法。当这些方法被调用时，监视器会记录相关信息。要测试此监视器，请在标记库中设置两个规则：

1. 具有一个点击事件和一个浏览器条件（仅当浏览器为 [!DNL Chrome] 时才传递）的规则。
1. 具有一个点击事件和一个浏览器条件（仅当浏览器为 [!DNL Firefox] 时才传递）的规则。

如果您在 [!DNL Chrome] 中打开页面，打开浏览器控制台，然后选择该页面，则控制台中会显示以下内容：

![](../../images/debug.png)

可以根据需要向这些处理程序添加其他挂接或其他信息。
